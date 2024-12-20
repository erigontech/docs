# RPC Daemon
*Remote Procedure Call*

Like any other Erigon component, the Remote Procedure Call (RPC) can run within the Erigon all-in-one client or as an independent process. This has many advantages, including easier development, the ability to run multiple RPC daemons at once, and the ability to run the daemon remotely. It is also possible to run the daemon locally (in read-only) if both processes have access to the data folder.

## Built-in RPC daemon

To enable RPC daemon as a built-in service in Erigon add the flags `--http` and `--ws` (sharing same port with http). For example:

```bash
./build/bin/erigon --internalcl --http.vhosts="*" --http.addr="0.0.0.0" --http.api=eth,web3,net,debug,trace,txpool
```
<div class="warning">

**Warning**: The above example is a convenient but insecure snippet to allow users to connect their wallet from any host. To have a secure connection it is recommended to utilize [TLS Authentication](./tls-authentication.md).
</div>

This command run Erigon on a remote server allowing connection from any host, enabling http api for eth, web3, net etc. To connect a remote wallet use IP address of the remote machine on the RPC URL. Default port is 8545 e.g. `http://123.123.123.123:8545`.

## Websocket

Erigon supports also WebSocket protocol, just add the flag `--ws` to enable the WS-RPC server (default: `false`) or `--ws.compression` to enable compression over WebSocket (default: `false`).

In order to specify websocket server listening port you can use the flag `--ws.port` (default: `8546`)

## GraphQL

GraphQL protocol is also supported, add flag `--graphql`.

## RPC as a separate process

To build the RPC daemon separately run the command:

```bash
make rpcdaemon
```

The RPC daemon can use:
- The local database, with Erigon running or on a snapshot of a database
- A remote database running on another machine.

### Running locally

Running RPC daemon on the same computer along with Erigon is the default option because it uses Shared Memory access to Erigon's db, which is much faster than TCP access. Remember to always provide the following options:
- `--datadir` to specify where Erigon data are stored ,by default `/home/user/.local/share/erigon`
- `--private.api.addr` to provide private api network address (default `127.0.0.1:9090`)

For example:

```bash
./build/bin/erigon  --internalcl --private.api.addr=localhost:9090 --http=false
./build/bin/rpcdaemon --private.api.addr=localhost:9090 --http.vhosts="*" --http.addr="0.0.0.0" --http.api=eth,erigon,web3,net,debug,trace,txpool —-datadir=/home/usr/.local/share/erigon
```

With the above command it has also been specified which RPC namespaces to enable by `--http.api` flag.

### Running Remotely

In some cases, it is useful to run Erigon nodes in a different network (for example, in a public cloud), but RPC daemon locally. In this scenario the local machine requires no storing capacity and basic computing requirements.

<div class="warning">

**Warning**: to ensure the integrity of communication and access control to the Erigon node, [TLS Authentication](./tls-authentication.md) is needed.

</div>

This works regardless of whether RPC daemon is on the same computer with Erigon, or on a different one. They use TPC socket connection to pass data between them. To use this mode, run Erigon in one terminal window.

To start RPC daemon remotely - just don't set the `--datadir` flag:

```bash
./build/bin/erigon --internalcl --private.api.addr=localhost:9090 --http=false
./build/bin/rpcdaemon --private.api.addr=localhost:9090 --http.api=eth,erigon,web3,net,debug,trace,txpool
```

If the Erigon process is on one machine and RPC daemon is on another machine, use the `--private.api.addr` option for Erigon and open port `9090`:

```bash
./build/bin/erigon --internalcl --private.api.addr=0.0.0.0:9090 --http=false --http.vhosts="*" --http.addr="0.0.0.0"
```

On the other machine:

```bash
./build/bin/rpcdaemon --http.vhosts="*" --private.api.addr=123.123.123.123:9090 --http.api=eth,erigon,web3,net,debug,trace,txpool
```

For instance you can run also a number of different RPC daemon on different machines, attaching to the same Erigon process.

The daemon should respond with something like:

`INFO [date-time] HTTP endpoint opened url=localhost:8545...`

When running remotely, RPC daemon by default maintains a state cache that is updated each time Erigon imports a new block. When the state cache is reasonably warm, it allows such a remote RPC daemon to execute queries related to the latest block (i.e. current state) with comparable performance to a local RPC daemon (about 2x slower vs. 10x slower without state cache). Since there can be multiple such RPC daemons per Erigon node, it may scale well for some workloads that are heavy on current state queries.

## Healthcheck

There are 2 options for running healtchecks
- POST request
- GET request with custom headers.

Both options are available at the `/health` endpoint.

### POST request

If the health check is successful it returns `200 OK`.

If the health check fails it returns `500 Internal Server Error`.

Configuration of the health check is sent as POST body of the method.

```
{
"min_peer_count": <minimal number of the node peers>,
"known_block": <number_of_block_that_node_should_know>
}
```

Not adding a check disables that.

- `min_peer_count` checks for mimimum of healthy node peers. Requires net namespace to be listed in `http.api`.
- `known_block` sets up the block that node has to know about. Requires eth namespace to be listed in `http.api`.

Example request:

`http POST http://localhost:8545/health --raw '{"min_peer_count": 3, "known_block": "0x1F"}'`

Example response:
```
{
"check_block": "HEALTHY",
"healthcheck_query": "HEALTHY",
"min_peer_count": "HEALTHY"
}
```
### GET with headers

If the healthcheck is successful it will return a `200` status code.

If the healthcheck fails for any reason a status 500 will be returned. This is true if one of the criteria requested fails its check.

You can set any number of values on the X-ERIGON-HEALTHCHECK header. Ones that are not included are skipped in the checks.

Available Options:
- `synced` will check if the node has completed syncing
- `min_peer_count<count>` will check that the node has at least <count> many peers
- `check_block<block>` will check that the node is at least ahead of the specified <block>
- `max_seconds_behind<seconds>` - will check that the node is no more than <seconds> behind from its latest block

Example Request:

```
curl --location --request GET 'http://localhost:8545/health' \
--header 'X-ERIGON-HEALTHCHECK: min_peer_count1' \
--header 'X-ERIGON-HEALTHCHECK: synced' \
--header 'X-ERIGON-HEALTHCHECK: max_seconds_behind600'
```

Example Response:

```
{
"check_block":"DISABLED",
"max_seconds_behind":"HEALTHY",
"min_peer_count":"HEALTHY",
"synced":"HEALTHY"
}
```

## Testing

By default, the RPC daemon serves data from `localhost:8545`. You may send curl commands to see if things are working.

Try `eth_blockNumber` for example. In a third terminal window enter this command:

```bash
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc": "2.0", "method": "eth_blockNumber", "params": [], "id":1}' localhost:8545
```

This should return something along the lines of this (depending on how far your Erigon node has synced):

```
{
"jsonrpc": "2.0",
"id": 1,
"result":" 0xa5b9ba"
}
```

Postman may also be used to test RPC daemon.

## Command Line Options

RPCdaemon is started and controlled using the command line and it is stopped by pressing `CTRL-C`.

You can configure RPCdaemon using command-line options (a.k.a. flags), which you can use to specify also sub-commands to invoke other functionalities.

The command-line help listing is reproduced below for your convenience. The same information can be obtained at any time from your own RPCdaemon instance by running:

```bash
./build/bin/rpcdaemon --help
```

For more detailed on RPC daemon info refer to this page:

<https://github.com/erigontech/erigon/blob/main/cmd/rpcdaemon/README.md>