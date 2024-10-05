# Hardware Requirements

## Disk type

A locally mounted SSD (Solid-State Drive) or NVMe (Non-Volatile Memory Express) disk is recommended for storage. Hard Disk Drives (HDD) are not recommended, as they can cause Erigon to lag behind the blockchain tip, albeit not fall behind.

Additionally, SSDs may experience performance degradation when nearing full capacity.

See here how you can [optimize storage](/basic/optimizing-storage.md).

## RAID Configuration

When using multiple disks, consider implementing a RAID0 configuration to maximize performance and utilize space efficiently. Note that RAID ZFS is not recommended

## Disk size

Please refer to [disk space required](/basic/disk-space.md) for details. To ensure smooth operation, it is recommended to maintain at least 25% of free disk space. For more detailed guidance on optimizing storage, refer to disk space required.

## CPU Requirements

* **Architecture**: 64-bit architecture.
* **Number of core and threads**: while a powerful CPU can help, it's not essential for running Erigon. A moderate number of cores and threads should suffice.

## RAM Requirements
    
* **Minimum**: 32GB

## Kernel Requirements

* **Linux**: kernel version > v4

