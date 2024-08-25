## CMake fails to build AUR/Git Packages

While installing/building AUR/Git Packages, if an error occurs like:

```
CMake Error: CMake was unable to find a build program corresponding to "Unix Makefiles". CMAKE_MAKE_PROGRAM is not set. You probably need to select a different build tool.

CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage
```

Then installing the `base-devel` package is a common fix for Arch based distros.

## Package Database Sync Problem

When getting errors like:

```
Unable to lock database
Failed to synchronise database
```

Do a `sudo pacman -Syy` to force every repository database sync/refresh.

## LibreOffice Theme Fix in KDE

If Toolbar icons does not adjust automatically according to dark theme.

1. Open LibreOffice.
2. In Menu bar, `Select Tools --> Options`.
3. Under `LibreOffice` section, select View and select `Icon Theme`.
4. Here, select any `Dark` theme for proper icons in a dark application theme environment.

If Editor background in LibreOffice is wrong due to set `Color Scheme`:

1. Under LibreOffice section, select `Application Colors`.
2. Set `Application background` to an desired color. For proper dark theme aesthetics, `Dark Grey` is recommended.
