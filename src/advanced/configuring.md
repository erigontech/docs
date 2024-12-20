# Configuring Erigon

The Erigon 3 CLI has a wide range of flags that can be used to customize its behavior. Here's a breakdown of some of the flags, see [Options](/advanced/options.md) for the full list:

## Data Storage

* `--datadir`: Set the data directory for the databases (default: `/home/usr/.local/share/erigon`)
* `--ethash.dagdir`: Set the directory to store the ethash mining DAGs (default: `/home/usr/.local/share/erigon-ethash`)
* `--database.verbosity` Enabling internal db logs. Very high verbosity levels may require recompile db. Default: 2, means warning. (default: `2`)

## Logging

* `--log.json`: Format console logs with JSON (default: `false`)
* `--log.console.json`: Format console logs with JSON (default: `false`)
* `--log.dir.json`: Format file logs with JSON (default: `false`)
* `--verbosity`: Set the log level for console logs (default: `info`)
* `--log.console.verbosity`: Set the log level for console logs (default: `info`)
* `--log.dir.disable`: Disable disk logging (default: `false`)
* `--log.dir.path`: Set the path to store user and error logs to disk
* `--log.dir.prefix`: Set the file name prefix for logs stored to disk
* `--log.dir.verbosity`: Set the log verbosity for logs stored to disk (default: `info`)
* `--log.delays`: Enable block delay logging (default: `false`)

## Pruning Presets

* `--prune.mode`: Choose a pruning preset: `archive`, `full`, or `minimal` (default: `full`) see also [Type of node](/basic/node.md)
* `--prune.distance`: Keep state history for the latest N blocks (default: everything) (default: `0`)
* `--prune.distance.blocks`: Keep block history for the latest N blocks (default: everything) (default: `0`)

## Performance Optimization

* `--batchSize`: Set the batch size for the execution stage (default: `512M`)
* `--bodies.cache`: Limit the cache for block bodies (default: `268435456`)
* `--private.api.addr`: Set the internal grpc API address (default: `127.0.0.1:9090`)
* `--private.api.ratelimit`: Set the amount of requests the server can handle simultaneously (default: `31872`)

## Txpool

* `--txpool.api.addr`: Set the txPool api network address (default: use value of `--private.api.addr`)
* `--txpool.disable` Experimental external pool and block producer, see `./cmd/txpool/readme.md` for more info. Disabling internal txpool and block producer. (default: `false`)
* `--txpool.pricebump` Price bump percentage to replace an already existing transaction (default: `10`)
* `--txpool.pricelimit` Minimum gas price (fee cap) limit to enforce for acceptance into the pool (default: `1`)
* `--txpool.locals`: Comma separated accounts to treat as locals (no flush, priority inclusion)
* `--txpool.nolocals`: Disables price exemptions for locally submitted transactions (default: `false`)
* `--txpool.accountslots`: Set the minimum number of executable transaction slots guaranteed per account (default: `16`)
* `--txpool.blobslots`: Set the max allowed total number of blobs (within type-3 txs) per account (default: `48`)
* `--txpool.blobpricebump`: Price bump percentage to replace existing (type-3) blob transaction (default: `100`)
* `--txpool.totalblobpoollimit`: Set the total limit of number of all blobs in txs within the txpool (default: `480`)
* `--txpool.globalslots`: Set the maximum number of executable transaction slots for all accounts (default: `10000`)
* `--txpool.globalbasefeeslots`: Set the maximum number of non-executable transactions where only not enough baseFee (default: `30000`)
* `--txpool.accountqueue`: Set the maximum number of non-executable transaction slots permitted per account (default: `64`)
* `--txpool.globalqueue`: Set the maximum number of non-executable transaction slots for all accounts (default: `30000`)
* `--txpool.lifetime`: Set the maximum amount of time non-executable transaction are queued (default: `3h0m0s`)
* `--txpool.trace.senders`: Set the comma-separated list of addresses, whose transactions will traced in transaction pool with debug printing
* `--txpool.commit.every`: Set the how often transactions should be committed to the storage (default: `15s`)

 ## Remote Procedure Call (RPC)

* `--rpc.accessList`: Specify granular (method-by-method) API allowlist
* `--rpc.allow-unprotected-txs`: Allow for unprotected (non-EIP155 signed) transactions to be submitted via RPC (default: `false`)
* `--rpc.batch.concurrency`: Limit the amount of goroutines to process 1 batch request (default: `2`)
* `--rpc.streaming.disable`: Disable json streaming for some heavy endpoints
* `--rpc.accessList`: Specify granular (method-by-method) API allowlist
* `--rpc.gascap`: Set a cap on gas that can be used in eth_call/estimateGas (default: `50000000`)
* `--rpc.batch.limit`: Set the maximum number of requests in a batch (default: `100`)
* `--rpc.returndata.limit`: Set the maximum number of bytes returned from eth_call or similar invocations (default: `100000`)
* `--rpc.allow-unprotected-txs`: Allow for unprotected (non-EIP155 signed) transactions to be submitted via RPC (default: `false`)
* `--rpc.maxgetproofrewindblockcount.limit`: Set the max GetProof rewind block count (default: `100000`)
* `--rpc.txfeecap`: Set a cap on transaction fee (in ether) that can be sent via the RPC APIs (`0` = no cap) (default: `1`)

## Network and Peers

* `--chain`: Set the name of the network to join (default: `mainnet`)
* `--dev.period`: Set the block period to use in developer mode (0 = mine only if transaction pending) (default: `0`)
* `--maxpeers`: Set the maximum number of network peers (network disabled if set to 0) (default: `100`)
* `--nodiscover`: Disable the peer discovery mechanism (manual peer addition) (default: `false`)
* `--netrestrict`: Restrict network communication to the given IP networks (CIDR masks)
* `--trustedpeers`: Set the comma-separated enode URLs which are always allowed to connect, even above the peer limit

## Miscellaneous

* `--externalcl`: Enables the external consensus layer (default: `false`)
* `--override.prague`: Manually specify the Prague fork time, overriding the bundled setting (default: `0`)
* `--pprof`: Enable the pprof HTTP server (default: `false`)
* `--metrics`: Enable metrics collection and reporting (default: `false`)
* `--diagnostics`: Disable diagnostics (default: `false`)
* `--config`: Set erigon flags from YAML/TOML file
* `--help`: Show help
* `--version`: Print the version