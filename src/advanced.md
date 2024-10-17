# Advanced Usage

Erigon is by default an "all-in-one" binary solution, but it's possible start any internal component as a separated processes:

- RPCDaemon, the JSON RPC layer
- TxPool, the transaction pool
- Sentry, the p2p layer
- Downloader, the history download layer
- Caplin, the novel Consensus Layer

This may be for security, scalability, decentralisation, resource limitation, custom implementation, or any other reason you/your team deems appropriate. See the appropriate section to understand how to start each service separately.

<div class="warning">

Don't start services as separated processes unless you have clear reason for it.

</div>
