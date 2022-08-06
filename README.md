# How to setup JavaFX with Eclipse on Mac M1

## Install OpenJDK 11 for Mac M1
1. Download the JDK from <a href="https://bell-sw.com/pages/downloads/#/java-11-lts" target="_blank">Bellsoft - Liberica Standard JDK 11</a>.
2. After running the installer, it will be installed in `/Library/Java/JavaVirtualMachines/liberica-jdk-11.jdk`.

## Configure JAVA_HOME and PATH_TO_FX
1. Open the file `~/.zshrc`
2. At the end add the following lines:
```
# Java home settings for Java 11 version
JAVA_HOME=$(/usr/libexec/java_home -v11)
export JAVA_HOME

# JavaFX settings
PATH_TO_FX=/Library/Java/JavaFX/javafx-sdk-18.0.2/lib
export PATH_TO_FX

PATH="${JAVA_HOME}/bin:${PATH}"
export PATH
```
3. Save the file.
4. Reload the environment settings with the command:
```
source ~/.zshrc
```
5. Test the Java installation with the commands:
```
echo $JAVA_HOME
echo $PATH_TO_FX
java -version
javac -version
```

## Install JavaFX
1. Download the JavaFX SDK and docs from <a href="https://gluonhq.com/products/javafx" target="_blank">Gluon JavaFX</a> or via <a href="https://openjfx.io" target="_blank">Open JavaFX</a>.
2. Install the SDK into the folder `/Library/Java/JavaFX/javafx-sdk-18.0.2`.
3. Install the docs into the folder `/Library/Java/JavaFX/javafx-18.0.2-javadoc`.
4. Execute the following command to correct the rights on the folders:
```
sudo chown -R root /Library/Java/JavaFX
```
## Install e(fx)clipse 3.8.0 in Eclipse
1. Open Eclipse Market Place.
2. Search for `fx`.
3. Install "e(fx)clipse 3.8.0".

## Configure JDK 11 in Eclipse
1. Open Eclipse.
2. In Settings go to Java > Installed JREs.
3. Add a new Standard VM.
4. Set JRE Home to `/Library/Java/JavaVirtualMachines/liberica-jdk-11.jdk/Contents/Home`
5. Set JRE Name to `JDK [Liberica 11.0.16]`.
6. Add the external JAR `/Library/Java/JavaVirtualMachines/liberica-jdk-11.jdk/Contents/Home/lib/jrt-fs.jar`.
7. Finish.

## Configure User Library JavaFX in Eclipse
1. Open Eclipse.
2. In Settings go to Java > Build Path > User Libraries.
3. Add a new user library `JavaFX [18.0.2]`. Do **not** check the option `system library (added to the boot class path)`.
4. Add all the JARs in the the folder `/Library/Java/JavaFX/javafx-sdk-18.0.2/lib`.

See:
- YouTube - <a href="https://www.youtube.com/watch?v=mUbORGu-z6Q" target="_blank">How to add JavaFX to Eclipse (the easy way!)</a>
- Pragmatic Ways - <a href="https://pragmaticways.com/how-to-add-javafx-to-eclipse-the-easy-way" target="_blank">How to add JavaFX to Eclipse (the easy way)</a>

## Create a new JavaFX project
1. In Eclipse: File > New > Other...
2. Select JavaFX > JavaFX Project.
3. Set the project name.
4. Set Use a project specific JRE to `JDK [Liberica 11.0.16]`.
5. Do **not** check the Module option `Create module-info.java file`.
6. Next
7. Open the Libraries tab.
8. Select `Modulepath` and add the user library `JavaFX [18.0.2]`.

Run the application. Nothing seems to happen.

9. Open the Run Configurations.
10. Open the tab Arguments.
11. Add the following VM Arguments
```
--module-path /Library/Java/JavaFX/javafx-sdk-18.0.2/lib --add-modules javafx.controls,javafx.fxml
```
12. Do **not** check the option `Use the -XstartOnFirstThread argument when launching with SWT`.

Run the application again and a blank window is shown.
