### AUR package fails to verify PGP/GPG key: "unknown public key", "One or more PGP signatures could not be verified!"

If you get:

```sh
llvm-5.0.1.src.tar.xz … FAILED (unknown public key 8F0871F202119294)
```

then:

```sh
~ gpg --recv-key 8F0871F202119294
```

and try again. Enter the key ID as appropriate.

Detail:

Many AUR packages contain lines to enable validating downloaded packages though the use of a PGP key. This establishes a level of trust between the software author and anyone who downloads the software - if you trust the key, and the download validates against the key, then you can trust the download.

Pacman has its own keyring for system packages in the repos. This means pacman will trust Manjaro and Arch packager keys. Your user starts with an empty keyring. That is, you trust no one’s keys. When you run makepkg you run it as your normal user, so if the PKGBUILD file contains a PGP key validation will fail because you don’t trust the key - you have to import the key into your keyring first.
 
This is easy. Open a terminal and type:

```sh
~ gpg --recv-key $KEYID
```

where `$KEYID` is the ID of the key you want to import.

Now when you run makepkg (directly or via your AUR helper) the downloaded file will be validated and all will be well.
If validation still fails then the file is either invalid or the keyserver cannot locate the key. With the recent issues with the default keyserver, some keys cannot be found and you may have to try other servers. A few examples are:

```
pgp.mit.edu
keyserver.pgp.com
keys.openpgp.org
```

To try a different server, you’ll use the `--keyserver` flag. Example:

```sh
~ gpg --keyserver pgp.mit.edu --recv-key 8F0871F202119294
```
