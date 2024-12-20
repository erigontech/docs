# Using Caplin as validator
*Running Erigon with Caplin as validator*

Caplin is also suitable for staking. However, it is required to pair it with a validator key manager, such as Lighthouse or Teku, since it doesn't have a native key management system.

This guide explains how to use Erigon with its embedded Caplin consensus layer and Lighthouse as the validator client for staking on Ethereum.

## 1. Start Erigon with Caplin
Run the following command to start Erigon with the embedded Caplin consensus layer with the beacon API on:

```bash
erigon \
  --datadir=/data/erigon \
  --chain=mainnet \
  --prune.mode=full \
  --http \
  --http.addr=0.0.0.0 \
  --http.port=8545 \
  --http.api=engine,eth,net,web3 \
  --ws \
  --ws.port=8546 \
  --caplin.enable-upnp \
  --caplin.discovery.addr=0.0.0.0 \
  --caplin.discovery.port=4000 \
  --caplin.discovery.tcpport=4001 \
  --chain=<NETWORK>
  --beacon.api=beacon,validator,builder,config,debug,events,node,lighthouse 
```

**Flags Explanation**:

- Execution Layer:
    - `--http.api=engine,eth,net,web3`: enables the necessary APIs for external clients and Caplin.
    - `--ws`: enables WebSocket-based communication (optional).
- Consensus Layer (Caplin):
    - `--caplin.discovery.addr` and `--caplin.discovery.port`: configures Caplin's gossip and discovery layer.
    - `--beacon.api=beacon,validator,builder,config,debug,events,node,lighthouse`: enables all possible API endpoints for the validator client.

## 2. Set Up Lighthouse Validator Client

### 2.1 Install Lighthouse

Download the latest Lighthouse binary:

```
curl -LO https://github.com/sigp/lighthouse/releases/latest/download/lighthouse
chmod +x lighthouse
sudo mv lighthouse /usr/local/bin/
```

Or, use Docker:

```bash
docker pull sigp/lighthouse:latest
```

### 2.2. Create Lighthouse Validator Key Directory

```bash
mkdir -p ~/.lighthouse/validators
```

### 2.3. Run Lighthouse Validator Client

Start the validator client and connect it to the Caplin consensus layer:
```bash
lighthouse vc \
  --network mainnet \
  --beacon-nodes http://127.0.0.1:5555 \
  --suggested-fee-recipient=<your_eth_address>
```
**Flags Explanation**:
- `--network mainnet`: Specifies the Ethereum mainnet.
- `--beacon-nodes`: Points to the Caplin beacon API at `http://127.0.0.1:5555`.
- `--suggested-fee-recipient`: Specifies your Ethereum address for block rewards.

### 2.4. Import Validator Keys

If you have existing validator keys, import them:

```bash
lighthouse account validator import --directory <path_to_validator_keys>
```

