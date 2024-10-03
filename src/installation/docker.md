# Docker
*How to run a Erigon node with Docker*

Using Docker allows starting Erigon packaged as a Docker image without installing the program directly on your system.
General Info

## General info

* The released archive now comprises 10 key binaries: erigon, downloader, devnet, EVM, caplin, diag, integration, RPCDaemon, Sentry, and txpool;
* The new Docker images feature seven binaries: erigon, integration, diag, Sentry, txpool, downloader, and RPCDaemon (same binaries included in the released archive);
* Multi-platform docker image available for linux/amd64/v2 and linux/arm64 platforms and based on alpine:3.20.2; No need to pull another docker image for another different platform.
* The Docker image is now compatible with multiple platforms: Linux (amd64, v2) and arm64. It's built on top of Alpine 3.20.2;
* All build flags now passed to the release workflow — so, user can see previously missed build info in our released binaries (as well as in docker images) and also better build optimization expected;
* With recent updates, all build configurations are now included in the release process. This provides users with more comprehensive build information for both binaries and Docker images, along with enhanced build optimizations..

## Download and start Erigon in Docker

Here are the steps to download and start Erigon 3 in Docker:

* Install Docker Desktop on Mac, Windows, or Linux.

* Check the Erigon Docker Hub page to see the available releases.

* Download the latest version:
```bash
docker pull erigontech/erigon:main-latest
```
* List the downloaded images to get the IMAGE ID:
```bash
docker images
```
* Check which Erigon version has been downloaded:
```bash
docker run -it <image_id> --v
```
* If you want to start Erigon add the options according to the usage page or the advanced customization page. For example:
```bash
docker run -it a3867a12bd23 --chain=holesky --prune.mode=minimal
```
* When done, exit the container or press `Ctrl+C`. The container will stop.

## Optional: Setup dedicated user

User UID/GID need to be synchronized between the host OS and container so files are written with correct permission.

You may wish to setup a dedicated user/group on the host OS, in which case the following `make` targets are available.

```bash
# create "erigon" user
make user_linux
# or
make user_macos
```

### Environment Variables

There is a `.env.example` file in the root of the repo.
```
* DOCKER_UID - The UID of the docker user

* DOCKER_GID - The GID of the docker user

* XDG_DATA_HOME - The data directory which will be mounted to the docker containers
```

If not specified, the UID/GID will use the current user.

A good choice for `XDG_DATA_HOME` is to use the `~erigon/.ethereum` directory created by helper targets `make user_linux` or `make user_macos`.

### Check: Permissions

In all cases, `XDG_DATA_HOME` (specified or default) must be writeable by the user UID/GID in docker, which will be determined by the `DOCKER_UID` and `DOCKER_GID` at build time.

If a build or service startup is failing due to permissions, check that all the directories, UID, and GID controlled by these environment variables are correct.

### Run

Next command starts: Erigon on port 30303, rpcdaemon on port 8545, prometheus on port 9090, and grafana on port 3000:

```
#
# Will mount ~/.local/share/erigon to /home/erigon/.local/share/erigon inside container
#
make docker-compose
#
# or
#
# if you want to use a custom data directory
# or, if you want to use different uid/gid for a dedicated user
#
# To solve this, pass in the uid/gid parameters into the container.
#
# DOCKER_UID: the user id
# DOCKER_GID: the group id
# XDG_DATA_HOME: the data directory (default: ~/.local/share)
#
# Note: /preferred/data/folder must be read/writeable on host OS by user with UID/GID given
#       if you followed above instructions
#
# Note: uid/gid syntax below will automatically use uid/gid of running user so this syntax
#       is intended to be run via the dedicated user setup earlier
#
DOCKER_UID=$(id -u) DOCKER_GID=$(id -g) XDG_DATA_HOME=/preferred/data/folder DOCKER_BUILDKIT=1 COMPOSE_DOCKER_CLI_BUILD=1 make docker-compose
#
# if you want to run the docker, but you are not logged in as the $ERIGON_USER
# then you'll need to adjust the syntax above to grab the correct uid/gid
#
# To run the command via another user, use
#
ERIGON_USER=erigon
sudo -u ${ERIGON_USER} DOCKER_UID=$(id -u ${ERIGON_USER}) DOCKER_GID=$(id -g ${ERIGON_USER}) XDG_DATA_HOME=~${ERIGON_USER}/.ethereum DOCKER_BUILDKIT=1 COMPOSE_DOCKER_CLI_BUILD=1 make docker-compose
```

`Makefile` creates the initial directories for Erigon, Prometheus and Grafana. The PID namespace is shared between erigon and rpcdaemon which is required to open Erigon's DB from another process (RPCDaemon local-mode). See: [https://github.com/ledgerwatch/erigon/pull/2392/files](https://github.com/ledgerwatch/erigon/pull/2392/files)

If your docker installation requires the docker daemon to run as root (which is by default), you will need to prefix the command above with `sudo`. However, it is sometimes recommended running docker (and therefore its containers) as a non-root user for security reasons. For more information about how to do this, refer to this [article](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

<div class="warning">
Windows support for docker-compose is not ready yet.
<div>