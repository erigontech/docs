# Welcome to Erigon 3!

	########b          oo                               d####b. 
	##                                                      '## 
	##aaaa    ##d###b. dP .d####b. .d####b. ##d###b.     aaad#' 
	##        ##'  '## ## ##'  '## ##'  '## ##'  '##        '## 
	##        ##       ## ##.  .## ##.  .## ##    ##        .## 
	########P dP       dP '####P## '#####P' dP    dP    d#####P 
	                           .##                              
	                       d####P                               


>
> **NOTE**:The Erigon 3 book is under construction: you may find broken links, empty pages and inexact  information.
> For instructions regarding Erigon 2 please refer to <https://erigon.gitbook.io>

> **DISCLAIMER**: Erigon 3 is still in alpha phase and it is not recommended to be used in production environments. The Erigon team does not take any responsibility for losses or damages occurred through the use of Erigon. While we employ a seasoned in-house security team, we have not subjected our systems to independent third-party security assessments, leaving potential vulnerabilities to bugs or malicious activity unaddressed. It is essential for validators to be aware that unforeseen events, including software glitches, may result in lost rewards.

Erigon is an efficiency frontier implementation of Ethereum, designed to provide a faster, more modular and optimised experience. An archive node by default, Erigon uses edge technologies such as staged sync, efficient state storage and database compression, combined with high modularity.

<div class="warning">

**Information**

If you wanto to test Erigon in minutes, go straight to the [quick nodes](quick_nodes.md) section.

</div>

# Features

Erigon offers several features that make it a good option for a node application such as efficient state storage through the use of a key-value database and faster initial synchronisation.

Built with modularity in mind, it also offers separate components such as the JSON RPC daemon, that can connect to both local and remote databases. For read-only calls, this RPC daemon does not need to run on the same system as the main Erigon binary, and can even run from a database snapshot.

Erigon 3 is a major update that introduces several significant changes, improvements, and optimizations. Some of the key features and differences include:

**Sync Improvements**

* **Sync from scratch** doesn't require re-executing **all history**. Instead, it leverages **snapshots** to download the latest state and its history.
* **ExecutionStage** now includes multiple E2 stages, such as ``stage_hash_state``, ``stage_trie``, ``stage_log_index``, ``stage_history_index``, and ``stage_trace_index``, for faster execution.
* **E3 can execute a single historical transaction** without executing its corresponding block, thanks to its **transaction-granularity indexing system**, which differs from a block-granularity approach.
* **E3 doesn't store Logs** (aka Receipts) - it always re-executes historical transactions (but it's cheaper than in E2 - see point above). Known performance issues: #10747
* **--sync.loop.block.limit** is enabled by default, with a default value of 5,000. To increase sync speed on good hardware, set ``--sync.loop.block.limit=10_000 --batchSize=2g``.

**Storage and Performance**

* **datadir/chaindata is small now** - to prevent its growth: we recommend setting ``--batchSize <= 2G``. It's also fine to remove the chaindata directory.
* Symlink or mount the latest state to a fast drive and history to a cheaper drive.

**Node Configuration**

- Archive Node is default. For full node and minimal node see [type of node](/basic/node.md).

**Other Features**

* **New User Guide**: A dedicated user guide for Erigon 3 provides detailed information on how to set up and configure your node.
* **Higher RAM Requirement**: Erigon 3 requires at least 64GB of RAM.

# Release Process

Erigon 3 also introduces changes to the release process, including:
* New Docker Image Repository: Erigon images are now available on Dockerhub repository "erigontech/erigon".
* Multi-Platform Support: The docker image is built for linux/amd64/v2 and linux/arm64 platforms using Alpine 3.20.2.
* Release Workflow Changes: Build flags are now passed to the release workflow, allowing users to view previously missed build information in released binaries.

# Known Issues

While Erigon 3 offers many improvements over its predecessor, there are still some known issues and limitations:
- don't `rm -rf` downloader, it will cause re-downloading of files (#10976).
