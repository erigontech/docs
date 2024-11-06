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

Other supported options: `--miner.extradata`, `--miner.notify`, `--miner.gaslimit`, `--miner.gasprice` , `--miner.gastarget`.

JSON-RPC supports methods: `eth_coinbase` , `eth_hashrate`, `eth_mining`, `eth_getWork`, `eth_submitWork`, `eth_submitHashrate`

JSON-RPC supports websocket methods: `newPendingTransaction`.

**For adding validators and specific command syntax, refer to the documentation of your chosen Validator Client.*