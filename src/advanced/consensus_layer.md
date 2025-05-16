# Consensus Layer

The Consensus Layer (CL) is a critical component of a decentralized network, responsible for reaching agreement on the state of the network. In the context of blockchain technology, the CL ensures the security and integrity of the blockchain by validating transactions and blocks.

Historically, an Execution Layer (EL) client alone was sufficient to run a full Ethereum node. However, as Ethereum transitioned from proof-of-work (PoW) to proof-of-stake (PoS) based consensus with "The Merge," a CL client must run alongside the EL to operate an Ethereum node, a Gnosis Chain node, or a Polygon node.

The execution client listens to new transactions, executes them in the Ethereum Virtual Machine (EVM), and maintains the latest state and database of all current Ethereum data.

The CL client, also known as the Beacon Node, implements the Proof-of-Stake consensus algorithm. This enables the network to achieve agreement based on validated data from the execution client. Both clients work together to keep track of the head of the Ethereum chain and allow users to interact with the Ethereum network.

Basically, without a CL client, the EL will never sync.

<div class="warning">

**Information**

By default, Erigon is configured to run with [Caplin](/advanced/caplin.md), the embedded CL.
</div>

## Choosing an external CL client

While Erigon runs by default with Caplin, the embedded CL, it is possible to run Erigon with any external CL. Below are some examples of how to configure Lighthouse and Prysm to run alongside Erigon:

- [Ethereum](/nodes/eth_extcl.md)
- [Gnosis Chain](/nodes/gno_extcl.md)

> **Important note**: When configuring a CL client, always refer to the official CL documentation for the most up-to-date and accurate configuration instructions to avoid any potential issues.
