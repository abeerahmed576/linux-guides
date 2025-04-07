> ***This guide is for Ext2/3/4 & Btrfs filesystems only***

Resizing partitions safely mainly involves two steps: resizing the filesystem and resizing the partition. Growing partition requires increasing the partition size first and then growing the filesystem and in the case of shrinking partition, it's the exact opposite order.

### Growing

1. Enter `parted` (GNU Parted) interactive mode for the disk device:

    ```sh
    (root) parted /dev/sdX
    ```

2. Now, use the `resizepart` command to set the new end for the partition.

    ```sh
    (parted) resizepart <partition_number> <new_end>
    ```

    - `new_end` can be specified in `s` (512-byte sectors), `B` (bytes), `MiB`, `GiB` etc. To determine the `partition_number`, use the `print` command to get details of the disk device. Also run `unit s` to see the size of partitions in sectors.

3. Now, we can grow the the filesystem to use the newly gained free space. Before growing, we have to perform a mandatory `fsck` (File System Consistency Check):

    ```sh
    (root) e2fsck -f /dev/sdXY
    ```

    Then, to grow the filesystem:

    ```sh
    (root) resize2fs /dev/sdXY <new_size>
    ```

    For Btrfs: (needed to be mounted first with option `subvol=/`)

    ```sh
    (root) btrfs filesystem resize <new_size>/max <path_to_mountpoint>/
    ```

    - `path_to_mountpoint` is where the btrfs partition is mounted. `max` will take all available space in the partition.

    - `new_size` can be specified in `G` (GiB), `M` (MiB) etc. Obviously, it has to be larger than the old size. In the case ext2/3/4 filesysytem, if we want to use all of the remaining space in partition, we can simply not specify any size and the command will default to the size of the partition.

### Shrinking

> Ext filesystems do not support online resizing. They need to be unmounted first for successful shrinking operation. It's better to use a Live Linux ISO for the following operations.

1. Before shrinking, we have to perform a mandatory `fsck` (File System Consistency Check):

    ```sh
    (root) e2fsck -f /dev/sdXY
    ```

    Then, to shrink the filesystem:

    ```sh
    (root) resize2fs /dev/sdXY <new_size>
    ```
    For Btrfs: (needed to be mounted first with option `subvol=/`)

    ```sh
    (root) btrfs filesystem resize <new_size>/max <path_to_mountpoint>/
    ```
    - `new_size` can be specified in `G` (GiB), `M` (MiB) etc. Obviously, it has to be smaller than the old size.

 	Then unmount.

    <br/>
    
    > Note: Before moving forward to resizing the partition, it's a good idea to shrink the filesystem a bit more than our intended size, as specifying a "wrong" end (not the absolute minimum required end for the filesystem) when resizing the partition in `parted` can lead to data loss in the filesystem. So, to be on the safer side, if our intended size for the filesystem is 100G, we want to resize it to 99G for now, then move on to resizing the partition to be make it 100G, and then resize the filesystem again to occupy the remaining space in the partition.

1. Enter `parted` (GNU Parted) interactive mode for the disk device:

    ```sh
    (root) parted /dev/sdX
    ```

2. Now, use the resizepart command to set the new end for the partition.
    ```sh
    (parted) resizepart <partition_number> <new_end>
    ```
    - `new_end` can be specified in `s` (512-byte sectors), `B` (bytes), `MiB`, `GiB` etc. To determine the `partition_number`, use the `print` command to get details for the disk device. Also run `unit s` to see the size of partitions in sectors.

    - In the case of shrinking, it's safer to specify `new_end` in **512-byte** sectors. To calculate the number of sectors for the `new_size`, we can use the following formula:

        ```
        new_size_in_sectors = new_size (GiB) x 1024 x 1024 x 2
        ```

        Then, the `new_end` in sectors will be: `start_of_the_partition + new_size_in_sectors`
    

        Example: If the partition starts at `2048s` and the `new_size_in_sectors` is 209175200s (100 GiB), then the `new_end` is:

        ```
        2048s + 209175200s = 209177248s
        ```

3. If we've shrinked the filesystem a bit more than intended in step 2, we should now run the following:

    ```sh
    (root) resize2fs /dev/sdXY
    ```
    For Btrfs: (needed to be mounted first with option `subvol=/`)

    ```sh
    (root) btrfs filesystem resize max <path_to_mountpoint>/
    ```

    - `path_to_mountpoint` is where the btrfs partition is mounted.
