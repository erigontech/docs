# Performance Tricks

These instructions are designed to improve the performance of Erigon 3, particularly for synchronization and memory management, on cloud drives and other systems with specific performance characteristics.

## Increase Sync Speed

* Increase download speed with flag ```--torrent.download.rate=[value]``` setting your max speed (default value is 128MB). For example:
```bash
--torrent.download.rate=512mb
```


## Lock Latest State in RAM

* Use `vmtouch -vdlw /mnt/erigon/snapshots/domain/*bt` to lock the "latest state indices" in RAM, preventing it from being evicted due to high historical RPC traffic.
```bash
vmtouch -vdlw /mnt/erigon/snapshots/domain/*bt
```

* Or same for "whole latest sate": `ls /mnt/erigon/snapshots/domain/*.kv | parallel vmtouch -vdlw`
* If you encounter "cannot allocate memory" issues with above commands, then free memory by next command and re-try: 
```bash
sync && sudo sysctl vm.drop_caches=3 && echo 1 > /proc/sys/vm/compact_memory
```

## Optimize for Cloud Drives

* Cloud Drives (gp3, pd-ssd) have good throughput but bad latency. So, we don't recommend them to Erigon. But still can set `SNAPSHOT_MADV_RND=false` to enable the operating system's cache prefetching - but it will lead to huge IO if RAM is small. 
```bash
SNAPSHOT_MADV_RND=false
```
