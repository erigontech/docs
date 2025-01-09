# How to run a Polygon node

Follow the [hardware](/getting-started/hw-requirements.md) and [software](/getting-started/sw-requirements.md) prerequisites.

Check which [type of node](/basic/node.md) you might want to run and the [disk space](/basic/disk-space.md) required.

<div class="warning">

**Information**

**Do not use HDD**: Hard Disk Drives (HDD) are not recommended for running Erigon, as it may cause the node to stay N blocks behind the chain tip and lead to performance issues.

**Use SSD or NVMe**: Solid State Drives (SSD) or Non-Volatile Memory Express (NVMe) drives are recommended for optimal performance. These storage devices provide faster read/write speeds and can handle the demanding requirements of an Erigon node.
</div>

## Install Erigon​

For MacOS and Linux, run the following commands to build from source the latest Erigon version:

```bash
git clone --branch v3.0.0-alpha6 --single-branch https://github.com/erigontech/erigon.git
cd erigon
make erigon
```

This should create the binary at ./build/bin/erigon

<div class="warning">

**Information**

If you are using [Windows](/installation/windows.md) follow the dedicated installation guide or use [Docker](/installation/docker.md).

</div>

# Start Erigon

To start a Erigon full node for **Polygon mainnet** with remote Heimdall:

```bash
./build/bin/erigon --chain=bor-mainnet --bor.heimdall=https://heimdall-api.polygon.technology
```

For a **Amoy testnet** archive node with remote Heimdall:

```bash
./build/bin/erigon --chain=amoy --bor.heimdall=https://heimdall-api-amoy.polygon.technology
```

## Basic Configuration​

- If you want to store Erigon files in a non-default location, add flag `--datadir=<your_data_dir>`. Default data directory is `/home/usr/.local/share/`.erigon.
- Erigon is full node by default, use `--prune.mode=archive` to run a archive node or `--prune.mode=minimal` (EIP-4444). If you want to change [type of node](/basic/node.md) delete the `--datadir` folder content and restart Erigon with the appropriate flags.
- `--http.addr="0.0.0.0" --http.api=eth,web3,net,debug,trace,txpool` to use RPC and e.g. be able to connect your [wallet](/basic/wallet.md).
- To increase download speed add `--torrent.download.rate=512mb` (default is 16mb)
- To stop the Erigon node you can use the `CTRL+C` command.

Additional flags can be added to [configure](/advanced/configuring.md) Erigon with several options.
