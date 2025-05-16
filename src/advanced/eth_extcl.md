# Ethereum with an external CL

Alternatively you can also run a Ethereum node with an external Consensus Layer (CL) 

Both [Prysm](#erigon-with-prysm-as-the-external-consensus-layer), [Lighthouse](#erigon-with-lighthouse-as-the-external-consensus-layer) or any other Consensus Layer client alongside with Erigon by adding the `--externalcl` flag. This will also allow you to access the Ethereum blockchain directly and give you the possibility to manage your keys to stake your ETH and do block production.


## Erigon with Prysm as the external CL

1. Start Erigon with the `--externalcl` flag:

    ```bash
    erigon --externalcl
    ```
    If your Consensus Layer (CL) client is on a different device, add the following flags:
    - `--authrpc.addr 0.0.0.0`, since the Engine API listens on localhost by default;
    - `--authrpc.vhosts <CL_host>` where <CL_host> is the source host or the appropriate hostname that your CL client is using.

2. Install and run **Prysm** by following the official guide: <https://docs.prylabs.network/docs/install/install-with-script>.

    Prysm must fully synchronize before Erigon can start syncing, since Erigon requires an existing target head to sync to. The quickest way to get Prysm synced is to use a public checkpoint synchronization endpoint from the list at <https://eth-clients.github.io/checkpoint-sync-endpoints>.

3. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

4. Prysm must point to the **[JWT secret](/advanced/jwt.md)** automatically created by Erigon in the datadir directory. In the following example the default data directory is used.

    ```bash
    ./prysm.sh beacon-chain \
    --execution-endpoint=http://localhost:8551 \
    --mainnet --jwt-secret=/home/usr/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url=https://beaconstate.info \
    --genesis-beacon-api-url=https://beaconstate.info
    ```


## Erigon with Lighthouse as the external CL

1. Start Erigon:

    ```bash
    ./build/bin/erigon --externalcl
    ```

2. Install and run Lighthouse by following the official guide: <https://lighthouse-book.sigmaprime.io/installation.html>

3. Because Erigon needs a target head in order to sync, Lighthouse must be synced before Erigon may synchronize. The fastest way to synchronize Lighthouse is to use one of the many public checkpoint synchronization endpoints at <https://eth-clients.github.io/checkpoint-sync-endpoints>.

4. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

5. Lighthouse must point to the [JWT secret](/advanced/jwt.md) automatically created by Erigon in the `--datadir` director. In the following example the default data directory is used.

    ```bash
    lighthouse bn \
    --network mainnet \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/user/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url https://mainnet.checkpoint.sigp.io \
    ```

