# Upgrading from a previous version

Updating to the latest version of Erigon gives you access to the latest features and ensures optimal performance and stability.

## General Recommendations Before Upgrade

- **Read Release Notes**: Carefully review the [Release Notes](https://github.com/erigontech/erigon/releases) for breaking changes and new features relevant to your setup.
- **Terminate your Erigon**: End your current Erigon session by pressing `CTRL+C`.
- **Backup**: Always back up your `datadir` before performing major upgrades.  

## Snapshots Format

As of Erigon 3.1 Pebble Paws, the snapshot format has been updated. When upgrading from version 3.0.x, you need to manually perform the following steps:

1. Backup your datadir.
2. [Upgrade your Erigon installation](#upgrading-your-erigon-installation) whether from a binary, compiled source code, or Docker.
3. Upgrade snapshot files:
    1. Navigate to the Erigon directory in your terminal
    2. Reset your datadir so that Erigon will change old data by running command `./build/bin/erigon snapshots reset --datadir /your/datadir`.
4. Run Erigon, it will reuse existing data and sync only to newer snapshots.

> If you skip these steps, you may need to re-sync from scratch.

## Upgrading your Erigon Installation

Follow the below instructions depending on your installation method:

- [Pre-built binaries](#pre-built-binaries)
- [Docker](#docker)
- [Compiled source code](#compiled-from-source)

## Pre-built Binaries

Download the latest binary file from <https://github.com/erigontech/erigon/releases>, do the [checksum](../installation/prebuilt.md#checksums) and reinstall it, no other operation needed.

## Docker

If you're using Docker to run Erigon, the process to upgrade to a newer version of the software is straightforward and revolves around pulling the latest Docker image and then running it. Here's how you can upgrade Erigon using Docker:

* **Pull the Latest Docker Image**: First, find out the tag of the new release from the [Erigon Docker Hub](https://hub.docker.com/r/erigontech/erigon). Once you know the tag, pull the new image:

    ```bash
    docker pull erigontech/erigon:<new_version_tag>
    ```

    Replace `<new_version_tag>` with the actual version tag you wish to use. For example:
    
    ```bash
    docker pull erigontech/erigon:v3.0.0-beta2
    ```


* **List Your Docker Images**: Check your downloaded images to confirm the new image is there and get the new image ID:

    ```bash
    docker images
    ```


* **Stop the Running Erigon Container**: If you have a currently running Erigon container, you'll need to stop it before you can start the new version. First, find the container ID by listing the running containers:

    ```bash
    docker ps
    ```


    Then stop the container using:

    ```bash
    docker stop <container_id>
    ```

    Replace `<container_id>` with the actual ID of the container running Erigon.

* **Remove the Old Container**: (Optional) If you want to clean up, you can remove the old container after stopping it:

    ```bash
    docker rm <container_id>
    ```

* **Run the New Image**: Now you can start a new container with the new Erigon version using the new image ID:

    ```bash
    docker run -it <new_image_id>
    ```

* **Verify Operation**: Ensure that Erigon starts correctly and connects to the desired network, verifying the logs for any initial errors.

By following these steps, you'll keep your Docker setup clean and up-to-date with the latest Erigon version without needing to manually clean up or reconfigure your environment.

## Compiled from source

To upgrade Erigon to a newer version when you've originally installed it via Git and manual compilation, you should follow these steps without needing to delete the entire folder:

* **Navigate to your Erigon directory**

* **Fetch the latest changes from the repository**: You need to make sure your local repository is up-to-date with the main GitHub repository. Run:

    ```bash
    git fetch --tags
    ```

* **Check out** the [latest version](https://github.com/erigontech/erigon/releases) and switch to it using:


    ```bash
    git checkout <new_version_tag>
    ```

    Replace `<new_version_tag>` with the version tag of the new release, for example:

    ```bash
    git checkout v3.1.0
    ```

* **Rebuild Erigon**: Since the codebase has changed, you need to compile the new version. Run:

    ```bash
    make erigon
    ```
   
This process updates your installation to the latest version you specify, while maintaining your existing data. You're essentially just replacing the executable with a newer version.