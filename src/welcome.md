# Welcome to Erigon 3!

	########b          oo                               d####b. 
	##                                                      '## 
	##aaaa    ##d###b. dP .d####b. .d####b. ##d###b.     aaad#' 
	##        ##'  '## ## ##'  '## ##'  '## ##'  '##        '## 
	##        ##       ## ##.  .## ##.  .## ##    ##        .## 
	########P dP       dP '####P## '#####P' dP    dP    d#####P 
	                           .##                              
	                       d####P                               


Erigon is an efficiency frontier implementation of Ethereum, designed to provide a faster, more modular and optimised experience. An archive node by default, Erigon uses edge technologies such as staged sync, efficient state storage and database compression, combined with high modularity.

Erigon offers several features that make it a good option for a node application such as efficient state storage through the use of a key-value database and faster initial synchronisation.

It also offers a separate JSON RPC daemon, that can connect to both local and remote databases. For read-only calls, this RPC daemon does not need to run on the same system as the main Erigon binary, and can even run from a database snapshot.

Erigon 3 is a major update that introduces several significant changes, improvements, and optimizations. Some of the key features and differences include:
* **New User Guide**: A dedicated user guide for Erigon 3 provides detailed information on how to set up and configure your node.
* **Higher RAM Requirement**: Erigon 3 requires at least 64GB of RAM (which may be reduced in future releases).
* **Golang 1.21**: The new version is built with Golang 1.21, which brings various improvements and enhancements.
* **Sync from Scratch**: Syncing from scratch doesn't require re-executing all history; instead, it uses snapshots to download the latest state and its history.
* **ExecutionStage**: Erigon 3 includes multiple stages in ExecutionStage (e.g., stage_hash_state, stage_trie) for faster execution.
* **Transaction-Level Execution**: Erigon 3 can execute individual historical transactions without executing their entire block, thanks to transaction-granularity indices.
Log Storage Removal: Logs (Receipts) are no longer stored in the datadir; instead, they are re-executed when needed.
* **Default Archive Node**: Erigon 3 is now an archive node by default, with pruning options for [Full Nodes](./basic/node.md#full-node) and [Minimal Nodes (EIP-4444)](./basic/node.md#minimal-node).
* **Improved Performance**: The new version offers faster performance, reduced startup time, and lower read-IO.

## Release Process

Erigon 3 also introduces changes to the release process, including:
* New Docker Image Repository: Erigon images are now available on Dockerhub repository "erigontech/erigon".
* Multi-Platform Support: The docker image is built for linux/amd64/v2 and linux/arm64 platforms using Alpine 3.20.2.
* Release Workflow Changes: Build flags are now passed to the release workflow, allowing users to view previously missed build information in released binaries.

## Known Issues

While Erigon 3 offers many improvements over its predecessor, there are still some known issues and limitations:
- `Trace_callMany` support for multiple transactions: #11798
- Windows binaries are not yet published, but will be available once the necessary work is completed.
- Users may encounter performance issues on chain-tip; `rm -rf chaindata` can help resolve these issues.