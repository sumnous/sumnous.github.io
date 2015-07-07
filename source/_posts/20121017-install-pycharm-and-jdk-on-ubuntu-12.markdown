---
layout: post
title: "Install PyCharm and JDK on Ubuntu 12.04"
date: 2012-10-17 15:48:29 +0800
comments: true
categories: [JDK, PyCharm, Ubuntu]
---

###Installing Sun JDK 7 on Ubuntu 12.04:


+ Download the sun jdk 7 tar file [from here](http://www.oracle.com/technetwork/java/javase/downloads/jdk7u7-downloads-1836413.html)

+ Extract the tar file:

```python
$ tar -xvzf jdk-7u4-linux-x64.tar.gz
```

+ Move extracted folder to this location:

```
$ sudo mv jdk1.7.0_04 /usr/lib/jvm/
```

+ Install new java source in system: 
	
```
$ sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.7.0_04/bin/javac 1 
$ sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.7.0_04/bin/java 1 
$ sudo update-alternatives --install /usr/bin/javaws javaws /usr/lib/jvm/jdk1.7.0_04/bin/javaws 1
```
<!--more-->

+ Choose default java:

```
$ sudo update-alternatives --config javac 
$ sudo update-alternatives --config java 
$ sudo update-alternatives --config javaws
```

+ java version test:

```
$ java -version
```

+ Verify the symlinks all point to the new java location:

```
$ ls -la /etc/alternatives/java*
```

+ Enable Java plugin for Mozilla Firefox (even for Chrome)
		
```
#for 64-Bit jdk 
$ sudo ln -s /usr/lib/jvm/jdk1.7.0_04/jre/lib/amd64/libnpjp2.so /usr/lib/mozilla/plugins 
#for 32-Bit jdk 
$ sudo ln -s /usr/lib/jvm/jdk1.7.0_04/jre/lib/i386/libnpjp2.so /usr/lib/mozilla/plugins
```

+ JAVA_HOME configuration:

     Some tools require JAVA_HOME variable. You can set JAVA_HOME in Ubuntu so simple: Edit the file .bashrc under your home directory and add the following lines: (if .bashrc is hidden click in Nautilus Menu View > Show Hidden Files)

```
export JAVA_HOME=/path/your/jdk 
export PATH=$JAVA_HOME/bin:$PATH
```

###Install pycharm on ubuntu 12.04:

+ Download pycharm-2.6.2.tar.gz [from here](http://download.jetbrains.com/python/pycharm-2.6.2.tar.gz)

```
$ tar -xvzf pycharm-2.6.2.tar.gz 
$ cd /pycharm-2.6.2/bin/ 
$ ./pycharm.sh &
```

