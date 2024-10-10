# Default Ports and Firewalls

Erigon Ports
-------------

| Component | Port | Protocol | Purpose | Should Expose |
| --------- | ---- | -------- | ------- | -------------- |
| Engine    | 9090 | TCP      | gRPC Server | Private        |
| Engine    | 42069 | TCP & UDP | Snap sync (Bittorrent) | Public         |
| Engine    | 8551 | TCP      | Engine API (JWT auth) | Private        |
| Sentry    | 30303 | TCP & UDP | eth/68 peering | Public         |
| Sentry    | 30304 | TCP & UDP | eth/67 peering | Public         |
| Sentry    | 9091 | TCP      | incoming gRPC Connections | Private       |
| RPCdaemon | 8545 | TCP      | HTTP & WebSockets & GraphQL | Private       |
| Diagnostics | 8080 | TCP & UDP| Diagnostic Tool | Private       |

Caplin ports
------------

| Component | Port | Protocol | Purpose | Should Expose |
| --------- | ---- | -------- | ------- | -------------- |
| Sentinel  | 4000 | UDP     | Peering | Public         |
| Sentinel  | 4001 | TCP     | Peering | Public         |

Shared ports
------------

| Component | Port | Protocol | Purpose | Should Expose |
| --------- | ---- | -------- | ------- | -------------- |
| All       | 6060 | TCP      | pprof   | Private        |
| All       | 6060 | TCP      | metrics | Private        |

Optional flags can be enabled that enable pprof or metrics (or both) - however, they both run on 6060 by default, so you'll have to change one if you want to run both at the same time.

Other ports
------------

* gRPC ports: 9092 consensus engine, 9093 snapshot downloader, 9094 TxPool

Hetzner firewall rules
----------------------

| IP Range                       | Description                                                                                                   |
| ------------------------------| -------------------------------------------------------------------------------------------------------------|
| 0.0.0.0/8                     | "This" Network (RFC 1122, Section 3.2.1.3)                                                              |
| 10.0.0.0/8                     | Private-Use Networks (RFC 1918)                                                                      |
| 100.64.0.0/10                  | Carrier-Grade NAT (CGN) (RFC 6598, Section 7)                                                    |
| 127.16.0.0/12                  | Private-Use Networks (RFC 1918)                                                                      |
| 169.254.0.0/16                 | Link Local (RFC 3927)                                                                                |
| 172.16.0.0/12                  | Private-Use Networks (RFC 1918)                                                                      |
| 192.0.0.0/24                   | IETF Protocol Assignments (RFC 5736)                                                            |
| 192.0.2.0/24                   | TEST-NET-1 (RFC 5737)                                                                                |
| 192.88.99.0/24                 | 6to4 Relay Anycast (RFC 3068)                                                                      |
| 192.168.0.0/16                 | Private-Use Networks (RFC 1918)                                                                      |
| 198.18.0.0/15                  | Network Interconnect Device Benchmark Testing (RFC 2544)                                     |
| 198.51.100.0/24                | TEST-NET-2 (RFC 5737)                                                                                |
| 203.0.113.0/24                 | TEST-NET-3 (RFC 5737)                                                                                |
| 224.0.0.0/4                    | Multicast (RFC 3171)                                                                                 |
| 240.0.0.0/4                    | Reserved for Future Use (RFC 1112, Section 4)                                                  |
| 255.255.255.255/32            | Limited Broadcast (RFC 919, Section 7)                                                            |
| 255.255.255.255/32            | RFC 922, Section 7                                                                                  |

Same in [IpTables](https://ethereum.stackexchange.com/questions/6386/how-to-prevent-being-blacklisted-for-running-an-ethereum-client/13068#13068) syntax.