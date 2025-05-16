# Consensus Layer

The Consensus Layer is a critical component of a decentralized network, responsible for reaching agreement on the state of the network. In the context of blockchain technology, the Consensus Layer is the layer that ensures the security and integrity of the blockchain by validating transactions and blocks.

Historically, an Execution Layer (EL) client alone was enough to run a full Ethereum node. However, as Ethereum has moved from proof-of-work (PoW) to proof-of-stake (PoS) based consensus with "The Merge", a Consensus Layer (CL) client needs to run alongside the EL to run a full Ethereum node, a Gnosis Chain node or a Polygon node.

The execution client listens to new transactions, executes them in the Ethereum Virtual Machine (EVM), and holds the latest state and database of all current Ethereum data.

The consensus client, also known as the *Beacon Node* or *CL client*, implements the Proof-of-Stake consensus algorithm, which enables the network to achieve agreement based on validated data from the execution client. Both clients work together to keep track of the head of the Ethereum chain and allow users to interact with the Ethereum network.

<div class="warning">

**Information**

By default, Erigon is configured to run with [Caplin](/advanced/caplin.md), the embedded Consensus Layer.
</div>

## Choosing the Consensus Layer client

A CL client needs to run alongside Erigon to run a Ethereum node and a Gnosis Chain node or its respective testnets. Basically, without a CL client the EL will never get in sync. While Erigon run by default with Caplin, the embedded CL, it is possible to run Erigon with any external CL.

Below are some examples on how to configure Lighhouse and Prysm to run along with Erigon:

- [Ethereum](/advanced/eth_extcl.md)
- [Gnosis Chain](/advanced/gno_extcl.md)

> **Important Note**: When configuring a CL client, always refer to the official CL documentation for the most up-to-date and accurate configuration instructions in order to avoid any potential issues.