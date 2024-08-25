## Installing Font

1. Download the fonts. Multiple styles of the desired font i.e `Regular`, `Bold`, `Italic`, `Thin`, `Medium` etc. are recommended to download. Both `.ttf` and `.otf` format can be used.

2. Move the fonts to `~/.local/share/fonts/` for local installation or `/usr/local/share/fonts/` for system-wide installation.

3. Clear and regenerate font cache using the following command:

    ```sh
    ~ fc-cache -f -v
    ```

4. Verify the installation using the following command:

    ```sh
    ~ fc-list | grep <font-family-name>
    ```

    Font family name examples: ProductSans, FiraSans, SanFransisco etc. All the font files being installed must be renamed as `<font-family-name> - <font-style>` if not already.

5. Apply the font from System Setting.

## Removing manually installed fonts

1. Identify the paths to the installed fonts by family name using `fc-list` with `grep`:

    ```sh
    ~ fc-list | grep <font-family-name>
    ```

2. Remove target fonts:

    ```sh
    ~ rm "~/.local/share/fonts/ProductSans-*.ttf"
    ```
    
    Assuming the path to the target files is `~/.local/share/fonts/` and the font family name is `ProductSans` and font format is `ttf`.

3. Clear and regenerate font cache:

    ```sh
    ~ fc-cache
    ```

## Setting Terminus as TTY font

Terminus font is one of the best tty/console fonts available for linux. To set Terminus for tty session, follow the steps below.

1. Install `terminus-font`.

    ```sh
    ~ sudo pacman -S terminus-font
    ```

2. Open `/etc/vconsole.conf` with `nano`.

    ```sh
    ~ sudo nano /etc/vconsole.conf
    ```

3. Add the following:

    `FONT=ter-122n`

4. Save the changes(Ctrl + O and Enter) and exit(Ctrl + X).

> Note:
> 1. The above steps set the tty font permanently.
> 
> 2. To see a list of available tty/console font installed, see `/usr/share/kbd/consolefonts/`.