# Welcome to Erigon 3!
             
>
> **NOTE**: The Erigon 3 book is under construction and you may find broken links, empty pages and inexact information.
> 
> For instructions regarding Erigon 2 please refer to <https://erigon.gitbook.io>.




	########b          oo                               d####b. 
	##                                                      '## 
	##aaaa    ##d###b. dP .d####b. .d####b. ##d###b.     aaad#' 
	##        ##'  '## ## ##'  '## ##'  '## ##'  '##        '## 
	##        ##       ## ##.  .## ##.  .## ##    ##        .## 
	########P dP       dP '####P## '#####P' dP    dP    d#####P 
	                           .##                              
	                       d####P    

> **DISCLAIMER**: Erigon 3 is in alpha phase and it is not recommended to be used in production environments. The Erigon team does not take any responsibility for losses or damages occurred through the use of Erigon. While we employ a seasoned in-house security team, we have not subjected our systems to independent third-party security assessments, leaving potential vulnerabilities to bugs or malicious activity unaddressed. It is essential for validators to be aware that unforeseen events, including software glitches, may result in lost rewards.

Erigon is an efficient Ethereum implementation designed for speed, modularity, and optimization. By default, it functions as an archive node, utilizing technologies like staged sync, efficient state storage, and database compression.

With **Erigon v3 Alpha 6**, the default configuration shifts from archive node to full node, enhancing efficiency, accessibility, and versatility for a wider range of users. Archive nodes remain available for developers and researchers needing full historical data, while the full node offers faster sync times and lower resource usage for everyday operations. More info [here](https://erigon.tech/announcing-erigon-v3-alpha-6-focus-on-staking-and-full-node-performance/).

<div class="warning">

**Information**

If you wanto to test Erigon in minutes, go straight to the [quick nodes](quick_nodes.md) section.

</div>

# Features

Erigon offers several features that make it a good option for a node application such as efficient state storage through the use of a key-value database and faster initial synchronisation.

Built with modularity in mind, it also offers separate components such as the JSON RPC daemon, that can connect to both local and remote databases. For read-only calls, this RPC daemon does not need to run on the same system as the main Erigon binary, and can even run from a database snapshot.

Erigon 3 is a major update that introduces several significant changes, improvements, and optimizations. Some of the key features and differences include:

The main changes from Erigon 2 are listed [here](https://github.com/erigontech/erigon?tab=readme-ov-file#erigon3-changes-from-erigon2).

# Release Process

Erigon 3 also introduces changes to the release process, including:
* New Docker Image Repository: Erigon images are now available on Dockerhub repository "erigontech/erigon".
* Multi-Platform Support: The docker image is built for linux/amd64/v2 and linux/arm64 platforms using Alpine 3.20.2.
* Release Workflow Changes: Build flags are now passed to the release workflow, allowing users to view previously missed build information in released binaries.
