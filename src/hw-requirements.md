# Hardware Requirements

## Disk type

A locally mounted SSD or NVMe disk is recommended for storage. HDD is not recommended because it will cause Erigon to always stay N blocks behind the chain tip, but not fall behind. In addition, SSD performance degrades when close to full capacity.

When using multiple hard drives, a RAID0 configuration is recommended as it offers high performance and efficient use of space. Raid ZFS is not recommended.

See here how you can [optimize storage](optimizing-storage.md).

## Disk size

Refer to [node](node.md) chapter.

## CPU 

CPU: 64-bit architecture. Number of core and threads is not really important, you don't need a super powerful computer to run Erigon.

## RAM
    
RAM: ≥ 32GB

## Kernel

On Linux: kernel > v4

# Tips for Faster Sync​

Use the machine with low latency (not throughput) disk and RAM for the faster initial sync.

Memory optimized nodes are recommended for faster sync. For example, AWS EC2 r5 or r6 series instances.
