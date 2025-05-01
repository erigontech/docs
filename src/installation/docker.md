# Docker
*How to run a Erigon node with Docker*

Using Docker allows starting Erigon packaged as a Docker image without installing the program directly on your system.

### General Info

- The released archive now comprises 10 key binaries: Erigon, Downloader, Devnet, EVM, Caplin, Diag, Integration, RPCDaemon, Sentry, and Txpool;
- The new Docker images feature seven binaries: Erigon, Integration, Diag, Sentry, Txpool, Downloader, and RPCDaemon (same binaries included in the released archive);
- Multi-platform Docker image available for linux/amd64/v2 and linux/arm64 platforms and based on alpine:3.20.2; No need to pull another Docker image for another different platform.
- The Docker image is now compatible with multiple platforms: Linux (amd64, v2) and arm64. It's built on top of Alpine 3.20.2;
- All build flags now passed to the release workflow — so, user can see previously missed build info in our released binaries (as well as in Docker images) and also better build optimization expected;
- With recent updates, all build configurations are now included in the release process. This provides users with more comprehensive build information for both binaries and Docker images, along with enhanced build optimizations..
- Images are stored at <https://hub.docker.com/r/erigontech/erigon>.


## Prerequisites

Having Docker Engine installed, see instructions [here](https://docs.docker.com/engine/install/).

## Download and start Erigon in Docker

Here are the steps to download and start Erigon in Docker:

1. Download the latest version:

```bash
docker pull erigontech/erigon
```

2. List the downloaded images to get the IMAGE ID:

```bash
docker images
```

3. Check which Erigon version has been downloaded:

```bash
docker run -it <image_id> --v
```

If you want to start Erigon add the options according to the [basic usage](/basic-usage.md) page or the advanced customization page. For example:

```bash
docker run -it 36f25992dd1a --chain=holesky --prune.mode=minimal
```

To exit the container press `Ctrl+C`; the container will stop.

## Docker Compose for basic users

Another option is to use Docker Compose. Docker Compose is a tool for defining and running multi-container Docker applications. It allows users to configure application services using a YAML file to start up all the services with a single command.

For Linux systems, Docker Compose must be installed separately, see instructions [here](https://docs.docker.com/compose/install/).

If you are running Docker on a single-user system, where you're the only user, you don't need to create a dedicated user/group.

<div class="warning">
Windows support for docker-compose is not ready yet.
</div>

### Create a YAML file for Erigon

#### Create a new file called `docker-compose.yml` in a directory of your choice (e.g., `~/erigon`)

The example of the YAML file defines two services: **execution** and **consensus**. Each service has its own configuration, including:
- `container_name`: The name of the container, in this case the network and the prune mode.
- `image`: The Docker image to use.
- `restart`: The restart policy.
- `volumes`: The volumes to mount.
- `networks`: The networks to connect to.
- `ports`: The ports to expose.
- `expose`: The ports to expose.
- `command`: The command to run when the container starts.
- `user`: The user run the container as.
- `logging`: The logging configuration.

The execution service uses the `erigontech/erigon:-latest` image and runs the Erigon client with various options.

```YAML
services:
  erigon:
    container_name: chiado_minimal
    image: erigontech/erigon:main-latest
    restart: unless-stopped
    volumes:
      - $PWD/erigon:/home/erigon/data
    ports:
      - 30323:30303
      - 30323:30303/udp
      - 30324:30304
      - 30324:30304/udp
      - 42089:42069
      - 42089:42069/udp
      - 4020:4000/udp
      - 4021:4001
      - 8565:8545
    expose:
      - 8545
    command: |
      --prune.mode=minimal
      --chain=chiado
      --datadir=/home/erigon/data
      --http
      --http.api=eth,erigon,web3,net,debug,trace,txpool,parity,admin,ots
      --http.addr=0.0.0.0
      --http.corsdomain=*
      --metrics
      --metrics.addr=0.0.0.0
      --pprof
      --pprof.addr=0.0.0.0
      --pprof.port=6070
      --authrpc.addr=0.0.0.0
      --authrpc.jwtsecret=/jwt
      --authrpc.vhosts=*
      --torrent.download.rate=10mb
      --torrent.upload.rate=1mb
    user: 0:0
```

### Start the Docker Compose services

Open your terminal into the directory where you created the above docker-compose.yml and type:

```bash
docker compose up -d
```

The containers will start as described in the YAML file, in detached mode. You can verify the output by typing

```bash
docker compose ps
```

To see containers log use:

```bash
docker compose logs -f
```

To stop the containers, you can use the following command:

```bash
docker compose stop
```

This command will stop the containers, but it won't remove them. If you want to remove the containers as well, you can use the following command:

```bash
docker compose down
```

This command will stop and remove the containers, as well as any networks that were created.


## Docker Compose for advanced users

Another option is to use Docker Compose. Docker Compose is a tool for defining and running multi-container Docker applications. It allows users to configure application services using a YAML file to start up all the services with a single command.

> For Linux systems, Docker Compose must be installed separately, see instructions [here](https://docs.docker.com/compose/install/).

### Optional: Setup dedicated user

User UID/GID need to be synchronized between the host OS and container so files are written with correct permission.

You may wish to setup a dedicated user/group on the host OS in order to have improved security and isolation, better resource management and control, easier auditing and logging and reduced risk of compromise impacting the host system.

You can do this by running the following commands:

Optional: Setup dedicated user

User UID/GID need to be synchronized between the host OS and container so files are written with correct permission.

You may wish to setup a dedicated user/group on the host OS, in which case the following make targets are available.

```bash
# create "erigon" user
make user_linux
# or
make user_macos
```

You can skip this step if you're running Docker on a single-user system, where you're the only user, since the risks associated with not creating a dedicated user are low.

### Environment Variables

There's a file called `.env.example` in the root of the repository that contains environment variables. These variables are used to configure the Docker containers. The variables are:

* `DOCKER_UID` - The UID of the docker user

* `DOCKER_GID` - The GID of the docker user

* `XDG_DATA_HOME` - The data directory which will be mounted to the docker containers

If you don't specify these variables, the UID and GID will use the current user's values.

A good choice for `XDG_DATA_HOME` is to use the `~erigon/.ethereum` directory created by helper targets `make user_linux` or `make user_macos`.

### Check: Permissions

Make sure that the `XDG_DATA_HOME` directory (either specified or default) is writable by the `DOCKER_UID` and `DOCKER_GID` in Docker. If you encounter permission issues during the build or service startup, check that the directories, UID, and GID controlled by these environment are correct.

### Running the Docker containers

Next command starts: Erigon on port 30303, rpcdaemon on port 8545, prometheus on port 9090, and grafana on port 3000:

```yaml
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



