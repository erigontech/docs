# Caplin

Caplin, the novel embedded Consensus Layer, brings unparalleled performance, efficiency, and reliability to Ethereum infrastructure. Its innovative design minimize disk usage, enabling faster transaction processing and a more secure network.

By integrating the consensus layer into the EVM-node, Caplin eliminates the need for separate disk storage, reducing overall system complexity and improving overall efficiency. OtterSync, a new syncing algorithm, further enhances performance by shifting 98% of the computation to network bandwidth, reducing sync times and improving chain tip performance, disk footprint, and decentralization.

<img class="center" src="/images/ottersync.png" alt="Ottersync">

# Caplin Usage

Caplin is enabled by default, at which point an external consensus layer is no longer needed.

```bash
./build/bin/erigon
```

Caplin also has an archive mode for historical states and blocks, which can be enabled with the `--caplin.archive` flag.

Caplin can also be used for [block production](/advanced/block-prod.md).