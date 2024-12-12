# Block production

*How to propose and validate blocks with Erigon*

Both remote miners and Caplin are supported.

# Using remote miners

To enable remote miners , add the flags:

```bash
--mine --miner.etherbase=...
```
or

```bash
--mine --miner.miner.sigkey=...
```

Other supported options are:
- `--miner.notify`: Comma separated HTTP URL list to notify of new work packages
- `--miner.gaslimit`: Target gas limit for mined blocks (default: `36000000`)
- `--miner.etherbase`: Public address for block mining rewards (default: "`0`")
- `--miner.extradata`: Block extra data set by the miner (default: `client version`)
- `--miner.noverify`: Disable remote sealing verification (default: `false`)
- `--miner.noverify`: Disable remote sealing verification (default: `false`)
- `--miner.sigfile`: Private key to sign blocks with
- `--miner.recommit`: Time interval to recreate the block being mined (default: `3s`)
- `--miner.gasprice`: This option sets the minimum gas price for mined transactions
- `--miner.gastarget`: This option sets the maximum amount of gas that could be spent during a transaction.

Erigon supports [standard JSON-RPC methods](https://ethereum.org/en/developers/docs/apis/json-rpc/).

# Using Caplin as validator
*Running Erigon with Caplin and Lighthouse Validator*

Caplin is also suitable for staking, however, you will need to utilize either Lighthouse, Teku, or another validator client as your key manager, since Caplin does not offer a native key management solution.

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

