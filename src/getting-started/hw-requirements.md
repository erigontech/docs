# Hardware Requirements

## Disk type

A locally mounted **SSD** (Solid-State Drive) or **NVMe** (Non-Volatile Memory Express) disk is recommended for storage. **Avoid Hard Disk Drives (HDD)**, as they can cause Erigon to lag behind the blockchain tip, albeit not fall behind.

Additionally, SSDs may experience performance degradation when nearing full capacity.

See here how you can [optimize storage](../basic/optimizing-storage.md).


Here is the outline of the hardware requirements for running Erigon on the following networks:

- Ethereum Mainnet
- Polygon (formerly Matic)
- Gnosis (formerly xDai)

Hardware requirements vary depending on whether you're running a Minimal, Full, or Archive node.

General recommendations for all node types include:

- **Disk Type:** Use high-end NVMe SSDs. RAID or ZFS setups may improve performance for archive nodes.
- **RAM:** Adequate memory reduces bottlenecks during sync and improves performance under load.
- **CPU:** 4–8 cores recommended for Full nodes; 8–16 cores for Archive.
- **Linux**: kernel version > v4
- When using multiple disks, consider implementing a **RAID 0** configuration to maximize performance and utilize space efficiently. RAID ZFS is not recommended.


## Minimal Node Requirements

Minimal nodes are suitable for light operation with pruned state and minimal historical data retention. (`--prune.mode=minimal`)

| Network   | Disk Size (Required) | Disk Size (Recommended) | RAM (Required) | RAM (Recommended) |
|-----------|----------------------|--------------------------|----------------|-------------------|
| Mainnet   | 500 GB       | 500 GB        | 16 GB           | 64 GB             |
| Polygon   | 2 TB  | 2 TB        | 32 GB           | 64 GB             |
| Gnosis    | 250 GB         | 500 GB      | 8 GB           | 16 GB              |


## Full Node Requirements

Full nodes maintain full state with standard pruning and all recent data.  (`--prune.mode=full`)

| Network   | Disk Size (Required) | Disk Size (Recommended) | RAM (Required) | RAM (Recommended) |
|-----------|----------------------|--------------------------|----------------|-------------------|
| Mainnet   | 1 TB       | 2 TB    | 16 GB          | 64 GB             |
| Polygon   | 2 TB   | 4 TB    | 16 GB          | 32 GB             |
| Gnosis    | 500 GB       | 1 TB          | 8 GB           | 16 GB             |


## Archive Node Requirements

Archive nodes retain **all** historical state and require significantly more disk space. These are typically used for block explorers or deep analytical queries. (`--prune.mode=archive`)

| Network   | Disk Size (Required) | Disk Size (Recommended) | RAM (Required) | RAM (Recommended) |
|-----------|----------------------|--------------------------|----------------|-------------------|
| Mainnet   | 2 TB     | 4 TB       | 32 GB          | 64 GB            |
| Polygon   | 4.3 TB   | 6 TB        | 64 GB          | 128 GB             |
| Gnosis    | 1 TB           | 2 TB         | 16 GB          | 32 GB             |



## Bandwidth Requirements

Your internet bandwidth is also an important factor, particularly for sync speed and validator performance.

| Node Type     | Bandwidth (Required) | Bandwidth (Recommended) |
|---------------|----------------------|--------------------------|
| Staking/Mining       | 10 Mbps              | 50 Mbps                 |
| Non-Staking   | 5 Mbps               | 25 Mbps                 |
