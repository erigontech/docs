# Sentry
*P2P network management*

Sentry connects Erigon to the Ethereum P2P network, enabling the discovery of other participants across the Internet and secure communication with them. It performs these main functions: 

- Peer discovery via the following:
    - Kademlia DHT
    - DNS lookup
    - Configured static peers
    - Node info saved in the database
    - Boot nodes pre-configured in the source code

- Peer management:
    - handshakes
    - holding p2p connection even if Erigon is restarted

The ETH core interacts with the Ethereum p2p network through the Sentry component. Sentry provides a simple interface to the core, with functions to download data, receive notifications about gossip messages, upload data on request from peers, and broadcast gossip messages either to a selected set of peers or to all peers.

## Running with an external Sentry or multiple Sentries

It is possible to have multiple Sentry to increase connectivity to the network or to obscure the location of the core computer. In this case it is necessary to define address and port of each Sentry that should be connected to the Core.

Before using the Sentry component the executable must be built. Head over to /erigon directory and type:

```bash
make sentry
```

Then it can be launched as an independent component with the command:

```bash
./build/bin/sentry
```

### Example

In this example we will run an instance of Erigon and Sentry on the same machine.

Following is the Sentry client running separately:  

```bash
screen ./build/bin/sentry --datadir=~/.local/share/erigon
```

And here is Erigon attaching to it

```bash
./build/bin/erigon --internalcl --snapshots=true --sentry.api.addr=127.0.0.1:9091
```

Erigon might be attached to several Sentry instances running across different machines. As per Erigon help:

```bash
--sentry.api.addr value
```

Where `value` is comma separated sentry addresses '<host>:<port>,<host>:<port>'

## Command line options

To display available options for sentry digit:

```bash
./build/bin/sentry --help
```