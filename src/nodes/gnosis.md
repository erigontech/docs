# Gnosis Chain

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
git clone --branch v3.0.0-alpha6 --single-branch https://github.com/erigontech/erigon.git
cd erigon
make erigon
```

This should create the binary at ./build/bin/erigon

<div class="warning">

**Information**

If you are using [Windows](/installation/windows.md) follow the dedicated installation guide or use [Docker](/installation/docker.md).

</div>


## Start Erigon​

If you want to be able to send transactions with your wallet and access the Gnosis Chain network directly, contribute to the network decentralization it is advised to run Erigon with [Caplin](/advanced/caplin.md), the internal Consensus Layer (CL).

Alternatively you can also run Prysm, Lighthouse or any other Consensus Layer client alongside with Erigon by adding the `--externalcl` flag. This will also allow you to access the Ethereum blockchain directly and give you the possibility to stake your ETH and do block production.

### Erigon with Caplin

The basic command to run Erigon with Caplin on Gnosis Chain is:

```bash
./build/bin/erigon --chain=gnosis
```

### Erigon with Lighthouse

1. Start Erigon:

    ```bash
    ./build/bin/erigon --externalcl
    ```

2. Install Lighthouse, another popular client that can be used with Erigon for block building. Follow the instructions until the chapter **Build Lighthouse**, skipping the `make` instruction.: <https://lighthouse-book.sigmaprime.io/installation.html>

3. Now compile Lighthouse in order to run Gnosis Chain using the feature flags :

    ```bash
    cd lighthouse
    env FEATURES=gnosis make
    ```

4. Because Erigon needs a target head in order to sync, Lighthouse must be synced before Erigon may synchronize. The fastest way to synchronize Lighthouse is to use one of the many public checkpoint synchronization endpoints:
    - `https://checkpoint.gnosischain.com` for Gnosis Chain
    - `https://checkpoint.chiadochain.net` for Chiado Testnet


5. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

6. Lighthouse must point to the **[JWT secret](/advanced/jwt.md)** automatically created by Erigon in the datadir director. In the following example the default data directory is used.

Below is an example of Lighthouse running **Gnosis Chain**:

    ```bash
    lighthouse \
    --network gnosis beacon_node \
    --datadir=data \
    --http \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/admin/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url "https://checkpoint.gnosischain.com"
    ```

And an example of Lighthouse running Chiado testnet:

    ```bash
    lighthouse \
    --network chiado \
    --datadir=data \
    --http \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/admin/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url "https://checkpoint.chiadochain.net"
    ```

## Basic Configuration​

- If you want to store Erigon files in a non-default location, add flag `--datadir=<your_data_dir>`. Default data directory is `/home/admin/.local/share/`.erigon.
- Erigon is full node by default, use `--prune.mode=archive` to run a archive node or `--prune.mode=minimal` (EIP-4444). If you want to change [type of node](/basic/node.md) delete the `--datadir` folder content and restart Erigon with the appropriate flags.
- Add the flag `--chain=chiado` for Chiado testnet.
- `--http.addr="0.0.0.0" --http.api=eth,web3,net,debug,trace,txpool` to use RPC and e.g. be able to connect your [wallet](/basic/wallet.md).
- To increase download speed add `--torrent.download.rate=512mb` (default is 16mb)
- To stop the Erigon node you can use the `CTRL+C` command.

Additional flags can be added to [configure](/advanced/configuring.md) Erigon with several options.