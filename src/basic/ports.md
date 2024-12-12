# Default Ports and Firewalls

Main recommendations:

- Avoid exposing other ports unless necessary for specific use cases (e.g., JSON-RPC or WebSocket).
- Regularly audit your firewall rules to ensure they are aligned with your infrastructure needs.
- Use monitoring tools like Prometheus or Grafana to track P2P communication metrics.

This minimal configuration ensures proper P2P functionality for both the Execution and Consensus layers without exposing unnecessary services. Let me know if you need further clarifications!


Too see ports used by Erigon and its components please refer to <https://github.com/erigontech/erigon?tab=readme-ov-file#default-ports-and-firewalls>.

To ensure proper P2P functionality for both the Execution and Consensus layers use a minimal configuration without exposing unnecessary services:

- Avoid exposing other ports unless necessary for specific use cases (e.g., JSON-RPC or WebSocket);
- Regularly audit your firewall rules to ensure they are aligned with your infrastructure needs;
- Use monitoring tools like Prometheus or Grafana to track P2P communication metrics.

## Command-Line Switches for Network and Port Configuration

Here is an extensive list of port-related options from the [options](/advanced/options.md) list:

### Engine

- `--private.api.addr [value]`: Erigon's internal gRPC API, empty string means not to start the listener (default: ```127.0.0.1:9090```)
- `--txpool.api.addr [value]`: TxPool api network address, (default: use value of `--private.api.addr`)
- `--torrent.port [value]`: Port to listen and serve BitTorrent protocol (default: `42069`)
- `--authrpc.port [value]`: HTTP-RPC server listening port for the Engine API (default: `8551`)

### Sentry

- `--port [value]`: Network listening port (default: `30303`)
- `--p2p.allowed-ports [value]`: Allowed ports to pick for different eth p2p protocol versions (default: `30303`, `30304`, `30305`, `30306`, `30307`)
- `--sentry.api.addr [value]`:  Comma separated sentry addresses ```<host>:<port>,<host>:<port>``` (default ```127.0.0.1:9091```)

### RPCdaemon

- `--ws.port [value]`: WS-RPC server listening port (default: `8546`)
- `--http.port [value]`: HTTP-RPC server listening port (default: `8545`)

### Caplin

- `--caplin.discovery.port [value]`: Port for Caplin DISCV5 protocol (default: `4000`)
- `--caplin.discovery.tcpport [value]`: TCP Port for Caplin DISCV5 protocol (default: `4001`)

### BeaconAPI

- `--beacon.api.port [value]`: Sets the port to listen for beacon api requests (default: `5555`)

### Diagnostics

- `--diagnostics.endpoint.port [value]`: Diagnostics HTTP server listening port (default: `6062`)

### Shared ports

- `--pprof.port [value]`: pprof HTTP server listening port (default: `6060`)
- `--metrics.port [value]`: Metrics HTTP server listening port (default: `6061`)
- `--downloader.api.addr [value]`: Downloader address ```<host>:<port>```






