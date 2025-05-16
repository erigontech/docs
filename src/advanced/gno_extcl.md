# Gnosis Chain with an external CL

Alternatively you can also run a Ethereum node as a Execution Layer (EL) with an external Consensus Layer (CL). Here is an example of configuration with Lighthouse.

1. Start Erigon:

    ```bash
    ./build/bin/erigon --chain=gnosis --externalcl 
    ```

    If your Consensus Layer (CL) client is on a different device, add the following flags:
    - `--authrpc.addr 0.0.0.0`, since the Engine API listens on localhost by default;
    - `--authrpc.vhosts <CL_host>` where <CL_host> is the source host or the appropriate hostname that your CL client is using.

2. Install Lighthouse, following instructions at <https://lighthouse-book.sigmaprime.io/installation.html>

3. Because Erigon needs a target head in order to sync, Lighthouse must be synced before Erigon may synchronize. The fastest way to synchronize Lighthouse is to use one of the many public checkpoint synchronization endpoints:
    - `https://checkpoint.gnosischain.com` for Gnosis Chain
    - `https://checkpoint.chiadochain.net` for Chiado Testnet


4. To communicate with Erigon, the **execution endpoint** must be specified as <erigon address>:8551, where <erigon address> is either `//localhost` or the IP address of the device running Erigon.

5. Lighthouse must point to the [JWT secret](/advanced/jwt.md) automatically created by Erigon in the `--datadir` director. In the following example the default data directory is used.

Below is an example of Lighthouse running **Gnosis Chain**:

    lighthouse \
    --network gnosis beacon_node \
    --datadir=data \
    --http \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/user/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url "https://checkpoint.gnosischain.com"

And an example of Lighthouse running Chiado testnet:

    lighthouse \
    --network chiado \
    --datadir=data \
    --http \
    --execution-endpoint http://localhost:8551 \
    --execution-jwt /home/user/.local/share/erigon/jwt.hex \
    --checkpoint-sync-url "https://checkpoint.chiadochain.net"
