# Ethereum

Follow the [hardware](/getting-started/hw-requirements.md) and [software](/getting-started/sw-requirements.md) prerequisites.

Check which [type of node](/basic/node.md) you might want torun and the [disk space](/basic/disk-space.md) needed.

<div class="warning">

**Information**

**Do not use HDD**: Hard Disk Drives (HDD) are not recommended for running Erigon, as it may cause the node to stay N blocks behind the chain tip and lead to performance issues.

**Use SSD or NVMe**: Solid State Drives (SSD) or Non-Volatile Memory Express (NVMe) drives are recommended for optimal performance. These storage devices provide faster read/write speeds and can handle the demanding requirements of an Erigon node.
</div>

## Install Erigon​

For MacOS and Linux, run the following commands to build from source the latest Erigon version:

```bash
git clone --branch v3.0.0-alpha5 --single-branch https://github.com/erigontech/erigon.git
cd erigon
make erigon
```

This should create the binary at ./build/bin/erigon

<div class="warning">

**Information**

If you are using [Windows](/installation/windows.md) follow the dedicated installation guide or use [Docker](/installation/docker.md).

</div>


## Start Erigon​

If you want to be able to send transactions with your wallet and access the Ethereum network directly, contribute to the network decentralization it is advised to run Erigon with [Caplin](/advanced/caplin.md), the internal Consensus Layer (CL).

Alternatively you can also run Prysm, Lighthouse or any other Consensus Layer client alongside with Erigon by adding the `--externalcl` flag. This will also allow you to access the Ethereum blockchain directly and give you the possibility to stake your ETH and do block production.

### Erigon with Caplin

The basic command to run Erigon with Caplin on Ethereum mainnet is:

```bash
./build/bin/erigon
```

### Erigon with Prysm as the external consensus layer

1. Start Erigon with the `--externalcl` flag:

    ```bash
    ./build/bin/erigon --externalcl
    ```

2. Install and run **Prysm** by following the official guide: <https://docs.prylabs.network/docs/install/install-with-script>.

    Prysm must fully synchronize before Erigon can start syncing, since Erigon requires an existing target head to sync to. The quickest way to get Prysm synced is to use a public checkpoint synchronization endpoint from the list at <https://eth-clients.github.io/checkpoint-sync-endpoints>.

3. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

4. Prysm must point to the **[JWT secret](/advanced/jwt.md)** automatically created by Erigon in the datadir directory. In the following example the default data directory is used.

    ```bash
    ./prysm.sh beacon-chain --execution-endpoint=http://localhost:8551 --mainnet --jwt-secret=/home/admin/.local/share/erigon/jwt.hex --checkpoint-sync-url=https://beaconstate.info --genesis-beacon-api-url=https://beaconstate.info
    ```

    If your Prysm is on a different device, add `--authrpc.addr 0.0.0.0` (Engine API listens on localhost by default) as well as `--authrpc.vhosts <CL host>` to your Prysm configuration.

### Erigon with Lighthouse

1. Start Erigon:

    ```bash
    ./build/bin/erigon --externalcl
    ```

2. Install and run Lighthouse by following the official guide: <https://lighthouse-book.sigmaprime.io/installation.html>

3. Because Erigon needs a target head in order to sync, Lighthouse must be synced before Erigon may synchronize. The fastest way to synchronize Lighthouse is to use one of the many public checkpoint synchronization endpoints at <https://eth-clients.github.io/checkpoint-sync-endpoints>.

4. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

5. Lighthouse must point to the **[JWT secret](/advanced/jwt.md)** automatically created by Erigon in the datadir director. In the following example the default data directory is used.

    ```bash
    lighthouse bn \
    --network mainnet \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/admin/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url https://mainnet.checkpoint.sigp.io \
    ```


## Basic Configuration​

- If you want to store Erigon files in a non-default location, add flag `--datadir=<your_data_dir>`. Default data directory is `/home/admin/.local/share/`.erigon.
- Erigon is archive node by default, use `--prune.mode=full` to run a full node (latest 90'000 blocks) or `--prune.mode=minimal` (EIP-4444). If you want to change [type of node](/basic/node.md) delete the `--datadir` folder content and restart Erigon with the appropriate flags.
- Default chain is `--chain=mainnet` for Ethereum mainnnet. Add the flag `--chain=holesky` for Holesky testnet, `--chain=sepolia` for Sepolia testnet. Goerli chain is no longer supported.
- `--http.addr="0.0.0.0" --http.api=eth,web3,net,debug,trace,txpool` to use RPC and e.g. be able to connect your [wallet](/basic/wallet.md).
- To increase download speed add `--torrent.download.rate=512mb` (default is 16mb)
- To stop the Erigon node you can use the `CTRL+C` command.

Additional flags can be added to [configure](/advanced/configuring.md) Erigon with several options.