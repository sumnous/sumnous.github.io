---
layout: post
title: "Install Octave on Mac OS X 10.9"
date: 2014-07-13 10:10:28 +0800
comments: true
categories: Octave
---
Recently I am working on Stanford Machine Learning Course By Andrew NG on Coursera, Andrew recommended Octave to build prototype quickly. It's been tricky to install octave on Mac, so I shared my process of intalling it. 

 
1.Install [XQuartz](https://xquartz.macosforge.org/landing/)

2.Install Xcode and Command Line Tools3

```vim
$ xcode-select --install
```
		
3.Install [homebrew](https://github.com/Homebrew/homebrew/wiki/installation)

```vim
$ brew doctor
$ brew update && brew upgrade
```

It's important to solve all the warning in homebrew, so it can work smoothly when installing octave.
		
4.Import the scientific computing packages

```vim
$ brew tap homebrew/science
```
		
5.Install Octave

```vim
$ brew install octave
```
		
6.Install gnuplot

```vim
$ brew install gnuplot
```
	
(Update: As phseven pointed out, gnuplot will be automatically installed with octave, but in some cases it won’t support X11.) For such cases, do the following:

```vim		
$ brew uninstall gnuplot
$ brew install gnuplot --with-x
```

If you plot something in Octave, and it occures problems like this:

```vim	
gnuplot> set terminal aqua enhanced title "Figure 1"  font "*,6" dashlength 1
	           			^	        	             
	    line 0: unknown or ambiguous terminal type; type just 'set terminal' for a list
```     
	
Just run:
		
```vim
setenv("GNUTERM","X11")
```
	
befor you plot anything, e.g.,
	
```vim
plot(x,y)
```
	
It will be convenient if you setup Octave startup file: `vim ~/.octaverc` and add the line `setenv GNUTERM x11`.
	
7.Open Octave just run `octave`, if you want to change the look of your Octave, just input `PS1('>> ')`

```vim
octave:1>
octave:1> PS1('>> ')
>>
>>
```
<!--more-->	
	
*Reference: [http://jatinganhotra.com/blog/2014/01/21/installing-octave-on-os-x-10-dot-9-mavericks/](http://jatinganhotra.com/blog/2014/01/21/installing-octave-on-os-x-10-dot-9-mavericks/)*


