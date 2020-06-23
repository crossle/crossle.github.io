---
layout: post
title: "adb shell dumpsys"
date: 2013-03-07 15:47:34
---

## adb shell dumpsys

adb shell dumpsys is a command that dumps interesting system state to the log.

{% highlight bash %}
\$ adb shell dumpsys | grep DUMP
DUMP OF SERVICE SurfaceFlinger:
DUMP OF SERVICE accessibility:
DUMP OF SERVICE account:
DUMP OF SERVICE activity:
DUMP OF SERVICE alarm:
DUMP OF SERVICE appwidget:
DUMP OF SERVICE audio:
DUMP OF SERVICE backup
...
{% endhighlight %}

You can dump the info to log, cpuinfo meminfo activity …
e.g. dump meminfo for VPlayer apk

{% highlight bash %}

    $ adb shell dumpsys meminfo 'me.abitno.vplayer.t'
    Applications Memory Usage (kB):
    Uptime: 63530153 Realtime: 99233241

    ** MEMINFO in pid 4592 [me.abitno.vplayer.t] **
                             Shared  Private     Heap     Heap     Heap
                       Pss    Dirty    Dirty     Size    Alloc     Free
                    ------   ------   ------   ------   ------   ------
           Native        0        0        0     3576     3549       14
           Dalvik     4705    10472     4496    10312    10096      216
           Cursor        2        4        0
           Ashmem        0        0        0
        Other dev    12933     3172     7404
         .so mmap      858     1848      496
        .jar mmap        0        0        0
        .apk mmap       99        0        0
        .ttf mmap        5        0        0
        .dex mmap        0        0        0
       Other mmap      381       16       32
          Unknown     2620      652     2612
            TOTAL    21603    16164    15040    13888    13645      230

     Objects
                   Views:      172         ViewRootImpl:        1
             AppContexts:        4           Activities:        1
                  Assets:        2        AssetManagers:        2
           Local Binders:       31        Proxy Binders:       26
        Death Recipients:        1
         OpenSSL Sockets:        0

{% endhighlight %}

## How to look for the help?

use argument -h to look for the help (e.g.adb shell dumpsys xxx -h)
I wanna check the service for VPlayer apk

{% highlight  bash %}
\$ adb shell dumpsys activity s | grep me.abitno.vplayer.t
_ ServiceRecord{42220f60 u0 me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService}
intent={cmp=me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService}
packageName=me.abitno.vplayer.t
processName=me.abitno.vplayer.t:vplayer
baseDir=/data/app/me.abitno.vplayer.t-2.apk
dataDir=/data/data/me.abitno.vplayer.t
app=ProcessRecord{41fd8060 4664:me.abitno.vplayer.t:vplayer/u0a10063}
intent={cmp=me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService}
_ Client AppBindRecord{422cee00 ProcessRecord{41fd8060 4664:me.abitno.vplayer.t:vplayer/u0a10063}}
ConnectionRecord{422ceea0 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService:@41f91e78}
ConnectionRecord{422ceea0 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService:@41f91e78}
_ ServiceRecord{42842348 u0 me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService}
intent={cmp=me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService}
packageName=me.abitno.vplayer.t
processName=me.abitno.vplayer.t:vplayer
baseDir=/data/app/me.abitno.vplayer.t-2.apk
dataDir=/data/data/me.abitno.vplayer.t
app=ProcessRecord{41fd8060 4664:me.abitno.vplayer.t:vplayer/u0a10063}
intent={cmp=me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService}
_ Client AppBindRecord{41c4d038 ProcessRecord{41e1d140 4592:me.abitno.vplayer.t/u0a10063}}
ConnectionRecord{41c36700 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService:@41e5d778}
ConnectionRecord{41c36700 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService:@41e5d778}
_ ConnectionRecord{422ceea0 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService:@41f91e78}
binding=AppBindRecord{422cee00 me.abitno.vplayer.t/me.abitno.vplayer.VPlayerService:me.abitno.vplayer.t:vplayer}
_ ConnectionRecord{41c36700 u0 CR me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService:@41e5d778}
binding=AppBindRecord{41c4d038 me.abitno.vplayer.t/me.abitno.vplayer.RemoteVPlayerService:me.abitno.vplayer.t}
activity=ActivityRecord{4218da70 u0 me.abitno.vplayer.t/me.abitno.media.explorer.FileExplorerContainer}
{% endhighlight %}

dumpsys source code locate `https://android.googlesource.com/platform/frameworks/native/+/master/cmds`
dumpstate is a tool dumps the current system state to stdout, it's a full info.
