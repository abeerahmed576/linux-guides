This is for when application don't follow system theme/application style. These steps are for **GTK** apps.

1. Open `/etc/environment` or `/etc/profile` (system-wide) or `~/.profile` (local) in the terminal using a text editor.

2. Add the following line:

    ```sh
    /etc/environment
    ----------------
    GTK_THEME=<The-Current-Theme-Name>
    ```

    ```sh
    /etc/profile ; ~/.profile
    -------------------------
    export GTK_THEME=<The-Current-Theme-Name>
    ```

    To get the theme name, check in the respective GTK style settings of the DE (In KDE, `System Settings --> Appearance  --> Application Style --> Configure GNOME/GTK Application Style`). Any currently installed GTK theme can be applied. They have to be in `/usr/share/themes` or `~/.themes/`

3. Save changes(Ctrl + S) and exit(Ctrl + X).

> Note: According to GNOME devs, this `GTK_THEME` environment variable is only to be used for debugging purposes.

### KDE

GTK Application Style can be configured at `System Settings --> Appearance --> Application Style --> Configure GNOME/GTK Application Style`.

> Note: Some GTK/QT Application running in a root session e.g: `Timeshift` may not follow system setting. Also third-party GTK Styles may not render the best visuals as Breeze. So, it is recommended to keep default GTK theme as Breeze for those apps. Copy `~/.config/gtk-3.0` & `~/.config/gtk-4.0` to `/root/.config/` after setting Breeze as GTK theme:

```sh
sudo cp -r ~/.config/gtk-* /root/.config/
```

GTK apps not following set GTK Application Style in KDE may also be forced following the first three steps mentioned above.