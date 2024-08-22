# Linux Guides on Software Installation, HowTo's

Short guides on various useful software installation, command-line utlities usage and HowTo's  

### Switch to Fastest Mirror

```
sudo pacman-mirrors --fasttrack
```

### Update Manjaro
```
sudo pacman -Syyu
```

### Install AUR package manager
```
sudo pacman -S yaourt
```

### Enabling AUR in Manjaro

![Enable AUR](https://www.fosslinux.com/4278/what-is-aur-and-how-to-enable-it-in-manjaro.htm)

## Install Vim Editor
```
sudo pacman -S vim
```

In case if you get any error while installing the package, try the command below and repeat the previous commands:
```
sudo pacman -Rs vim
```

## TEAMVIEWER

If you encounter an error message saying, **Teamviewer daemon is not running!**, starting its service will suffice. To start the service run the following command in the Terminal:

```
systemctl enable teamviewerd
```

Please notice the service name. It's **teamviewerd**, not "teamviewer".

## GIMP

Install from **Official** Repositories.

## Install XnView Multi Platform

Install from "Add/Remove Software" app using AUR.

## XnView Settings

```
General
	General
	- Startup
		- Uncheck "Open browser"
		- Startup directory: None
		- Mode when starting with a file: Normal
	
Interface
	Keyboard
		Pressing ESC once quits XnViewMP: Always

Browser
	Catalog
		Catalog
			Enable Catalog: Untick
```

## Archive Software (RAR, ZIP, etc)

Open "Add/Remove Software" app and search for "peazip-gtk2" from AUR repository. Build from the search result.
```
peazip-gtk2 (GTK2 archiver utility)
Repository: AUR
size: 20.7 MB
```
# Color Picker

Search "pick-colour-picker" in "Add/Remove Software" having AUR selected. Build the app from the search result.

# Filezilla

Install using "Add/Remove Software".
URL: https://www.fosslinux.com/2421/how-to-install-filezilla-in-manjaro-linux-17-1-gnome.htm

# dflux
"xflux" changes monitor color temperature adaptively to ease eye strain.

### fluxgui
Better lighting for Linux. Open source GUI for xflux.

- From "Start", open "Add/Remove Software" and look for "xflux-gui-git". Build it.
- After completing installation, press Start and look for **f.lux indicator applet**. Click on it. This little app's icon should appear in the panel (like, Windows's taskbar). Right-click on it, and choose Preferences. In this screen, choose your desired color temperature. Finally check the "Autostart f.lux indicator applet" to start automatically when Manjaro starts.

# Nikon RAW .NEF Driver

To open Nikon's RAW .NEF files in GIMP, install a software, "Darktable". It installs a driver that enables .NEF files to be open by GIMP

```
sudo pacman -S darktable
```

## Install traceroute

```
sudo pacman -S traceroute
```

In case if you get any error while installing the package, try the command below and repeat the previous commands
```
sudo pacman -Rs traceroute
```
## Disable Windows Grouping

![Windows Grouping](Panel-Preferences-Items-WindowsButtons-WindowGrouping-Never.jpg)

- Click "Start" button and search for "Panel" and click on it to start panel customization app.
- Select the "Items" tab.
- From the list window, select "Windows Buttons" and edit it.
- Under "Behavior" section, Select "Never" for "Windows Grouping".
- Close the windows all the way down to get out the Penel windows.

## Flameshot (Screenshot Software)

Install **flameshot** from AUR. After installation, run it from "Start". A system tray icon will appear.
Right-click to bring the context menu up and click "Configuration" which bring up its dialog box. Click on "General" tab and check the **Launch at startup** checkbox.

**Assign to PrintScreen Shortcut Key**

- Head to the system settings and navigate your way to the Keyboard settings.
- You will find all the keyboard shortcuts listed there, ignore them and scroll down to the bottom. Now, you will find a + button.
- Click the “+” button to add a custom shortcut. You need to enter the following in the fields you get:
**Name:** Anything You Want
**Command:** /usr/bin/flameshot gui
- Finally, set the shortcut to PrtSc – which will warn you that the default screenshot functionality will be disabled – so proceed doing it.

![Flameshot Keyboard Shortcut Key Assignment](https://github.com/manzurahmed/manjaro-software-installation-guide/blob/master/flameshot-config-default.jpg)

## Switching Kernel

Instead of using the Manjaro Settings Manager GUI to identify, choose, add, and remove kernels everything can be achieved from a terminal as well. 

**Identifying the Kernel Being Used**
This terminal command will give your system's kernel information: 
```
mhwd-kernel -li
```
As an example, once the terminal is opened, the following command will install a new kernel (4.19) **without deleting the existing kernel currently being used**:
```
sudo mhwd-kernel -i linux419
```

### Trimage - Image Compressor

GUI based Image compressor and optimizer. Open "Add/Remove Software" and search "triimage" in AUR. Install and enjoy.

Website: https://trimage.org/

## Install .TTF fonts

Copy all .ttf fonts to /usr/share/fonts/TTF and run the following command from Terminal:
```
fc-cache -vf
```
## KdenLive

Install Kdenlive from **Main** repository. NOT from AUR.

## Google Chrome

1. Open "Add/Remove Software". Make sure you have enabled AUR.
2. Search for "google-chrome" and build to install Chrome.
3. That's it.

# Putty (SSH client)

URL: https://ecuadorminingnews.com/install-putty/

1. Open the terminal. (Ctrl+Alt+T)

2. Enter the following command to the terminal
```
    sudo pacman -S putty
```
3. putty is now installed.

In case if you get any error while installing the package, try the command below and repeat the previous commands
```
    sudo pacman -Rs putty
```

# Koala SASS (.scss) Preprocessor

1. Search "**ruby**" (version 2.7.0.1) in AUR and install it.
2. Ruby also installs "**rvm**" (version 1.29.9.-2).
3. Start **Terminal**. Run this command to install "gconf" package:
```
sudo pacman -S gconf
```
4. Search "**koala-bin**" (version 2.3.0.3) in AUR and install it.

# Zeal

Zeal is an offline documentation browser for software developers.
Install from App store.

Link: https://zealdocs.org/

# OBS Studio (obs-studio)

Official Repositories (community) by Christian Hesse (eworm@archlinux.org)
