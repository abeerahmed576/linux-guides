1. Download Noto Sans Bengali from `fonts.google.com`.
2. Extract the downloaded zip.
3. Move the `NotoSansBengali-VariableFont_wdth,wght.ttf` to `/usr/local/share/fonts/` using:

    ```sh
    sudo mv NotoSansBengali-VariableFont_wdth,wght.ttf /usr/local/share/fonts/
    ```

4. Create a file `50-custom-bangla.conf` in `~/.config/fontconfig/conf.d/` (Create the directory if not existing)

5. Paste the following:

    ```xml
    <?xml version="1.0"?>
    <!DOCTYPE fontconfig SYSTEM "fonts.dtd">

    <fontconfig>
      <!-- Bangla (bn/BD) -->
      <match target="font">
        <test name="lang" compare="contains">
          <string>BD</string>
        </test>
        <alias>
          <family>sans-serif</family>
          <prefer>
            <family>Noto Sans Bengali</family>
          </prefer>
        </alias>
      </match>

      <match target="font">
        <test name="lang" compare="contains">
          <string>BD</string>
        </test>
        <alias>
          <family>serif</family>
          <prefer>
            <family>Noto Sans Bengali</family>
          </prefer>
        </alias>
      </match>

      <match target="font">
        <test name="lang" compare="contains">
          <string>BD</string>
        </test>
        <alias>
          <family>monospace</family>
          <prefer>
            <family>Noto Sans Bengali</family>
          </prefer>
        </alias>
      </match>
      <!-- Bangla (bn/BD) End -->
    </fontconfig>
    ```

6. Then, run:

    ```sh
    ~ fc-cache -f -v
    ```
7. Done! Noto Sans Bengali is now installed system-wide.

