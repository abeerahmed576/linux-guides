# Install Avro on Manjaro Linux

### Related Resources:
- https://medium.com/@sashraf94/installing-ibus-avro-on-arch-distros-arch-manjaro-for-newbies-6a73a2839f66
- https://arinbasu.medium.com/how-to-set-up-bengali-language-writing-in-archlinux-using-openbox-2a3169306947
- https://wiki.archlinux.org/title/IBus


## First thing : Install Pamac
```
sudo pacman -Syu pamac
```

## Enabling AUR

```
sudo pacman -Syu yaourt
```

## Now to Avro

Search for **ibus-avro-git**, it’ll be displayed in AUR repos. Build it.

## Enabling ibus-avro

1. From Start menu, type "IBus Preferences" and hit Enter key. You will be prompt to start IBus Deamon. Start it.
2. A new icon "EN" will appear on the Taskbar.
3. Press Right click on that button and select "Preferences".
4. There are 4 tabs, General, Input Method, Emoji and Advanced.
5. Click on "Input Method".
6. From Right hand side, click on "+Add" button, input method select list will appear.
7. Click on Bangla and "Bengali - Avro Phonetic" will appear under "Bengali".
8. Add Avro as input method.

## Autostart Avro Daemon every time I start my PC

1. Open "Session and Startup" from Start menu. Choose "Application Autostart" tab and click on "Add" button.
2. "Add application" form will appear. Write "ibus" in "Name:" field and "ibus-daemon" in "Command:" field. Now, press OK button.

Watch this video for details: https://www.youtube.com/watch?v=4MGO7uNi2rY

# FOR MANJARO KDE


- Create a file named, **ibus.sh** in **~/.config/autostart** folder with the following lines. Save and close.
- Click Start menu, choose System Settings > Startup and Shutdown > Autostart > Script File. Add ibus.sh script file to be executed in startup.

```
#!/usr/bin/env bash
exec ibus-daemon -drx
```

add the following line to **.profile** file:
```
ibus-daemon -drx
```

It will run ibus daemon all the time.
