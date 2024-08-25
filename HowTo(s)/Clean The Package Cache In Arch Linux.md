1. First, check how many cached packages are available in my cache folder.

    ```sh
    $ sudo ls /var/cache/pacman/pkg/ | wc -l
    ```

2. Now, let me check the total disk space used by the cache folder.

    ```sh
    $ du -sh /var/cache/pacman/pkg/
    ```

3. To clean all packages, except the 3 most recent versions, run the following command:

    ```sh
    $ sudo paccache -r
    ```

4. Let me check again how many packages are left in the cache folder.

    ```sh
    $ sudo ls /var/cache/pacman/pkg/ | wc -l
    ```

5. Now, check the total disk space used by the cache folder.

    ```sh
    $ du -sh /var/cache/pacman/pkg/
    ```

6. Still want to remove more packages? Of course, you can! Paccache allows you to decide how many recent versions you want to keep. For instance, run the following command if you want to keep only one most recent version:

    ```sh
    $ sudo paccache -rk 1
    ```

    Where, `k` indicates to keep number of each package in the cache.

7. To remove all cached versions of uninstalled packages, re-run paccache with u flag:

    ```sh
    $ sudo paccache -ruk0
    ```

    Where, `u` flag indicates the uninstalled packages.

8. You can also use the following pacman command to remove all uninstalled packages:

    ```sh
    $ sudo pacman -Sc
    ```

9. To completely remove all packages (whether they are installed or uninstalled) from the cache, run the following command:

    ```sh
    $ sudo pacman -Scc
    ```

    Please be careful while using this command. There is no way to retrieve the cached packages once they are deleted.

10. Last method is to go to the `Pamac` GUI and click the "Three Horizontal Bars" or "Three Vertical Dots" icon, Click `Preference` and enter password. Now,

    - To clean package cache:
In the `General` tab, go all the way down to `Cache` segment and set `Number of versions of each package to keep` to `0`. This will reveal the amount of all cache packages stored in the system.

    - To clean build package cache:
Head to `AUR` tab. In the `Build Directory` options, the amount of all build package cache is shown.

### Automatically clean package cache in Arch Linux

If you are too lazy to clean the package cache manually, you can automate this task using pacman hook. It will automatically clean the package cache after every pacman transaction.
To do so.....

1. Create file `/etc/pacman.d/hooks/clean_package_cache.hook` :

    ```sh
    $ sudo mkdir /etc/pacman.d/hooks

    $ sudo nano /etc/pacman.d/hooks/clean_package_cache.hook
    ```

2. Add the following lines:

    ```sh
    [Trigger]
    Operation = Remove
    Type = Package
    Target = *

    [Action]
    Description = Cleaning pacman cache...
    When = PostTransaction
    Exec = /usr/bin/paccache -r
    ```

3. Save and close the file. From now on, the package cache will be cleaned automatically after every 
transactions (like upgrade, install, remove). You don't have to run `paccache` command manually every time.

For more details, refer the `Paccache` help section by running the following command:

```sh
$ paccache -h
```