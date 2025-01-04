# TxPool
*Memory pool management*

In Erigon, `txpool` is a specific API namespace that keeps pending and queued transactions in the local memory pool. It is used to store transactions that are waiting to be processed by miners. Default is `4096` pending and `1024` queued transactions. However, the number of pending transactions can be much higher than this default value.

The transaction pool (txpool or mempool) is the dynamic in-memory area where pending transactions reside before they are included in a block and thus become static. Each node on the Ethereum mainnet has its own pool of transactions and, combined, they all form the global pool. 

The thousands of pending transactions that enter the global pool by being broadcast on the network and before being included in a block are an always changing data set that’s holding millions of dollars at any given second. There are many ways to use txpool such as yield farming, liquidity providing, arbitrage, front running and MEV .

Erigon has a separate executable that allow to run TxPool as a separate process.
Running with TX pool as a separate process

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

## Command line options

To display available options for sentry digit:

```bash
./build/bin/txpool --help
```

The `--help` flag listing is reproduced below for your convenience.

```bash
Launch external Transaction Pool instance - same as built-into Erigon, but as independent Process

Usage:
  txpool [flags]

Flags:
--datadir string                  Data directory for the databases (default "/home/admin/.local/share/erigon")
-h, --help                            help for txpool
--log.console.json                Format console logs with JSON
--log.console.verbosity string    Set the log level for console logs (default "info")
--log.dir.json                    Format file logs with JSON
--log.dir.path string             Path to store user and error logs to disk
      --log.dir.prefix string           The file name prefix for logs stored to disk
      --log.dir.verbosity string        Set the log verbosity for logs stored to disk (default "info")
      --log.json                        Format console logs with JSON
      --metrics                         Enable metrics collection and reporting
      --metrics.addr string             Enable stand-alone metrics HTTP server listening interface (default "127.0.0.1")
      --metrics.port int                Metrics HTTP server listening port (default 6060)
      --pprof                           Enable the pprof HTTP server
      --pprof.addr string               pprof HTTP server listening interface (default "127.0.0.1")
      --pprof.cpuprofile string         Write CPU profile to the given file
      --pprof.port int                  pprof HTTP server listening port (default 6060)
      --private.api.addr string         execution service <host>:<port> (default "localhost:9090")
      --sentry.api.addr strings         comma separated sentry addresses '<host>:<port>,<host>:<port>' (default [localhost:9091])
      --tls.cacert string               CA certificate for client side TLS handshake
      --tls.cert string                 certificate for client side TLS handshake
      --tls.key string                  key file for client side TLS handshake
      --trace string                    Write execution trace to the given file
      --txpool.accountslots uint        Minimum number of executable transaction slots guaranteed per account (default 16)
      --txpool.api.addr string          txpool service <host>:<port> (default "localhost:9094")
      --txpool.commit.every duration    How often transactions should be committed to the storage (default 15s)
      --txpool.globalbasefeeslots int   Maximum number of non-executable transactions where only not enough baseFee (default 10000)
      --txpool.globalqueue int          Maximum number of non-executable transaction slots for all accounts (default 10000)
      --txpool.globalslots int          Maximum number of executable transaction slots for all accounts (default 10000)
      --txpool.pricebump uint           Price bump percentage to replace an already existing transaction (default 10)
      --txpool.pricelimit uint          Minimum gas price (fee cap) limit to enforce for acceptance into the pool (default 1)
      --txpool.trace.senders strings    Comma separared list of addresses, whose transactions will traced in transaction pool with debug printing
      --verbosity string                Set the log level for console logs (default "info")
```
