# Contributing to Erigon 3

## Development

Erigon is an open-source project that welcomes contributions from developers worldwide who are passionate about advancing the Ethereum ecosystem. Bounties may be offered for noteworthy contributions, as the team is committed to continuously enhancing the tool to better serve the Erigon community.

### Programmer's Guide

Begin by exploring the comprehensive **[Programmer's Guide](https://github.com/ledgerwatch/erigon/blob/devel/docs/programmers_guide/guide.md)**, which covers topics such as the Ethereum state structure, account contents, and account addressing mechanisms. This guide serves as a valuable resource, providing detailed information on Erigon's architecture, coding conventions, and development workflows related to managing and interacting with the Ethereum state.

### Dive Deeper into the Architecture

For those interested in gaining a deeper understanding of Erigon's underlying architecture, visit the following resources:

- **[DB Walk-through](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_walkthrough.MD)**: This document provides a detailed walk-through of Erigon's database structure. It explains how Erigon organizes persistent data into tables like PlainState for accounts and storage, History Of Accounts for tracking account changes, and Change Sets for optimized binary searches on changes. It contrasts Erigon's approach with go-ethereum's use of the Merkle Patricia Trie.
- **[Database FAQ](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_faq.md)**: The Database FAQ addresses common questions and concerns related to Erigon's database design. It covers how to directly read the database via gRPC or while Erigon is running, details on the MDBX storage engine and RAM usage model, and points to further resources on the database interface rationale and architecture.
- **[DB Walk-through](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_walkthrough.MD)**: This document provides a detailed walk-through of Erigon's database structure. It explains how Erigon organizes persistent data into tables like PlainState for accounts and storage, History Of Accounts for tracking account changes, and Change Sets for optimized binary searches on changes. It contrasts Erigon's approach with go-ethereum's use of the Merkle Patricia Trie.
- **[Database FAQ](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/db_faq.md)**: The Database FAQ addresses common questions and concerns related to Erigon's database design. It covers how to directly read the database via gRPC or while Erigon is running, details on the MDBX storage engine and RAM usage model, and points to further resources on the database interface rationale and architecture.

### Feature Exploration

Erigon introduces several innovative features that contributors may find interesting to explore and contribute to:

- **[DupSort Feature Explanation](https://github.com/erigontech/erigon/blob/release/2.60/docs/programmers_guide/dupsort.md)**: Erigon's DupSort feature optimizes storage and retrieval of duplicate data by utilizing prefixes for keys in databases without the concept of "Buckets/Tables/Collections" or by creating tables for efficient storage with named "Buckets/Tables/Collections."
- **[EVM without Opcodes](https://github.com/erigontech/erigon/blob/release/2.60/docs/evm_semantics.md)** (Ether Transfers Only): Erigon explores a simplified version of the Ethereum Virtual Machine (EVM) focusing solely on ether transfers, offering an efficient execution environment for specific use cases.
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

# Documentation

To contribute to this documentation, commit your change to the development branch on **[Github](https://github.com/erigontech/docs/tree/development)**. You might want to run it locally to verify the output before committing, see how MdBook works [here](https://rust-lang.github.io/mdBook/index.html).
