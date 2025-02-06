# Using an external consensus client as validator

To enable external consensus clients, add the flags:

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
