#DevelopersGuideWindows
*Developers guide for Windows. Updated Aug 23, 2012 by frost.g...@gmail.com*

##Aparapi Developer Guide: Microsoft® Windows® 32- and 64-bit platforms

##SVN Client

To contribute to Aparapi you will need an SVN client to access the latest source code.

This page lists a number of SVN client providers http://subversion.apache.org/packages.html

For Microsoft Windows® users TortoiseSVN incorporates SVN functionality directly into Windows Explorer view and is often preferred http://tortoisesvn.tigris.org/

Also you might want to consider one of the SVN-based plugins for Eclipse. http://wiki.eclipse.org/SVN_Howto
Oracle® Java JDK install (JDK1.6 or later)

http://www.oracle.com/technetwork/java/javase/downloads/index.html

The Oracle® J2SE JDK site contains downloads and documentation showing how to install for various platforms. http://www.oracle.com/technetwork/java/javase/index-137561.html

When the installation is complete, ensure that your JAVA_HOME environment variable is pointing to the install location (such as c:\progra~1\java\jdk1.6.0_26)and that %JAVA_HOME%\bin is in your path.

    C:> set JAVA_HOME=c:\progra~1\java\jdk1.6.0_26
    C:> set PATH=%PATH%;%JAVA_HOME%\bin

Note that we tend to use the 8.3 form of Microsoft® Windows® path variables this avoids us having to quote paths in scripts.

Double check your path and ensure that there is not another JDK/JRE in your path.

    C:> java -version
    java version "1.6.0_26"
    Java(TM) SE Runtime Environment (build 1.6.0_26-b03)
    Java HotSpot(TM) Client VM (build 20.1-b02, mixed mode, sharing)

##Apache Ant

Apache Ant™ can be downloaded from the apache project page http://ant.apache.org

Aparapi has been tested using 1.7.1 version of Ant, it may well work with earlier versions, but if you encounter issues we recommend updating to at least 1.7.1 before reporting issues. Installation is straightforward, just unzip the ant.zip file and ensure that your ANT_HOME}} environment variable is pointing to your ANT installation and that `{{{%ANT_HOME%\bin` is in your path.

    C:> set ANT_HOME=C:\progra~1\apache\apache-ant-1.8.1
    C:> set PATH=%PATH%;%ANT_HOME%\bin

Double check the installation and environment vars.

    ant -version
    Apache Ant version 1.7.1 compiled ..

##AMD APP SDK

To compile Aparapi JNI code you need access to OpenCL headers and libraries. The instructions below assume that there is an available AMD APP SDK v2.5 (or later) installed and that your platform supports the required device drivers for your GPU card. Install the Catalyst driver first, and then install AMD APP SDK v2.5.

See http://developer.amd.com/sdks/AMDAPPSDK/pages/DriverCompatibility.aspx for help locating the appropriate driver for your AMD card. Be sure you obtain the catalyst driver that includes the OpenCL™ runtime components.

    The OpenCL™ runtime is required for executing Aparapi or OpenCL™ on your CPU or GPU, but it is not necessary for building/compiling Aparapi.
    The AMD APP SDK v2.5 is necessary for compiling the Aparapi JNI code against OpenCL™ APIs.

Once you have a suitable driver, download a copy of AMD APP SDK v2.5 from http://developer.amd.com/sdks/AMDAPPSDK/downloads/Pages/default.aspx.

Download the installation guide for Microsoft® Windows® (and Linux®) from http://developer.amd.com/sdks/AMDAPPSDK/assets/AMD_APP_SDK_Installation_Notes.pdf. Note that if you updating from a previous version of AMD APP SDK (or its predecessor ATI STREAM SDK), first uninstall the previous version. The release notes are available here http://developer.amd.com/sdks/AMDAPPSDK/assets/AMD_APP_SDK_Release_Notes_Developer.pdf
##A C++ compiler

For Microsoft® Windows® platforms the JNI build can support either Microsoft® Visual Studio® 2008, 2009 or 2010 compiler or MinGW (Minimal GNU for Windows) from GNU. Now that Visual Studio express is available for free, we would recommend using Visual studio. If you wish to use another compiler then you will have to tweak the com.amd.aparapi.jni/build.xml file to get your compiler to work.
Microsoft® Visual Studio® 2008/2010 for 32-bit or 64-bit platforms

Aparapi has been tested with various versions of Microsoft® Visual Studio® 2008, 2009 and 2010 including Enterprise, Professional and Express editions, if you encounter any version specific issues please let us know so we can address it and/or update this documentation.

If you already have Microsoft® Visual Studio® installed you will need to know the location of the compiler and the SDK. These can vary depending upon the platform and version you are using. Typically an install results in a Visual Studio install, such as. c:\Program Files\Microsoft Visual Studio 9.0

And an SDK, such as. c:\Program Files\Microsoft SDKs\Windows\v6.0A

Note the location of both of these as this information will be needed to configure the com.amd.aparapi.jni\build.property file (later).
For Visual Studio Express 64 bit users

Visual studio express does not include the 64 bit compiler or libraries. You will need to also install the SDK from Microsoft. this link should help
##MinGW – (MINimum Gnu for Windows)

As an alternative to installing Microsoft® Visual Studio® we have included support for the MinGW tool chain and Aparapi has been (minimally) tested with this compiler.

MingGW can be downloaded from http://www.mingw.org/ by following the instructions on their Getting Started page. We recommend installing the mingw-get-inst msi installer and just taking the defaults.

Note the install location as this information will be needed to edit build.xml file and uncomment the line referencing the mingw instal dir. Typically the install location is

    C:\MinGW

After a successful build, you will need to ensure that the bin sub directory is in your path before you attempting to run an Aparapi enabled application built using MinGW. MinGW apps require access to MingGW/GNU C++/C runtime at execution time.

    set PATH=%PATH%;C:\MinGW\bin

This is one reason the binary distribution is ''not'' built using mingw.
##JUnit

The initial Open Source drop includes a suite of JUnit tests for validating bytecode to OpenCL code generation. These tests require JUnit 4.

Download JUnit from http://www.junit.org/

Note the location of your JUnit installation; the location is needed to configure the test\codegen\build.xml file. See the UnitTestGuide page for howto configure the JUnit build.
##Eclipse

Eclipse is not required to build Aparapi, however the developers of Aparapi do use Eclipse and have made the Eclipse artifacts (.classpath and .project files) available so that projects can be imported into Eclipse.

The com.amd.aparapi.jni subproject (containing C++ JNI source) should be imported as a resource project, we do not recommend importing com.amd.aparapi.jni as a CDT project, and we do not recommend trying to configure a CDT build, the existing build.xml files has been customized for multiplatform C++ compilations.
##Building

Check out the Aparapi SVN trunk:

svn checkout http://aparapi.googlecode.com/svn/trunk

You will end up with the following files/directories

    aparapi/
       com.amd.aparapi/
          src/java/com.amd.aparapi/*.java
          build.xml
       com.amd.aparapi.jni/
          src/cpp/*.cpp
          src/cpp/*.h
          build.xml
       test/
          codegen/
             src/java/
                com.amd.aparapi/
                com.amd.aparapi.test/
             build.xml
          runtime/
             src/java/
                com.amd.aparapi/
                com.amd.aparapi.test/
             build.xml
       samples/
          mandel
             src/java/com.amd.aparapi.samples.mandel/*.java
             build.xml
             mandel.sh
             mandel.bat
          squares/
             src/java/com.amd.aparapi.samples.squares/*.java
             build.xml
             squares.sh
             squares.bat
          convolution/
             src/java/com.amd.aparapi.samples.convolution/*.java
             build.xml
             conv.sh
             conv.bat
       examples/
          nbody/
             src/java/com.amd.aparapi.nbody/
             build.xml
             nbody.sh
             nbody.bat
       build.xml
       README.txt
       LICENSE.txt
       CREDITS.txt

##Sub Directories

The com.amd.aparapi and com.amd.aparapi.jni subdirectories contain the source for building and using Aparapi.

The ant build.xml file, in each folder accept 'clean' and 'build' targets.

Use the build.xml file at the root of the tree for two purposes:

    To initiate a build of com.amd.aparapi and com.amd.aparapi.jni.
    To create a binary distribution directory and zip file. This zip file is same as those available from the download section of the code.google.com/p/aparapi site.

##Preparing for your first build

You should only need to edit com.amd.aparapi.jni\build.xml file if you wish to use mingw or if you Visual Studio or gcc compiler is in an unusual place.

Perform a build from the root directory using the following command:

    $ ant clean dist

The jni build will perform some simple tests to check the configuration properties and hopefully also guide you to a possible solution.

Once your build has completed you should see an additional subdirectory named dist_windows_x86 or dist_windows_x86_64 (depending upon your platform type).

    aparapi.jar containing Aparapi classes for all platforms.
    the shared library for your platform (aparapi_x86.dll or aparapi_x86_64.dll).
    an /api subdirectory containing the 'public' javadoc for Aparapi.
    a samples directory containing the source and binaries for the mandel and squares sample projects.

The root directory also contains either dist_windows_x86_64.zip or dist_windows_x86.zip containing a compressed archive of the distribution tree.

[Attribution](Attribution.md)
