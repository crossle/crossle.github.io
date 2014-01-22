---
layout: post
title:  "How to use android.os.SystemProperites"
date:   2013-02-27 15:47:34
categories: Android
---

What's SystemProperies?
-----------------------

SystemProperties is gives access to the system properties store. The system properties store contains a list of string key-value pairs. It's very nice, but marked `hide`, we can't use it!

You can use `adb shell getprop` print the info if you installed android sdk. In a similar way, use adb shell setprop key value put key-value to systemproperties.

How to use SystemProperties?
---------------------------

By reflection

{% highlight java %}
ClassLoader cl = context.getClassLoader();
Class<?> SystemProperties = cl.loadClass("android.os.SystemProperties");

//Parameters Types
@SuppressWarnings("rawtypes")
Class[] paramTypes = { String.class };
Method get = SystemProperties.getMethod("get", paramTypes);

//Parameters
Object[] params = { key };
String ret = (String) get.invoke(SystemProperties, params);
{% endhighlight %}


Get the source code include your project

  SystemProperites.java be located `AOSP/frameworks/base/core/java/android/os/SystemProperties.java`, Because of invoke jni, so it's trouble.

Use command adb shell getprop

{% highlight java %}
try {
  Process ifc = Runtime.getRuntime().exec("getprop ro.debuggable");
  BufferedReader bis = new BufferedReader(new InputStreamReader(ifc.getInputStream()));
  String line = bis.readLine();
  ifc.destroy();
} catch (java.io.IOException e) {
}
{% endhighlight %}

Conclusion
----------

I think use the reflection is convenience. the full Source [SystemPropertiesProxy](https://gist.github.com/crossle/5046538)

