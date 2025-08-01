# Options

*All available options*

Erigon is primarily controlled using the command line, started using the `./build/bin/erigon` command and stopped by pressing `CTRL-C`.

Using the command-line options allows for configurations, and several functionalities can be called using sub commands.

The `--help` flag listing is reproduced below for your convenience.

```bash
./build/bin/erigon --help
```

## Commands

```
NAME:
   erigon - erigon

USAGE:
   erigon [command] [flags]

VERSION:
   3.0.12-39c6a6ff

COMMANDS:
   init                      Bootstrap and initialize a new genesis block
   import                    Import a blockchain file
   seg, snapshots, segments  Managing historical data segments (partitions)
   support                   Connect Erigon instance to a diagnostics system for support
   help, h                   Shows a list of commands or help for one command

GLOBAL OPTIONS:
   --datadir value                                                                  Data directory for the databases (default: /home/bloxster/.local/share/erigon)
   --ethash.dagdir value                                                            Directory to store the ethash mining DAGs (default: /home/bloxster/.local/share/erigon-ethash)
   --externalcl                                                                     Enables the external consensus layer (default: false)
   --txpool.disable                                                                 External pool and block producer, see ./cmd/txpool/readme.md for more info. Disabling internal txpool and block producer. (default: false)
   --txpool.pricelimit value                                                        Minimum gas price (fee cap) limit to enforce for acceptance into the pool (default: 1)
   --txpool.pricebump value                                                         Price bump percentage to replace an already existing transaction (default: 10)
   --txpool.blobpricebump value                                                     Price bump percentage to replace existing (type-3) blob transaction (default: 100)
   --txpool.accountslots value                                                      Minimum number of executable transaction slots guaranteed per account (default: 16)
   --txpool.blobslots value                                                         Max allowed total number of blobs (within type-3 txs) per account (default: 48)
   --txpool.totalblobpoollimit value                                                Total limit of number of all blobs in txs within the txpool (default: 480)
   --txpool.globalslots value                                                       Maximum number of executable transaction slots for all accounts (default: 10000)
   --txpool.globalbasefeeslots value                                                Maximum number of non-executable transactions where only not enough baseFee (default: 30000)
   --txpool.globalqueue value                                                       Maximum number of non-executable transaction slots for all accounts (default: 30000)
   --txpool.trace.senders value                                                     Comma separated list of addresses, whose transactions will traced in transaction pool with debug printing
   --txpool.commit.every value                                                      How often transactions should be committed to the storage (default: 15s)
   --prune.distance value                                                           Keep state history for the latest N blocks (default: everything) (default: 0)
   --prune.distance.blocks value                                                    Keep block history for the latest N blocks (default: everything) (default: 0)
   --prune.mode value                                                               Choose a pruning preset to run onto. Available values: "full", "archive", "minimal", "blocks".
                                                                                          full: Keep only necessary blocks and latest state,
                                                                                          blocks: Keep all blocks but not the state history,
                                                                                          archive: Keep the entire state history and all blocks,
                                                                                          minimal: Keep only latest state (default: "full")
   --batchSize value                                                                Batch size for the execution stage (default: "512M")
   --bodies.cache value                                                             Limit on the cache for block bodies (default: "268435456")
   --database.verbosity value                                                       Enabling internal db logs. Very high verbosity levels may require recompile db. Default: 2, means warning. (default: 2)
   --private.api.addr value                                                         Erigon's components (txpool, rpcdaemon, sentry, downloader, ...) can be deployed as independent Processes on same/another server. Then components will connect to erigon by this internal grpc API. example: 127.0.0.1:9090, empty string means not to start the listener. do not expose to public network. serves remote database interface (default: "127.0.0.1:9090")
   --private.api.ratelimit value                                                    Amount of requests server handle simultaneously - requests over this limit will wait. Increase it - if clients see 'request timeout' while server load is low - it means your 'hot data' is small or have much RAM.  (default: 31872)
   --etl.bufferSize value                                                           Buffer size for ETL operations. (default: "256MB")
   --tls                                                                            Enable TLS handshake (default: false)
   --tls.cert value                                                                 Specify certificate
   --tls.key value                                                                  Specify key file
   --tls.cacert value                                                               Specify certificate authority
   --state.stream.disable                                                           Disable streaming of state changes from core to RPC daemon (default: false)
   --sync.loop.throttle value                                                       Sets the minimum time between sync loop starts (e.g. 1h30m, default is none)
   --bad.block value                                                                Marks block with given hex string as bad and forces initial reorg before normal staged sync
   --http                                                                           JSON-RPC server (enabled by default). Use --http=false to disable it (default: true)
   --http.enabled                                                                   JSON-RPC HTTP server (enabled by default). Use --http.enabled=false to disable it (default: true)
   --graphql                                                                        Enable the graphql endpoint (default: false)
   --http.addr value                                                                HTTP-RPC server listening interface (default: "localhost")
   --http.port value                                                                HTTP-RPC server listening port (default: 8545)
   --authrpc.addr value                                                             HTTP-RPC server listening interface for the Engine API (default: "localhost")
   --authrpc.port value                                                             HTTP-RPC server listening port for the Engine API (default: 8551)
   --authrpc.jwtsecret value                                                        Path to the token that ensures safe connection between CL and EL
   --http.compression                                                               Enable compression over HTTP-RPC (default: false)
   --http.corsdomain value                                                          Comma separated list of domains from which to accept cross origin requests (browser enforced)
   --http.vhosts value                                                              Comma separated list of virtual hostnames from which to accept requests (server enforced). Accepts 'any' or '*' as wildcard. (default: "localhost")
   --authrpc.vhosts value                                                           Comma separated list of virtual hostnames from which to accept Engine API requests (server enforced). Accepts 'any' or '*' as wildcard. (default: "localhost")
   --http.api value                                                                 API's offered over the HTTP-RPC interface (default: "eth,erigon,engine")
   --ws.port value                                                                  WS-RPC server listening port (default: 8546)
   --ws                                                                             Enable the WS-RPC server (default: false)
   --ws.compression                                                                 Enable compression over WebSocket (default: false)
   --http.trace                                                                     Print all HTTP requests to logs with INFO level (default: false)
   --http.dbg.single                                                                Allow pass HTTP header 'dbg: true' to printt more detailed logs - how this request was executed (default: false)
   --state.cache value                                                              Amount of data to store in StateCache (enabled if no --datadir set). Set 0 to disable StateCache. Defaults to 0MB (default: "0MB")
   --rpc.batch.concurrency value                                                    Does limit amount of goroutines to process 1 batch request. Means 1 bach request can't overload server. 1 batch still can have unlimited amount of request (default: 2)
   --rpc.streaming.disable                                                          Erigon has enabled json streaming for some heavy endpoints (like trace_*). It's a trade-off: greatly reduce amount of RAM (in some cases from 30GB to 30mb), but it produce invalid json format if error happened in the middle of streaming (because json is not streaming-friendly format) (default: false)
   --db.read.concurrency value                                                      Does limit amount of parallel db reads. Default: equal to GOMAXPROCS (or number of CPU) (default: 1408)
   --rpc.accessList value                                                           Specify granular (method-by-method) API allowlist
   --trace.compat                                                                   Bug for bug compatibility with OE for trace_ routines (default: false)
   --rpc.gascap value                                                               Sets a cap on gas that can be used in eth_call/estimateGas (default: 50000000)
   --rpc.batch.limit value                                                          Maximum number of requests in a batch (default: 100)
   --rpc.returndata.limit value                                                     Maximum number of bytes returned from eth_call or similar invocations (default: 100000)
   --rpc.allow-unprotected-txs                                                      Allow for unprotected (non-EIP155 signed) transactions to be submitted via RPC (default: false)
   --rpc.txfeecap value                                                             Sets a cap on transaction fee (in ether) that can be sent via the RPC APIs (0 = no cap) (default: 1)
   --txpool.api.addr value                                                          TxPool api network address, for example: 127.0.0.1:9090 (default: use value of --private.api.addr)
   --trace.maxtraces value                                                          Sets a limit on traces that can be returned in trace_filter (default: 200)
   --experimental.commitment-history                                                Enables blazing fast eth_getProof for executed block (default: false)
   --http.timeouts.read value                                                       Maximum duration for reading the entire request, including the body. (default: 30s)
   --http.timeouts.write value                                                      Maximum duration before timing out writes of the response. It is reset whenever a new request's header is read. (default: 30m0s)
   --http.timeouts.idle value                                                       Maximum amount of time to wait for the next request when keep-alives are enabled. If http.timeouts.idle is zero, the value of http.timeouts.read is used. (default: 2m0s)
   --authrpc.timeouts.read value                                                    Maximum duration for reading the entire request, including the body. (default: 30s)
   --authrpc.timeouts.write value                                                   Maximum duration before timing out writes of the response. It is reset whenever a new request's header is read. (default: 30m0s)
   --authrpc.timeouts.idle value                                                    Maximum amount of time to wait for the next request when keep-alives are enabled. If authrpc.timeouts.idle is zero, the value of authrpc.timeouts.read is used. (default: 2m0s)
   --rpc.evmtimeout value                                                           Maximum amount of time to wait for the answer from EVM call. (default: 5m0s)
   --rpc.overlay.getlogstimeout value                                               Maximum amount of time to wait for the answer from the overlay_getLogs call. (default: 5m0s)
   --rpc.overlay.replayblocktimeout value                                           Maximum amount of time to wait for the answer to replay a single block when called from an overlay_getLogs call. (default: 10s)
   --rpc.subscription.filters.maxlogs value                                         Maximum number of logs to store per subscription. (default: 0)
   --rpc.subscription.filters.maxheaders value                                      Maximum number of block headers to store per subscription. (default: 0)
   --rpc.subscription.filters.maxtxs value                                          Maximum number of transactions to store per subscription. (default: 0)
   --rpc.subscription.filters.maxaddresses value                                    Maximum number of addresses per subscription to filter logs by. (default: 0)
   --rpc.subscription.filters.maxtopics value                                       Maximum number of topics per subscription to filter logs by. (default: 0)
   --snap.keepblocks                                                                Keep ancient blocks in db (useful for debug) (default: false)
   --snap.stop                                                                      Workaround to stop producing new snapshots, if you meet some snapshots-related critical bug. It will stop move historical data from DB to new immutable snapshots. DB will grow and may slightly slow-down - and removing this flag in future will not fix this effect (db size will not greatly reduce). (default: false)
   --snap.state.stop                                                                Workaround to stop producing new state files, if you meet some state-related critical bug. It will stop aggregate DB history in a state files. DB will grow and may slightly slow-down - and removing this flag in future will not fix this effect (db size will not greatly reduce). (default: false)
   --snap.skip-state-snapshot-download                                              Skip state download and start from genesis block (default: false)
   --db.pagesize value                                                              DB is splitted to 'pages' of fixed size. Can't change DB creation. Must be power of 2 and '256b <= pagesize <= 64kb'. Default: equal to OperationSystem's pageSize. Bigger pageSize causing: 1. More writes to disk during commit 2. Smaller b-tree high 3. Less fragmentation 4. Less overhead on 'free-pages list' maintainance (a bit faster Put/Commit) 5. If expecting DB-size > 8Tb then set pageSize >= 8Kb (default: "4KB")
   --db.size.limit value                                                            Runtime limit of chaindata db size (can change at any time) (default: "1TB")
   --db.writemap                                                                    Enable WRITE_MAP feature for fast database writes and fast commit times (default: true)
   --torrent.port value                                                             Port to listen and serve BitTorrent protocol (default: 42069)
   --torrent.maxpeers value                                                         Unused parameter (reserved for future use) (default: 100)
   --torrent.conns.perfile value                                                    Number of connections per file (default: 10)
   --torrent.download.slots value                                                   Amount of files to download in parallel. (default: 32)
   --torrent.staticpeers value                                                      Comma separated host:port to connect to
   --torrent.upload.rate value                                                      Bytes per second, example: 32mb (default: "4mb")
   --torrent.download.rate value                                                    Bytes per second, example: 32mb (default: "128mb")
   --torrent.verbosity value                                                        0=silent, 1=error, 2=warn, 3=info, 4=debug, 5=detail (must set --verbosity to equal or higher level and has default: 2) (default: 2)
   --port value                                                                     Network listening port (default: 30303)
   --p2p.protocol value [ --p2p.protocol value ]                                    Version of eth p2p protocol (default: 68, 67)
   --p2p.allowed-ports value [ --p2p.allowed-ports value ]                          Allowed ports to pick for different eth p2p protocol versions as follows <porta>,<portb>,..,<porti> (default: 30303, 30304, 30305, 30306, 30307)
   --nat value                                                                      NAT port mapping mechanism (any|none|upnp|pmp|stun|extip:<IP>)
                                                                                         "" or "none"         Default - do not nat
                                                                                         "extip:77.12.33.4"   Will assume the local machine is reachable on the given IP
                                                                                         "any"                Uses the first auto-detected mechanism
                                                                                         "upnp"               Uses the Universal Plug and Play protocol
                                                                                         "pmp"                Uses NAT-PMP with an auto-detected gateway address
                                                                                         "pmp:192.168.0.1"    Uses NAT-PMP with the given gateway address
                                                                                         "stun"               Uses STUN to detect an external IP using a default server
                                                                                         "stun:<server>"      Uses STUN to detect an external IP using the given server (host:port)
   --nodiscover                                                                     Disables the peer discovery mechanism (manual peer addition) (default: false)
   --v5disc                                                                         Enables the experimental RLPx V5 (Topic Discovery) mechanism (default: false)
   --netrestrict value                                                              Restricts network communication to the given IP networks (CIDR masks)
   --nodekey value                                                                  P2P node key file
   --nodekeyhex value                                                               P2P node key as hex (for testing)
   --discovery.dns value                                                            Sets DNS discovery entry points (use "" to disable DNS)
   --bootnodes value                                                                Comma separated enode URLs for P2P discovery bootstrap
   --staticpeers value                                                              Comma separated enode URLs to connect to
   --trustedpeers value                                                             Comma separated enode URLs which are always allowed to connect, even above the peer limit
   --maxpeers value                                                                 Maximum number of network peers (network disabled if set to 0) (default: 32)
   --chain value                                                                    name of the network to join (default: "mainnet")
   --dev.period value                                                               Block period to use in developer mode (0 = mine only if transaction pending) (default: 0)
   --vmdebug                                                                        Record information useful for VM and contract debugging (default: false)
   --networkid value                                                                Explicitly set network id (integer)(For testnets: use --chain <testnet_name> instead) (default: 1)
   --experiment.persist.receipts value                                              Set > 0 to store receipts in chaindata db (only on chain-tip) - RPC for recent receit/logs will be faster. Values: 1_000 good starting point. 10_000 receitps it's ~1Gb (not much IO increase). Please test before go over 100_000 (default: 0)
   --experiment.persist.receipts.v2                                                 To store receipts in chaindata db (only on chain-tip) - RPC for recent receit/logs will be faster. Values: 1_000 good starting point. 10_000 receitps it's ~1Gb (not much IO increase). Please test before go over 100_000 (default: false)
   --fakepow                                                                        Disables proof-of-work verification (default: false)
   --gpo.blocks value                                                               Number of recent blocks to check for gas prices (default: 20)
   --gpo.percentile value                                                           Suggested gas price is the given percentile of a set of recent transaction gas prices (default: 60)
   --allow-insecure-unlock                                                          Allow insecure account unlocking when account-related RPCs are exposed by http (default: false)
   --identity value                                                                 Custom node name
   --clique.checkpoint value                                                        Number of blocks after which to save the vote snapshot to the database (default: 10)
   --clique.snapshots value                                                         Number of recent vote snapshots to keep in memory (default: 1024)
   --clique.signatures value                                                        Number of recent block signatures to keep in memory (default: 16384)
   --clique.datadir value                                                           Path to clique db folder
   --mine                                                                           Enable mining (default: false)
   --proposer.disable                                                               Disables PoS proposer (default: false)
   --miner.notify value                                                             Comma separated HTTP URL list to notify of new work packages
   --miner.gaslimit value                                                           Target gas limit for mined blocks (default: 0)
   --miner.etherbase value                                                          Public address for block mining rewards (default: "0")
   --miner.gasprice value                                                           Minimum gas price for mining a transaction (default: 0)
   --miner.extradata value                                                          Block extra data set by the miner (default = client version)
   --miner.noverify                                                                 Disable remote sealing verification (default: false)
   --miner.sigfile value                                                            Private key to sign blocks with
   --miner.recommit value                                                           Time interval to recreate the block being mined (default: 3s)
   --sentry.api.addr value                                                          Comma separated sentry addresses '<host>:<port>,<host>:<port>'
   --sentry.log-peer-info                                                           Log detailed peer info when a peer connects or disconnects. Enable to integrate with observer. (default: false)
   --downloader.api.addr value                                                      downloader address '<host>:<port>'
   --downloader.disable.ipv4                                                        Turns off ipv4 for the downloader (default: false)
   --downloader.disable.ipv6                                                        Turns off ipv6 for the downloader (default: false)
   --no-downloader                                                                  Disables downloader component (default: false)
   --downloader.verify                                                              Verify snapshots on startup. It will not report problems found, but re-download broken pieces. (default: false)
   --healthcheck                                                                    Enable grpc health check (default: false)
   --bor.heimdall value                                                             URL of Heimdall service (default: "http://localhost:1317")
   --webseed value                                                                  Comma-separated URL's, holding metadata about network-support infrastructure (like S3 buckets with snapshots, bootnodes, etc...)
   --bor.withoutheimdall                                                            Run without Heimdall service (for testing purposes) (default: false)
   --bor.period                                                                     Override the bor block period (for testing purposes) (default: false)
   --bor.minblocksize                                                               Ignore the bor block period and wait for 'blocksize' transactions (for testing purposes) (default: false)
   --bor.milestone                                                                  Enabling bor milestone processing (default: true)
   --bor.waypoints                                                                  Enabling bor waypont recording (default: false)
   --polygon.sync                                                                   Enabling syncing using the new polygon sync component (default: true)
   --polygon.sync.stage                                                             Enabling syncing with a stage that uses the polygon sync component (default: false)
   --polygon.logindex                                                               Workaround for incorrect logIndex in RPC (default: false)
   --ethstats value                                                                 Reporting URL of a ethstats service (nodename:secret@host:port)
   --override.prague value                                                          Manually specify the Prague fork time, overriding the bundled setting (default: 0)
   --caplin.discovery.addr value                                                    Address for Caplin DISCV5 protocol (default: "0.0.0.0")
   --caplin.discovery.port value                                                    Port for Caplin DISCV5 protocol (default: 4000)
   --caplin.discovery.tcpport value                                                 TCP Port for Caplin DISCV5 protocol (default: 4001)
   --caplin.checkpoint-sync-url value [ --caplin.checkpoint-sync-url value ]        checkpoint sync endpoint
   --caplin.subscribe-all-topics                                                    Subscribe to all gossip topics (default: false)
   --caplin.max-peer-count value                                                    Max number of peers to connect (default: 128)
   --caplin.enable-upnp                                                             Enable NAT porting for Caplin (default: false)
   --caplin.max-inbound-traffic-per-peer value                                      Max inbound traffic per second per peer (default: "1MB")
   --caplin.max-outbound-traffic-per-peer value                                     Max outbound traffic per second per peer (default: "1MB")
   --caplin.adaptable-maximum-traffic-requirements                                  Make the node adaptable to the maximum traffic requirement based on how many validators are being ran (default: true)
   --sentinel.addr value                                                            Address for sentinel (default: "localhost")
   --sentinel.port value                                                            Port for sentinel (default: 7777)
   --sentinel.bootnodes value [ --sentinel.bootnodes value ]                        Comma separated enode URLs for P2P discovery bootstrap
   --sentinel.staticpeers value [ --sentinel.staticpeers value ]                    connect to comma-separated Consensus static peers
   --ots.search.max.pagesize value                                                  Max allowed page size for search methods (default: 25)
   --silkworm.exec                                                                  Enable Silkworm block execution (default: false)
   --silkworm.rpc                                                                   Enable embedded Silkworm RPC service (default: false)
   --silkworm.sentry                                                                Enable embedded Silkworm Sentry service (default: false)
   --silkworm.verbosity value                                                       Set the log level for Silkworm console logs (default: "info")
   --silkworm.contexts value                                                        Number of I/O contexts used in embedded Silkworm RPC and Sentry services (zero means use default in Silkworm) (default: 0)
   --silkworm.rpc.log                                                               Enable interface log for embedded Silkworm RPC service (default: false)
   --silkworm.rpc.log.maxsize value                                                 Max interface log file size in MB for embedded Silkworm RPC service (default: 1)
   --silkworm.rpc.log.maxfiles value                                                Max interface log files for embedded Silkworm RPC service (default: 100)
   --silkworm.rpc.log.response                                                      Dump responses in interface logs for embedded Silkworm RPC service (default: false)
   --silkworm.rpc.workers value                                                     Number of worker threads used in embedded Silkworm RPC service (zero means use default in Silkworm) (default: 0)
   --silkworm.rpc.compatibility                                                     Preserve JSON-RPC compatibility using embedded Silkworm RPC service (default: true)
   --beacon.api value [ --beacon.api value ]                                        Enable beacon API (available endpoints: beacon, builder, config, debug, events, node, validator, lighthouse)
   --beacon.api.addr value                                                          sets the host to listen for beacon api requests (default: "localhost")
   --beacon.api.cors.allow-methods value [ --beacon.api.cors.allow-methods value ]  set the cors' allow methods (default: "GET", "POST", "PUT", "DELETE", "OPTIONS")
   --beacon.api.cors.allow-origins value [ --beacon.api.cors.allow-origins value ]  set the cors' allow origins
   --beacon.api.cors.allow-credentials                                              set the cors' allow credentials (default: false)
   --beacon.api.port value                                                          sets the port to listen for beacon api requests (default: 5555)
   --beacon.api.read.timeout value                                                  Sets the seconds for a read time out in the beacon api (default: 5)
   --beacon.api.write.timeout value                                                 Sets the seconds for a write time out in the beacon api (default: 31536000)
   --beacon.api.protocol value                                                      Protocol for beacon API (default: "tcp")
   --beacon.api.ide.timeout value                                                   Sets the seconds for a write time out in the beacon api (default: 25)
   --caplin.blocks-archive                                                          sets whether backfilling is enabled for caplin (default: false)
   --caplin.blobs-archive                                                           sets whether backfilling is enabled for caplin (default: false)
   --caplin.states-archive                                                          enables archival node for historical states in caplin (it will enable block archival as well) (default: false)
   --caplin.blobs-immediate-backfill                                                sets whether caplin should immediatelly backfill blobs (4096 epochs) (default: false)
   --caplin.blobs-no-pruning                                                        disable blob pruning in caplin (default: false)
   --caplin.checkpoint-sync.disable                                                 disable checkpoint sync in caplin (default: false)
   --caplin.snapgen                                                                 enables snapshot generation in caplin (default: false)
   --caplin.mev-relay-url value                                                     MEV relay endpoint. Caplin runs in builder mode if this is set
   --caplin.validator-monitor                                                       Enable caplin validator monitoring metrics (default: false)
   --caplin.custom-config value                                                     set the custom config for caplin
   --caplin.custom-genesis value                                                    set the custom genesis for caplin
   --caplin.use-engine-api                                                          Use engine API for internal Caplin. useful for testing and if CL network is degraded (default: false)
   --trusted-setup-file value                                                       Absolute path to trusted_setup.json file
   --rpc.slow value                                                                 Print in logs RPC requests slower than given threshold: 100ms, 1s, 1m. Exluded methods: eth_getBlock,eth_getBlockByNumber,eth_getBlockByHash,eth_blockNumber,erigon_blockNumber,erigon_getHeaderByNumber,erigon_getHeaderByHash,erigon_getBlockByTimestamp,eth_call (default: 0s)
   --txpool.gossip.disable                                                          Disabling p2p gossip of txs. Any txs received by p2p - will be dropped. Some networks like 'Optimism execution engine'/'Optimistic Rollup' - using it to protect against MEV attacks (default: false)
   --sync.loop.block.limit value                                                    Sets the maximum number of blocks to process per loop iteration (default: 5000)
   --sync.loop.break.after value                                                    Sets the last stage of the sync loop to run
   --sync.parallel-state-flushing                                                   Enables parallel state flushing (default: true)
   --chaos.monkey                                                                   Enable 'chaos monkey' to generate spontaneous network/consensus/etc failures. Use ONLY for testing (default: false)
   --shutter                                                                        Enable the Shutter encrypted transactions mempool (defaults to false) (default: false)
   --shutter.p2p.bootstrap.nodes value [ --shutter.p2p.bootstrap.nodes value ]      Use to override the default p2p bootstrap nodes (defaults to using the values in the embedded config)
   --shutter.p2p.listen.port value                                                  Use to override the default p2p listen port (defaults to 23102) (default: 0)
   --polygon.pos.ssf                                                                Enabling Polygon PoS Single Slot Finality (default: false)
   --polygon.pos.ssf.block value                                                    Enabling Polygon PoS Single Slot Finality since block (default: 0)
   --pprof                                                                          Enable the pprof HTTP server (default: false)
   --pprof.addr value                                                               pprof HTTP server listening interface (default: "127.0.0.1")
   --pprof.port value                                                               pprof HTTP server listening port (default: 6060)
   --pprof.cpuprofile value                                                         Write CPU profile to the given file
   --trace value                                                                    Write execution trace to the given file
   --metrics                                                                        Enable metrics collection and reporting (default: false)
   --metrics.addr value                                                             Enable stand-alone metrics HTTP server listening interface (default: "127.0.0.1")
   --metrics.port value                                                             Metrics HTTP server listening port (default: 6061)
   --diagnostics.disabled                                                           Disable diagnostics (default: true)
   --diagnostics.endpoint.addr value                                                Diagnostics HTTP server listening interface (default: "127.0.0.1")
   --diagnostics.endpoint.port value                                                Diagnostics HTTP server listening port (default: 6062)
   --diagnostics.speedtest                                                          Enable speed test (default: false)
   --log.json                                                                       Format console logs with JSON (default: false)
   --log.console.json                                                               Format console logs with JSON (default: false)
   --log.dir.json                                                                   Format file logs with JSON (default: false)
   --verbosity value                                                                Set the log level for console logs (default: "info")
   --log.console.verbosity value                                                    Set the log level for console logs (default: "info")
   --log.dir.disable                                                                disable disk logging (default: false)
   --log.dir.path value                                                             Path to store user and error logs to disk
   --log.dir.prefix value                                                           The file name prefix for logs stored to disk
   --log.dir.verbosity value                                                        Set the log verbosity for logs stored to disk (default: "info")
   --log.delays                                                                     Enable block delay logging (default: false)
   --config value                                                                   Sets erigon flags from YAML/TOML file
   --help, -h                                                                       show help
   --version, -v                                                                    print the version
```
