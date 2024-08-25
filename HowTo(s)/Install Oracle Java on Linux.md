1. Download the latest JDK from the official site.
2. Open the terminal and enter the following command:

    ```sh
    ~ sudo mkdir /usr/lib/jvm
    ```

3. Extract the `jdk-Xuxx-linux-xXX.tar.gz` file in that directory using this commands:

    ```sh
    ~ cd /usr/lib/jvm
    ~ sudo tar -xvzf ~/Downloads/jdk-Xuxx-linux-xXX.tar.gz
    ```

4. Enter the following command to open the environment variables file:

    ```sh
    ~ sudo nano /etc/environment
    ```

5. In the opened file, add the following bin folder location to the existing `PATH` variable, starting with a colon(':'):

    `/usr/lib/jvm/jdk-XX/bin`

    Colon seperates the locations defined in the `PATH` variable. If the environment file is empty, use the following `PATH` variable definition to avoid potenially breaking the system:

    `PATH="$PATH:/usr/lib/jvm/jdk-XX/bin"`

6. Add the following environment variables at the end of the file:

    `JAVA_HOME="/usr/lib/jvm/jdk-XX"`

    Save changes and close nano. (Ctrl + O and Ctrl + X)

    ### For Debian-based Distros(7-9)

7. Enter the following commands to inform the system about the Java's location. Depending on your JDK version, the paths can be different.

    ```sh
    ~ sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-XX/bin/java" 0

    ~ sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk-XX/bin/javac" 0

    ~ sudo update-alternatives --set java /usr/lib/jvm/jdk-XX/bin/java

    ~ sudo update-alternatives --set javac /usr/lib/jvm/jdk-XX/bin/javac
    ```

8. To verify the setup enter the following commands and make sure that they print the location of `java` and `javac` as you have provided in the previous step:

    ```sh
    ~ update-alternatives --list java

    ~ update-alternatives --list javac
    ```

9. Restart the computer (or just log-out and login) and open the terminal again to check if Java is properly installed:

    ```sh
    ~ java -version
    ```

If you get the installed Java version as the output, you have successfully installed the Oracle JDK in your system. 

------
For Manjaro, Install `java-runtime-common` from AUR for `archlinux-java` usability. 

- To see installed jdks: 

    ```sh
    ~ archlinux-java status
    ```

- To set an available jdk as default:

    ```sh
    ~ archlinux-java set jdk-XXX
    ```