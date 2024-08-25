**systemd-boot** is a simple UEFI bootloader with minimalism. Unlike **GRUB**, it provides a simple textual menu to select boot options and no customization options whatsoever. But it is great as a barebone and lightweight bootloader for a linux installation. It only supports machines with UEFI supported motherboard.

## Installing Systemd-Boot

Steps to install systemd-boot slightly differ in the case of a running linux installation from a `chroot` (eg. new installation or fixing the bootloader from a live iso). Installing from a `chroot` requires some extra steps for the installation to be bootable.

systemd-boot comes part of the **systemd** init system. So, no extra packages are needed to be installed to enable systemd-boot in our installation.

To install systemd-boot:

```sh
(root) bootctl install
```

By default, systemd-boot will install itself in **ESP** (EFI System Partition) with the same mountpoint defined in `/etc/fstab`. To see the mount point of ESP systemd-boot picked up:

```sh
$ bootctl -p
```

```sh
$ bootctl -x # This shows where systemd will look for the linux and initramsfs images. If there is no seperate /boot partition with "XBOOTLDR partition (Extended Boot)" partition type, this defaults to the ESP partition
```

## Configuring Systemd-Boot

Unlike GRUB, systemd-boot doesn't automatically create entries for it pointing to the linux and initramfs images. Also for systemd-boot to be able to reach the linux and initramfs images, they need to be in the same ESP partition as systemd-boot is installed in or in a seperate `/boot` partition with **XBOOTLDR partition (Extended Bootloader Partition)** (`ea00` for gdisk) partition type. If not automated, the images are needed to be manually placed in the directories for systemd-boot everytime there is a kernel or microcode update. To automate this process, we have to use the "kernel-install" program, packaged with systemd, which installs or removes linux and initramfs images to the required partitions and automatically creates boot entries for systemd-boot.

If in a running linux installation:

```sh
(root) kernel-install add <KERNEL_VERSION> /usr/lib/modules/<KERNEL_VERSION>/vmlinuz

or,

(root) kernel-install add
```

`kernel-install` puts the images at the root of the ESP or XBOOTLDR partition in this folder structure: `<MACHINE-ID>/<KERNEL-VERSION>/`

To get the `KERNEL_VERISON`, we can look into `/usr/lib/modules`. Every installed kernel should have a corresponding folder in this directory and the folder names are normally the version of the kernel. We can also run `uname -r` to get version of the currently running kernel.

If installing from a `chroot`, run the first `kernel-install` command explicitly mentioning the kernel version. Because `kernel-install add` will fail as it automatically picks up the `KERNEL_VERSION` of the live iso's kernel which may not be the same as the kernel installed in `/usr/lib/modules`.

At this point, for a running linux installation, we are basically set. We can edit in `ESP/loader/loader.conf` to set the timeout, default boot entry etc according to our needs. But for a chroot installation, we have to do some go through some extra steps to have a bootable linux installation.

1. After the `kernel-install` command successfully runs, open `ESP/<MACHINE-ID>/<KERNEL-VERSION>/<auto-gened-entry>.conf` with a text-editor (`/boot/<MACHINE-ID>/<KERNEL-VERSION>/<auto-gened-entry>.conf` if installed with XBOOTLDR partiton):

    ```sh
    (root) nano <auto-gened-entry>.conf
    ```

2. In the `options` line, we have to replace everything before `systemd.machind_id` with following kernel options:

    `root=/dev/sdXY rw`

    Where `/dev/sdXY` is the `/` directory of our linux installation. We can also append options like `quiet`, `splash` or `loglevel=3` if we want here. After necessary insertions, save and exit.

    For the `root` option, it is a better idea to use the UUID of the `/` partition. But in a chroot environment, it might be a little difficult to copy-paste the UUID, so we will do this after successfully booting into our installation.

Done. Our linux installation is bootable with systemd-boot now.

If we have kernel options that we want to boot with, we can define them `/etc/kernel/cmdline`. `kernel-install` automatically fetches our desired options from here and appends them in the `.conf` file everytime the command is issued. After successfully booting into our linux installation, open `/etc/kernel/cmdline` with a text editor: (will be automatically created if non-existent)
```sh
(root) nano /etc/kernel/cmdline
```

Before this, we want to fetch the UUID of the `/` partition and assign it to the root option from before. To do that:

```sh
(root) blkid /dev/sdXY
```

This will output various details for our `/` partition. We just want to copy the `UUID="<random_string>"` and use it in cmdline:

`root=UUID="<random_string>" rw quiet loglevel=3 systemd.machine_id=<MACHINE_ID>`

`MACHINE_ID` can be fetched from `/etc/machine-id`.

## Automation

Unfortunately, systemd-boot won't be updated in the ESP directory automatically after a systemd update. Although it's not a mandatory task, it is a good idea to update systemd-boot in the ESP. Luckily, systemd provides a service file to take care of this process after an update. To enable that:
```sh
(root) systemctl enable systemd-boot-update.service
```

It can also be done with a pacman hook:

```sh
/etc/pacman.d/hooks/95-systemd-boot.hook

[Trigger]
Type = Package
Operation = Upgrade
Target = systemd

[Action]
Description = Gracefully upgrading systemd-boot...
When = PostTransaction
Exec = /usr/bin/systemctl restart systemd-boot-update.service
```

`kernel-install` process also needs to be automated for a kernel install/update. For this, two AUR packages can be used: `pacman-hook-kernel-install` (by eNV25) and `kernel-install-mkinitcpio` (by dalto@endeavouros). `kernel-install-mkinitcpio` also prompts `mkinitcpio` to create fallback initramfs image which `pacman-hook-kernel-install` doesn't (It's the default behaviour of `kernel-install` and this package simply issues it after an update)

There are two pacman hooks provided by mkinitcpio package in Arch which automatically generates the initramfs after a kernel install/update and puts them in /boot. For our systemd-boot installation, the images put in /boot are basically useless (except the microcode images `*-ucode.img`). So, we may want to mask those pacman hooks by running the following commands:

```sh
(root) ln -s /dev/null /etc/pacman.d/hooks/60-mkinitcpio-remove.hook
(root) ln -s /dev/null /etc/pacman.d/hooks/90-mkinitcpio-install.hook
```

The hooks are originally in `/usr/share/libalpm/hooks` . We are putting two empty links with the same name of those hooks in `/etc/pacman.d/hooks` as configuration files put in `/etc` takes precedence in Linux.

With these steps, the `kernel-install` is now automated.