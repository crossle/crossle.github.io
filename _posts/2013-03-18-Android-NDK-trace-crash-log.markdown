---
layout: post
title:  "Android NDK trace crash log"
date:   2013-03-18 18:47:34
categories: Android NDK
---

ndk-stack
-------

`ndk-stack` is a simple tool that allows you to filter stack traces, trace the crash code quickly

adb logcat log:

{% highlight bash %}
    I/DEBUG   (   31): *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
    I/DEBUG   (   31): Build fingerprint: 'generic/google_sdk/generic/:2.2/FRF91/43546:eng/test-keys'
    I/DEBUG   (   31): pid: 351, tid: 351  %gt;%gt;%gt; /data/local/ndk-tests/crasher <<<
    I/DEBUG   (   31): signal 11 (SIGSEGV), fault addr 0d9f00d8
    I/DEBUG   (   31):  r0 0000af88  r1 0000a008  r2 baadf00d  r3 0d9f00d8
    I/DEBUG   (   31):  r4 00000004  r5 0000a008  r6 0000af88  r7 00013c44
    I/DEBUG   (   31):  r8 00000000  r9 00000000  10 00000000  fp 00000000
    I/DEBUG   (   31):  ip 0000959c  sp be956cc8  lr 00008403  pc 0000841e  cpsr 60000030
    I/DEBUG   (   31):          #00  pc 0000841e  /data/local/ndk-tests/crasher
    I/DEBUG   (   31):          #01  pc 000083fe  /data/local/ndk-tests/crasher
    I/DEBUG   (   31):          #02  pc 000083f6  /data/local/ndk-tests/crasher
    I/DEBUG   (   31):          #03  pc 000191ac  /system/lib/libc.so
    I/DEBUG   (   31):          #04  pc 000083ea  /data/local/ndk-tests/crasher
    I/DEBUG   (   31):          #05  pc 00008458  /data/local/ndk-tests/crasher
    I/DEBUG   (   31):          #06  pc 0000d362  /system/lib/libc.so
    I/DEBUG   (   31):
{% endhighlight %}

ndk-trace crash log
-------------------

{% highlight bash %}
    Build fingerprint: 'generic/google_sdk/generic/:2.2/FRF91/43546:eng/test-keys'
    pid: 351, tid: 351  >>> /data/local/ndk-tests/crasher <<<
    signal 11 (SIGSEGV), fault addr 0d9f00d8
    Stack frame #00  pc 0000841e  /data/local/ndk-tests/crasher : Routine zoo in /tmp/foo/crasher/jni/zoo.c:13
    Stack frame #01  pc 000083fe  /data/local/ndk-tests/crasher : Routine bar in /tmp/foo/crasher/jni/bar.c:5
    Stack frame #02  pc 000083f6  /data/local/ndk-tests/crasher : Routine my_comparison in /tmp/foo/crasher/jni/foo.c:9
    Stack frame #03  pc 000191ac  /system/lib/libc.so
    Stack frame #04  pc 000083ea  /data/local/ndk-tests/crasher : Routine foo in /tmp/foo/crasher/jni/foo.c:14
    Stack frame #05  pc 00008458  /data/local/ndk-tests/crasher : Routine main in /tmp/foo/crasher/jni/main.c:19
    Stack frame #06  pc 0000d362  /system/lib/libc.so
{% endhighlight %}

Usage:

`adb logcat | $NDK/ndk-stack -sym $PROJECT_PATH/obj/local/armeabi`

Addr2line
---------

addr2line is a tool for translates addresses into file names and line numbers.

Usage:

`addr2line -f -e /a/b/c/d.so 0007d89`

