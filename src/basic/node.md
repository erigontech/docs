# Type of Node

Erigon 3 introduces a flexible approach to node configuration, offering three distinct types to suit various user needs. Depending on your need, you can choose from three different node types.

| Usage        | Minimal Node | Full Node | Archive Node |
|--------------|--------------|-----------|--------------|
| Privacy, RPC |    **Yes**   |   **Yes** |    **Yes**   |
| Contribute to network | No  |   **Yes** |    **Yes**   |
| Contribute to network | No  |   **Yes** |    **Yes**   |
| Research     |    No        |    No     |    **Yes**   |
| Staking      |    **Yes**   |  **Yes**  |    **Yes**   |
| Staking      |    **Yes**   |  **Yes**  |    **Yes**   |

## Minimal node


Erigon 3 implements support for [EIP-4444](https://eips.ethereum.org/EIPS/eip-4444) through its *Minimal Node configuration*, enabled by the flag `--prune.mode=minimal`. For example:

```bash
./build/bin/erigon --prune.mode=minimal
```

Minimal node is suitable for users with constrained hardware who wants to achieve more **privacy** during their interaction with EVM, like for example sending transactions with your node. Minimal node is also suitable for staking. 

## Full node

Erigon 3 is full node by default (`--prune.mode=full`). This configuration delivers **faster sync times** and reduced resource consumption for everyday operation, maintaining essential data while **reducing storage requirements**. We recommend running a full node whenever possible, as it supports the network's decentralization, resilience, and robustness, aligning with Ethereum's trustless and distributed ethos. Given the reduced [disk space](disk-space.md) requirements of Erigon 3, the full node configuration is suitable for the majority of users.

## Archive node

Ethereum's state refers to account balances, contracts, and consensus data. Archive nodes store every historical state, making it easier to access past data, but requiring more disk space. They provide comprehensive historical data, making them optimal for conducting extensive **research** on the chain, ranging from searching for old states of the EVM to implementing advanced block explorers, such as Otterscan, and undertaking **development** activities.

Erigon 3 has consistently reduced the [disk space](disk-space.md) requirements for running an archive node, rendering it more affordable and accessible to a broader range of users. To run a archive node use the flag `--prune.mode=archive`.

<div class="warning">

**Information**

In order to switch type of node, you must first delete the ```/chaindata``` folder in the chosen ```--datadir``` directory.

</div>
