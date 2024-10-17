# Consensus Layer

The Consensus Layer is a critical component of a decentralized network, responsible for reaching agreement on the state of the network. In the context of blockchain technology, the Consensus Layer is the layer that ensures the security and integrity of the blockchain by validating transactions and blocks.

Historically, an Execution Layer (EL) client alone was enough to run a full Ethereum node. However, as Ethereum has moved from proof-of-work (PoW) to proof-of-stake (PoS) based consensus with "The Merge", a Consensus Layer (CL) client needs to run alongside the EL to run a full Ethereum node, a Gnosis Chain node or a Polygon node.

The execution client listens to new transactions, executes them in the Ethereum Virtual Machine (EVM), and holds the latest state and database of all current Ethereum data.

The consensus client, also known as the Beacon Node or CL client, implements the Proof-of-Stake consensus algorithm, which enables the network to achieve agreement based on validated data from the execution client. Both clients work together to keep track of the head of the Ethereum chain and allow users to interact with the Ethereum network.

<div class="warning">
By default, Erigon is configured to run with Caplin, the embedded Consensus Layer.
</div>


## Caplin

Erigon can run with its flagship embedded consensus layer, Caplin, which provides fast and secure block validation. This option offers simplicity and reliability, making it a popular choice for many users.

## External Consensus Layer Clients

In addition to Caplin, Erigon also supports external consensus layer clients, such as Lighthouse, Lodestar, Nimbus, Prysm, and Teku. These clients offer flexibility and customization options, allowing users to choose the best solution for their specific needs.

## Standalone Caplin Client and External Integration

Caplin can also be used as a standalone client, connected to another execution client like Geth, providing a unique integration option. Furthermore, blocks can be validated using either Caplin or an external consensus layer client, giving users flexibility in their validation approach.