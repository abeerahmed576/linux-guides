## Convert PDF to Image

> The package `poppler` is needed to be installed if not already.

1. Open Konsole/Terminal.
2. `cd` to the same directory of the PDF.
3. Use the following command:

```sh
~ pdftoppm -jpeg document.pdf document
```

Here, the command essentially tells the app to convert the file called `document.pdf` into a file called `document` (The extension of the image file will be automatically given). We can also change it to `-png` if we prefer that as our output file. We should use the full form `jpeg` instead of just `jpg`.

## Clean MBR of a Disk

```sh
(root) dd if=/dev/zero of=/dev/sda bs=512 count=1
```

`/dev/sda` is the target storage disk.

## Mount an ISO in Linux CLI

```sh
(root) mount -o loop /path/to/iso /mn
```

## Setting locale to English in Linux

Open `/etc/locale.conf` with sudo nano. Then set `LANG` value to `en_US.UTF-8`.

> Note: If only `LANG` variable is set, the value of it will also be set to other locales like `LC_TIME`, `LC_ADDRESS` etc.
Other locales will have to be set seperately if different from `LANG` value.
