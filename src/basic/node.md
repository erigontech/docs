# Type of Node

Erigon 3 introduces a flexible approach to node configuration, offering three distinct types to suit various user needs. Depending on your need, you can choose from three different node types.

If you are looking for more **privacy** during your interaction with EVM, like for example sending transactions with your node, you can use a [minimal node](#minimal-node), which is fast to set up and uses a minimal amount of [disk space](disk-space.md).

If you want to do extensive **research**, like for example searching for old states of the EVM, or implementing Otterscan, you will need an [archive node](#archive-node).

If you want to run a validator and produce blocks, **staking** is achievable already with a [full node](#full-node).


| Usage        | Minimal Node | Full Node | Archive Node |
|--------------|--------------|-----------|--------------|
| Privacy, RPC |    **Yes**   |   **Yes** |    **Yes**   |
| Research     |    No        |    No     |    **Yes**   |
| Staking      |    No        |  **Yes**  |    **Yes**   |


To switch type of node, you must first delete the ```/chaindata``` folder in the chosen ```--datadir``` directory.

## Archive node
The traditional Archive Node remains the default, providing complete historical data.

## Full node
For users seeking a balance between storage efficiency and functionality, the Full Node option can be activated with the flag `--prune.mode=full`. For example:

```bash
./build/bin/erigon --prune.mode=full
```

This setup maintains essential data while reducing storage requirements.

## Minimal node
Erigon 3 implements support for [EIP-4444](https://eips.ethereum.org/EIPS/eip-4444) through its *Minimal Node configuration*, enabled by the flag `--prune.mode=minimal`. For example:

```bash
./build/bin/erigon --prune.mode=minimal
```

This lightweight option aligns with the Ethereum Improvement Proposal's goal of reducing long-term storage burden on nodes, potentially improving network scalability and participation.