---
layout: post
title:  "Android apk decompiler"
date:   2013-03-18 15:47:34
categories: Android
---

Tools
----

Android-apktools is a tools reverse engineering 3rd party, closed, binary Android apps.
dex2jar is a tools to work with android .dex and java .class files.
JD-GUI is a standalone graphical utility that displays Java source codes of “.class” files.
You can browse the reconstructed source code with the JD-GUI for instant access to methods and fields.

Decompiler
--------

Decompiler android resouce file use Android-apktools. Download `apktool-install-linux-r05-ibot.tar.bz2`
and `apktool1.5.2.tar.bz2`, unzip to a same folder, run `apktool d -f xxx.apk xxx`.

Decompiler android java file use dex2jar, unzip a classes.dex from apk, run ./d2j-dex2jar.sh classes.dex,
then you will got the file named classes-dex2jar.jar.

Use JD-GUI open classes-dex2jar.jar, you'll say the java source.


