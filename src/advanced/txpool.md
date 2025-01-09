# TxPool
*Memory pool management*

In Erigon, `txpool` is a specific API namespace that keeps pending and queued transactions in the local memory pool. It is used to store transactions that are waiting to be processed by miners. Default is `4096` pending and `1024` queued transactions. However, the number of pending transactions can be much higher than this default value.

The transaction pool (txpool or mempool) is the dynamic in-memory area where pending transactions reside before they are included in a block and thus become static. Each node on the Ethereum mainnet has its own pool of transactions and, combined, they all form the global pool. 

The thousands of pending transactions that enter the global pool by being broadcast on the network and before being included in a block are an always changing data set that’s holding millions of dollars at any given second. There are many ways to use txpool such as yield farming, liquidity providing, arbitrage, front running and MEV .

WHile Txpool component is run by default as an internal Erigon component,  it can also be run as a separate process.

## Running with TX pool as a separate process

Before using a separate TxPool process the executable must be built:

```bash
cd erigon
make txpool
```

If Erigon is on a different device, add the flag `--pprof.addr 0.0.0.0` or TxPool will listen on localhost by default.

```bash
./build/bin/txpool --pprof.addr 0.0.0.0
```

Erigon must be launched with options to listen to external TxPool

```bash
./build/bin/erigon --pprof --pprof.addr 123.123.123.123
```

## More info

For other information regardin Txpool functionality, configuration, and usage, please refer to the embedded file you can find in your compiled Erigon folder at `./cmd/txpool/README.md`.

## Command Line Options

To display available options for Txpool digit:

```bash
./build/bin/txpool --help
```

The `--help` flag listing is reproduced below for your convenience.

```
Launch external Transaction Pool instance - same as built-into Erigon, but as independent Process

Usage:
  txpool [flags]

Flags:
      --datadir string                     Data directory for the databases (default "/home/bloxster/.local/share/erigon")
      --db.writemap                        Enable WRITE_MAP feature for fast database writes and fast commit times (default true)
      --diagnostics.disabled               Disable diagnostics
      --diagnostics.endpoint.addr string   Diagnostics HTTP server listening interface (default "127.0.0.1")
      --diagnostics.endpoint.port uint     Diagnostics HTTP server listening port (default 6062)
      --diagnostics.speedtest              Enable speed test
  -h, --help                               help for txpool
      --log.console.json                   Format console logs with JSON
      --log.console.verbosity string       Set the log level for console logs (default "info")
      --log.delays                         Enable block delay logging
      --log.dir.disable                    disable disk logging
      --log.dir.json                       Format file logs with JSON
      --log.dir.path string                Path to store user and error logs to disk
      --log.dir.prefix string              The file name prefix for logs stored to disk
      --log.dir.verbosity string           Set the log verbosity for logs stored to disk (default "info")
      --log.json                           Format console logs with JSON
      --metrics                            Enable metrics collection and reporting
      --metrics.addr string                Enable stand-alone metrics HTTP server listening interface (default "127.0.0.1")
      --metrics.port int                   Metrics HTTP server listening port (default 6061)
      --pprof                              Enable the pprof HTTP server
      --pprof.addr string                  pprof HTTP server listening interface (default "127.0.0.1")
      --pprof.cpuprofile string            Write CPU profile to the given file
      --pprof.port int                     pprof HTTP server listening port (default 6060)
      --private.api.addr string            execution service <host>:<port> (default "localhost:9090")
      --sentry.api.addr strings            comma separated sentry addresses '<host>:<port>,<host>:<port>' (default [localhost:9091])
      --tls.cacert string                  CA certificate for client side TLS handshake
      --tls.cert string                    certificate for client side TLS handshake
      --tls.key string                     key file for client side TLS handshake
      --trace string                       Write execution trace to the given file
      --txpool.accountslots uint           Minimum number of executable transaction slots guaranteed per account (default 16)
      --txpool.api.addr string             txpool service <host>:<port> (default "localhost:9094")
      --txpool.blobpricebump uint          Price bump percentage to replace an existing blob (type-3) transaction (default 100)
      --txpool.blobslots uint              Max allowed total number of blobs (within type-3 txs) per account (default 48)
      --txpool.commit.every duration       How often transactions should be committed to the storage (default 15s)
      --txpool.globalbasefeeslots int      Maximum number of non-executable transactions where only not enough baseFee (default 30000)
      --txpool.globalqueue int             Maximum number of non-executable transaction slots for all accounts (default 30000)
      --txpool.globalslots int             Maximum number of executable transaction slots for all accounts (default 10000)
      --txpool.gossip.disable              Disabling p2p gossip of txs. Any txs received by p2p - will be dropped. Some networks like 'Optimism execution engine'/'Optimistic Rollup' - using it to protect against MEV attacks
      --txpool.pricebump uint              Price bump percentage to replace an already existing transaction (default 10)
      --txpool.pricelimit uint             Minimum gas price (fee cap) limit to enforce for acceptance into the pool (default 1)
      --txpool.totalblobpoollimit uint     Total limit of number of all blobs in txs within the txpool (default 480)
      --txpool.trace.senders strings       Comma separated list of addresses, whose transactions will traced in transaction pool with debug printing
      --verbosity string                   Set the log level for console logs (default "info")
```