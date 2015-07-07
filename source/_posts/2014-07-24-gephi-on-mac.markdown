---
layout: post
title: "Gephi on OS X Mavericks 10.9"
date: 2014-07-24 12:10:28 +0800
comments: true
categories: Gephi
---

*"Gephi is an open source visualization and exploration platform available on Windows, Linux and Mac OS X. It supports all types of networks – directed, undirected and mixed, and is capable of handling very large network graphs of up to one million nodes. Various metrics are supported including betweenness, closeness, diameter, clustering coefficient, average shortest path, pagerank and HITS. Dynamic filtering allows edges and/or nodes to be selected based on network structure or data. Ideal for social network analysis, link analysis and biological network analysis. Perhaps the most advanced of the open source tools." [<5 Free Social Network Analysis Tools - Butler Analytics>](http://butleranalytics.com/5-free-social-network-analysis-tools/)*

Running OS X Mavericks 10.9.4. I downloaded [Gephi 0.8.2-beta](http://gephi.github.io/users/download/) and it would not load correctly. After starting, it would freeze if I clicked anything. After looking for the solutions on the internet, I found this is a show-stopper for every normal Mac user caused by not supporting JAVA 7(which is installed on updating Mac 10.9) on Gephi. So we need to swich back to JAVA 6, it's really annoying...

Took me almost a day to solve this problem... :( 

This is the steps what I did to fix the problem for running Gephi on Mac OS X 10.9 [@joernhees](https://github.com/joernhees):

1. Download and install JAVA 1.6: [http://support.apple.com/kb/DL1572](http://support.apple.com/kb/DL1572)

2. Delete your gephi settings dir: `rm -r ~/Library/Application\ Support/gephi`

3. Find your java home with `/usr/libexec/java_home -v 1.6`, it should print something like `/System/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home`

4. Edit `/Applications/Gephi.app/Contents/Resources/gephi/etc/gephi.conf` to set your jdkhome e.g. like this: `echo "jdkhome=\"$(/usr/libexec/java_home -v 1.6)\"" >> /Applications/Gephi.app/Contents/Resources/gephi/etc/gephi.conf`

5. Start Gephi and open the Les Miserables sample, if you see the graph good.

6. Check Gephi's about for the line saying Java: 1.6.0_65; Java HotSpot(TM) 64-Bit Server VM 20.65-b04-466.1

<center><img src="https://raw.githubusercontent.com/sumnous/sumnous.github.io/source/source/images/gephi-about.png" width="400" height="600"></center>

Moreover, according to [@Kikohs](https://github.com/kikohs), in your .bash_profile or .zshrc, add:

```vim
# JAVA,
# Your java 6 version here
export JAVA_HOME=/Library/Java/JavaVirtualMachines/1.6.0_51-b11-457.jdk/Contents/Home

function setjdk() {
    if [ $# -ne 0 ]; then
        removeFromPath '/System/Library/Frameworks/JavaVM.framework/Home/bin'
        if [ -n "${JAVA_HOME+x}" ]; then
            removeFromPath $JAVA_HOME
        fi
        export JAVA_HOME=`/usr/libexec/java_home -v $@`
        export PATH=$JAVA_HOME/bin:$PATH
    fi
    echo JAVA_HOME set to $JAVA_HOME
    java -version
}
function removeFromPath() {
    export PATH=$(echo $PATH | sed -E -e "s;:$1;;" -e "s;$1:?;;")
}
```

Those functions allow you to quickly switch for java 6 to java 7 and vice-versa:

```vim
$> setjdk 1.6  # java 6
$> setjdk 1.7  # java 7
```
Attached a picture of [American College football](http://networkdata.ics.uci.edu/data.php?id=5) Network I drawed using Gephi :P

<center><img src="https://raw.githubusercontent.com/sumnous/sumnous.github.io/source/source/images/football_generate.png"></center>


*Reference:* 
1. [About the ISSUE on Gephi](https://github.com/gephi/gephi/issues/748)
2. [Discussions on Gephi forums](https://forum.gephi.org/viewtopic.php?f=24&t=3034&start=20)

