---
published: true
title: install Oracle Java JDK 8 on CentOS
layout: post
---
First thing first:

    yum update

search for if any older JDK versions are installed:

    rpm -qa | grep -E '^open[jre|jdk]|j[re|dk]'

sample output:

    gobject-introspection-1.36.0-4.el7.x86_64
    pygobject3-base-3.8.2-4.el7.x86_64


check the already installed Java version:

    java -version

If Java 1.6 or 1.7 have been installed already, you can uninstall them:

    yum remove java-1.6.0-openjdk
    yum remove java-1.7.0-openjdk

### Download And Install Oracle Java JDK

At the time I write this JDK version is JDK 8u101 change version to latest as you read this. 

Go to the Oracle [Java download page](http://www.oracle.com/technetwork/java/javase/downloads/index.html) and download the required version ( I use 64bit CentOS 6 server, I have downloaded the 64bit rpm package ) 

run the following command to install it:

    rpm -ivh jdk-8u101-linux-x64.rpm

Sample output:

    Preparing...                          ################################# [100%]
    Updating / installing...
       1:jdk1.8.0_101-2000:1.8.0_25-fcs    ########################### [100%]
    Unpacking JAR files...
        rt.jar...
        jsse.jar...
        charsets.jar...
        tools.jar...
        localedata.jar...
        jfxrt.jar...

### Check Java version

Check for the installed JDK version in your system using command:

    java -version

Sample output:

    java version "1.8.0_101"
    Java(TM) SE Runtime Environment (build 1.8.0_101-b17)
    Java HotSpot(TM) 64-Bit Server VM (build 101.101-b02, mixed mode)

### Setup Global Environment Variables

Create a file called ```java.sh``` under ```/etc/profile.d/``` directory

    vim /etc/profile.d/java.sh

Add the following lines:

    #!/bin/bash
    JAVA_HOME=/usr/java/jdk1.8.0_25/
    PATH=$JAVA_HOME/bin:$PATH
    export PATH JAVA_HOME
    export CLASSPATH=.

Save and close the file. Make it executable using command:

    chmod +x /etc/profile.d/java.sh
    source /etc/profile.d/java.sh

That’s all.