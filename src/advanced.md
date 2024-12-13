# Advanced Usage

Erigon is by default an "all-in-one" binary solution, but it's possible start any internal component as a separated processes:

- [RPCDaemon](./advanced/rpc_daemon.md), the JSON RPC layer
- [TxPool](./advanced/txpool.md), the transaction pool
- [Sentry](./advanced/sentry.md), the p2p layer
- [Downloader](./advanced/downloader.md), the history download layer
- [Caplin](./advanced/caplin.md), the novel Consensus Layer

This may be for security, scalability, decentralisation, resource limitation, custom implementation, or any other reason you/your team deems appropriate. See the appropriate section to understand how to start each service separately.

> Don't start services as separated processes unless you have clear reason for it.
