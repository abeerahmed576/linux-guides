- Icons = `~/.local/share/icons/` & `/usr/share/icons/`

- Window Decoration = `~/.local/share/aurorae/themes/` & `/usr/share/aurorae/themes/`

- Colors/Color Scheme = `~/.local/share/color-schemes/` & `/usr/share/color-schemes/`

- Konsole Color Scheme = `~/.local/share/konsole/`

- Plasma Style = `~/.local/share/plasma/desktoptheme/` & `/usr/share/plasma/desktoptheme/`

- Splash Screen = `~/.local/share/plasma/look-and-feel/` & `/usr/share/plasma/look-and-feel/`

- Global Theme = `~/.local/share/plasma/look-and-feel/` & `/usr/share/plasma/look-and-feel/`

- Plasmoids/Widgets = `~/.local/share/plasma/plasmoids/` & `/usr/share/plasma/plasmoids/`

    > Note: `ksysguard` package is required for the `Netspeed` Widget (By Hessijames) to work.

    > Note: To manually install a widget, Just extract the `.plasmoid` file and copy the contents to this path. The name of the folder containing the widget files has to be the same as `X-KDE-PluginInfo-Name` in `metadata.desktop` file of the widget.

- SDDM = `/usr/share/sddm/themes/`

    > Note:
    > - Applying Plasma Settings on **SDDM** in System Settings is easier. However, to manually change settings like font, font-size, theme, cursor theme, edit the `/etc/sddm.conf.d/kde_settings.conf` or `/usr/share/sddm/themes/breeze/theme.conf.user` file (Assuming `breeze` is the currently applied SDDM theme). See `theme.conf` file in the same folder for reference.
    >
    > - If trying to change wallpaper of **SDDM** from System Settings but the changes are not being applied, then copy the desired wallpaper to `/usr/share/sddm/themes/breeze` (Assuming `breeze` is the currently applied SDDM theme). Then open the auto-generated `theme.conf.user` file (If doesn't exist, open `System Settings` and load a different SDDM wallpaper and apply changes) and set `background` value to the file name of the desired wallpaper.]

- Kvantum = `~/.config/Kvantum/` & `/usr/share/Kvantum/`

- Cursor Icon = `~/.icons/` & `/usr/share/icons/`

- GTK Application Style = `~/.themes/` & `/usr/share/themes/`

    > Note:
    > - For GTK application style, only `gtk-3.0` and `gtk-4.0` folders are needed. Copy these two folders from the downloaded GTK theme, go to the mentioned location, create a folder with any name and paste those folders.
    > 
    > - Some GTK/QT apps running with root priviledges may not render the best visuals with a third-party GTK Styles or not follow set style at all, e.g: `Timeshift`, `Grub Customizer`. For those, setting the `Breeze` Style with preferred color scheme, dark mode preference is a workaround. To permanently set `Breeze` for them, `System Settings --> Apperance --> Application Style --> Configure GNOME/GTK Application Style` --> Select `Breeze` and apply. Then copy `~/.config/gtk-3.0` & `~/.config/gtk-4.0` to `/root/.config/` :
    > 
    >   ```sh
    >   ~ sudo cp -r ~/.config/gtk-* /root/.config/
    >   ```
    >
    >   Then apply the desired GTK style for other GTK apps.

    > Random Note for `Timeshift`: Timeshift uses the files `/etc/lsb-release`, `/etc/os-release` files to determine the label for a snapshot/backup.

- KWin Scripts = `~/.local/share/kwin/scripts/`

    > Note: The folder name containing the Kwin scripts files has to be in all small letters.

- Wallpapers = `~/.local/share/wallpapers` & `/usr/share/wallpapers/` & `/usr/local/share/wallpapers/`

    > Note: The Desired Screen Lock wallpaper has to be in `/usr/share/wallpapers/` or `/usr/local/share/wallpapers`


