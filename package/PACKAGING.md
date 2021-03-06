# 🎁 Santulator Packaging

If you'd like to build an installable bundle of Santulator for Mac, Linux or Windows, just like those you can find on the [Santulator download page](https://santulator.github.io/download/) then follow these instructions.  These installers are self-contained files that have everything the user will need to run Santulator without the need to, for example, install Java separately.

## Preparing your Build Environment

### JDK 11

You will need to install JDK 11 to build the installable bundle of Santulator.  The version provided by [AdoptOpenJDK](https://adoptopenjdk.net/) is an excellent choice for this.

### OpenJFX 11

Get the JavaFX 11 JMOD files from [the Gluon download page](https://gluonhq.com/products/javafx/).  Choose the right option for your platform.  For example, for Linux pick the file listed as "JavaFX Linux jmods".  Unzip the file and save the resulting directory somewhere on your system.

### Java Packager

Download the Java Packager.  Choose the right link for your platform from those listed [on this page](https://mail.openjdk.java.net/pipermail/openjfx-dev/2018-September/022500.html).  For Mac and Linux, unpack the zip file store the directory somewhere on your system.  For Windows, copy the two files into the following directories:

| File               | Destination Directory |
|--------------------|-----------------------|
| `jpackager.exe`    | `%JAVA_HOME%\bin`     |
| `jdk.packager.jar` | `%JAVA_HOME%\jmods`   |

### Windows: Inno Setup

The Windows build procedure requires [Inno Setup](http://www.jrsoftware.org/isdl.php).  Download and install this software on your PC.

### Windows: Extra DLLs

You need the files `MSVCP140.dll` & `VCRUNTIME140.dll` installed in `C:\Windows\System32`.  To do this, simply download and install [`vc_redist.x64.exe` from Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=48145).

For some background on this, see [issue #5](https://github.com/Santulator/Santulator/issues/5).

## Creating the Installable Bundle

### Mac & Linux: Creating the Bundle

Assuming that you have installed the JMOD files you downloaded in the above section "[OpenJFX 11](#openjfx-11)" into `/opt/java-modules/javafx-jmods-11` and the [Java Packager](#java-packager) into `/opt/jpackager-11/`, you can run the following command to create the installable bundle:
~~~
$ ./gradlew clean createBundle -PjavafxJmodsPath=/opt/java-modules/javafx-jmods-11 -PjavaPackagerPath=/opt/jpackager-11
~~~

You will find the created installable bundle in the directory `package/build/bundle`.

### Windows: Creating the Bundle

#### Windows: Running the Java Packager

Assuming that you have installed the JMOD files you downloaded in the above section "[OpenJFX 11](#openjfx-11)" into `C:\javafx-jmods-11`, you can run the following command to create the installable bundle:

~~~
gradlew clean -PjavafxJmodsPath=C:\javafx-jmods-11 createBundle
~~~

#### Windows: Running Inno Setup

When you run Java Packager as described in the previous step, you will see a line such as the following near the end of the console output:

~~~
Inno Setup file: C:\repositories\Santulator\package\build\resources\main\application.iss
~~~

Open this file in Inno Setup.  Go to the "Build" menu and select "Compile".  Once this has completed you will find a directory `Output` at the same level as the `application.iss` file containing the Windows Installation bundle.

## Using the Java Packager with JDK 11

[![Using the Java Packager with JDK 11](/assets/Using-The-Java-Packager-With-JDK-11.png)][Using the Java Packager with JDK 11]

For more general information about the approach taken to building the installable bundles for Mac, Linux and Windows and how you could apply this in your own project, see the article [Using the Java Packager with JDK 11].

## Return to Santulator README

[Click here](../README.md) to return to the main Santulator README file for more information about the project.

[Using the Java Packager with JDK 11]:https://medium.com/@adam_carroll/java-packager-with-jdk11-31b3d620f4a8
