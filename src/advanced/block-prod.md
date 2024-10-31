# Block production

How to propose and validate blockswith Erigon

Only remote miners are supported.

To enable, add the flags:

```bash
--mine --miner.etherbase=...
```
or

```bash
--mine --miner.miner.sigkey=...
```

Other supported options: `--miner.extradata`, `--miner.notify`, `--miner.gaslimit`, `--miner.gasprice` , `--miner.gastarget`

JSON-RPC supports methods: `eth_coinbase` , `eth_hashrate`, `eth_mining`, `eth_getWork`, `eth_submitWork`, `eth_submitHashrate`

JSON-RPC supports websocket methods: `newPendingTransaction`

# Using Caplin as validator

<div class="warning">

**Information**

Only Lighthouse, Lodestar and Teku are supported as Validator Clients.

</div>

To enable block production and Caplin's beacon API when using Caplin as the Consensus Layer (CL) engine, the flag `--beacon.api` must be added. For example:

```bash
--beacon.api=beacon,builder,config,debug,node,validator,lighthouse
```
<div class="warning">

**Information**

Enabling the Beacon API will lead to a 6 GB higher RAM usage.
</div>


For example, if you want to run Erigon and Caplin as a validator here is an example of configuration:

```bash
./build/bin/erigon --chain=holesky --prune.mode=full --beacon.api=beacon,builder,config,debug,node,validator,lighthouse
```

While here the command for Lighthouse* would look like:

```bash
lighthouse validator_client --network holesky --beacon-nodes http://localhost:5555
```

**For adding validators and specific command syntax, refer to the documentation of your chosen Validator Client.*