# Optimizing Storage
*Using fast disks and cheap disks*

For optimal performance, it's recommended to store the datadir on a fast NVMe-RAID disk. However, if this is not feasible, you can store the history on a cheaper disk and still achieve good performance.

## Step 1: Store datadir on the slow disk

Place the `datadir` on the slower disk. Then, create symbolic links (using `ln -s`) to the **fast disk** for the following sub-folders:

- `chaindata`
- `domain`

This will speed up the execution of E3.

On the **slow disk** place `datadir` folder with the following structure:
 - `chaindata` (linked to fast disk)
 - `snapshots`
 - `domain` (linked to fast disk)
 - `history`
 - `idx`
 - `accessors`
 - `temp`


## Step 2: Speed Up History Access (Optional)

If you need to further improve performance:

- Store the `accessors` folder on the fast disk. This should provide a noticeable speed boost.
- If the speed is still not satisfactory, move the `idx` folder to the fast disk.
- If performance is still an issue, consider moving the entire history folder to the fast disk.

By following these steps, you can optimize your Erigon 3 storage setup to achieve a good balance between performance and cost.