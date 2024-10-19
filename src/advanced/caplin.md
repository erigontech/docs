# Caplin

Caplin's Erigon 3 represents a major breakthrough in Ethereum infrastructure, offering unparalleled performance, efficiency, and reliability. Its innovative all-in-one design and disk-saving features make it an attractive solution for developers, users, and the broader Ethereum ecosystem.

The main reason for developing a new consensus layer is to improve the node architecture by overcoming the limitation of Engine API.  For example, the Engine API sends data one block at a time, while Erigon is designed to handle many blocks at once and needs to sort and process data efficiently. Therefore, it would be better for Erigon to handle the blocks independently instead of relying on the Engine API.

**Strengths and Performances:**

* Thanks to Caplin, Erigon 3 is the world's first all-in-one EVM-node on the efficient software frontier;
* The integration of a consensus layer within the EVM-node enables faster and more efficient transaction processing, ensuring a more secure and reliable network.
* Caplin's all-in-one design allows for seamless integration with existing Ethereum infrastructure, making it an attractive solution for developers and users seeking to upgrade their experience.

**Disk-Saving Features:**

* Caplin's Erigon 3 (Alpha 1) boasts a unique consensus layer design that minimizes disk usage, resulting in significant storage space savings.
* This innovative approach enables Caplin to optimize its EVM-node, ensuring that it can handle increased transaction volumes while maintaining minimal disk usage.
* By integrating the consensus layer into the EVM-node, Caplin eliminates the need for separate disk storage, reducing overall system complexity and improving overall efficiency.

# Caplin Usage

Caplin is enabled by default, at which point an external consensus layer is no longer needed.

```bash
./build/bin/erigon
```

Caplin also has an archive mode for historical states and blocks, which can be enabled with the `--caplin.archive` flag.

Caplin can also be used for [block production](/advanced/block-prod.md).