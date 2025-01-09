# Lighthouse

Lighthouse is another popular client that combined with Erigon can be used for block building. The necessary steps to run Erigon with Lightouse are listed here following:

1. Start Erigon with the flag `--externalcl` to allow a external Consesus Layer: 

    ```bash
    ./build/bin/erigon --externalcl
    ```

2. Install Lighthouse by following the [official instructions](https://lighthouse-book.sigmaprime.io).

3. Lighthouse must fully synchronize before Erigon can start syncing, since Erigon requires an existing target head to sync to. The quickest way to get Lighthouse synced is to use a public checkpoint synchronization endpoint from the list at <https://eth-clients.github.io/checkpoint-sync-endpoints>.

    In order to communicate with Erigon the execution endpoint `<erigon address>:8551` must be specified, where `<erigon address>` is either `//localhost` or the IP address of the device running Erigon. 

    Lighthouse must point to the [JWT secret](/advanced/jwt.md) automatically created by Erigon in the datadir directory (in the below example the default data directory is used).

    ```bash
    lighthouse bn \
    --network mainnet \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/usr/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url https://mainnet.checkpoint.sigp.io \
    ```

    If your Lighthouse is on a different device, add `--authrpc.addr 0.0.0.0` (Engine API listens on localhost by default) as well as `--authrpc.vhosts <CL host>`.






