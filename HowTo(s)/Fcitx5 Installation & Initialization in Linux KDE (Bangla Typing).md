## Required Packages:
1. `fcitx5`
2. `fcitx5-configtool`
3. `fcitx5-qt`
4. `fcitx5-gtk`
5. `fcitx5-openbangla-git`
6. `openbangla-keyboard-git`

## Setup:

1. In KDE, go to S`ystem Settings -> Regional Settings -> Input Method`.
2. Click `Add Input Method`. Then select `OpenBangla Keyboard` and add then `Apply`.

## Setting environment variables:

The following environment variables needs to be defined in order for **Fcitx5** to work in GUI apps. These can be set in either `/etc/environment`, `/etc/xprofile` (Xorg), `~/.xprofile` (Xorg), `/etc/systemd/system/user@.service.d/fcitx5SetUp.conf` (Wayland) or `~/.config/environment.d/envvars.conf` (Wayland). But `/etc/environment` is not recommended as this one may get overwritten after a system upgrade.

```sh
~/.xprofile; /etc/xprofile (For Xorg session)
---------------------------------------------
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
export XMODIFIERS=@im=fcitx5
```

```sh
~/.config/environment.d/envvars.conf (For Wayland session)
----------------------------------------------------------
GTK_IM_MODULE=fcitx5
QT_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx5
```

```sh
/etc/systemd/system/user@.service.d/fcitx5SetUp.conf (For Wayland Session)
--------------------------------------------------------------------------
[Service]
Environment="GTK_IM_MODULE=fcitx5"
Environment="QT_IM_MODULE=fcitx5"
Environment="XMODIFIERS=@im=fcitx5"
```

```sh
/etc/environment
-----------------
GTK_IM_MODULE=fcitx5
QT_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx5
```

## Autostart
In KDE, Fcitx5 automatically starts upon logging in, so no need to bother with autostarting.