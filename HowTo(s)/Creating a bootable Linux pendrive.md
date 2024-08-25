1. Download the ISO and the checksum file.

2. First, verify the checksum:

    ```sh
    ~ sha1sum -c manjaro.iso.sha1
    ```

    It should print a line which says “OK”. Depending on which checksum is provided, you may need to use `sha256sum` or `sha512sum`.
If it’s not okay, it might be a bad download, so download it again.

3. Print out the checksum, we’ll need it later on:

    ```sh
    ~ sha1sum manjaro.iso

    dc7427636040e9469861251858aae820c2ae16cc  manjaro-kde-20.0.3-200606-linux56.iso
    ```

4. Plug in your USB stick. We need to unmount it first if it's mounted:

    ```sh
    ~ sudo umount /dev/sdx
    ```

    Or, unplug and plug USB stick. If it's automatically mounted, change the respective settings.

5. Check the device name it got associated with:

    ```sh
    ~ ls -l /dev/disk/by-id | grep usb
    
    […] usb Flash_USB_Disk_37271228A5E0216322818-0:0 → …/…/XdA
    ```

6. Start the write process with dd:

    ```sh
    ~ sudo dd if=manjaro.iso of=/dev/XdA bs=1M oflag=sync status=progress
    ```

    For old and slow USB2 sticks you can use a lower block size (bs) value like 128K;
for faster sticks you can use 4M.

7. You get a confirmation when the transfer has been finished:

    ```sh
    xxx bytes (yyy MB, zzz MiB) copied, ... s, ... MB/s
    ```

8. Now you can check whether the file has been correctly copied to the stick:

    ```sh
    ~sudo dd if=/dev/XdA iflag=count_bytes count=xxx | sha1sum
    ```

    Adjust the count parameter `xxx` to represent the number of bytes written which you
get from the confirmation above in point 7.

    ```sh
    xxx bytes (yyy MB, zzz MiB) copied, ... s, ... MB/s
    dc7427636040e9469861251858aae820c2ae16cc
    ```

9. Compare the checksum with the one you got in step 3, if they match, you’re good to go!