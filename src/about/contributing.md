# Contributing

 
- [Contributing to Erigon 3](#contributing-to-erigon-3)
- [Contributing to Documentation](#contributing-to-this-documentation)


## Contributing to Erigon 3

### Development

Erigon is an open-source project that welcomes contributions from developers worldwide who are passionate about advancing the Ethereum ecosystem. Bounties may be offered for noteworthy contributions, as the team is committed to continuously enhancing the tool to better serve the Erigon community.

### Programmer's Guide

Begin by exploring the comprehensive **[Programmer's Guide](https://github.com/ledgerwatch/erigon/blob/devel/docs/programmers_guide/guide.md)**, which covers topics such as the Ethereum state structure, account contents, and account addressing mechanisms. This guide serves as a valuable resource, providing detailed information on Erigon's architecture, coding conventions, and development workflows related to managing and interacting with the Ethereum state.

### Dive Deeper into the Architecture

For those interested in gaining a deeper understanding of Erigon's underlying architecture, visit the following resources:
- **[DB Walk-through](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_walkthrough.MD)**: This document provides a detailed walk-through of Erigon's database structure. It explains how Erigon organizes persistent data into tables like PlainState for accounts and storage, History Of Accounts for tracking account changes, and Change Sets for optimized binary searches on changes. It contrasts Erigon's approach with go-ethereum's use of the Merkle Patricia Trie.
- **[Database FAQ](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_faq.md)**: The Database FAQ addresses common questions and concerns related to Erigon's database design. It covers how to directly read the database via gRPC or while Erigon is running, details on the MDBX storage engine and RAM usage model, and points to further resources on the database interface rationale and architecture.

### Feature Exploration

Erigon introduces several innovative features that contributors may find interesting to explore and contribute to:
- **[DupSort Feature Explanation](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/dupsort.md)**: Erigon's DupSort feature optimizes storage and retrieval of duplicate data by utilizing prefixes for keys in databases without the concept of "Buckets/Tables/Collections" or by creating tables for efficient storage with named "Buckets/Tables/Collections."
- **[EVM without Opcodes](https://github.com/erigontech/erigon/blob/release/2.60/docs/evm_semantics.md)** (Ether Transfers Only): Erigon explores a simplified version of the Ethereum Virtual Machine (EVM) focusing solely on ether transfers, offering an efficient execution environment for specific use cases.

## Wiki

Visit also Erigon's **[Wiki](https://github.com/ledgerwatch/erigon/wiki)** to gain more important insights:

- Caplin downloader sync
- Choice of storage engine
- Consensus Engine separation
- Criteria for transitioning from Alpha to Beta
- Erigon Beta 1 announcement
- Erigon2 prototype
- EVM with abstract interpretation and backtracking
- Header downloader
- LMDB freelist
- LMDB freelist illustrated guide
- State sync design
- TEVM Trans-piled EVM: accelerate EVM improvement R&D, but learning from eWASM
- Transaction Pool Design
- Using Postman to test RPC.

# Contributing to this Documentation

This documentation is powered by [MdBook](https://rust-lang.github.io/mdBook).

To contribute to the Erigon 3 Docs, you can either:

1) Create an Issue: Open a new issue in the main branch to suggest changes or report problems.
2) Open a Branch and Submit a PR: Create a new branch, make your changes, and submit a pull request (PR) on Github.

Before committing your changes, it's recommended to run the documentation locally to verify the output. This ensures that your changes render correctly and maintain the consistency of the documentation.