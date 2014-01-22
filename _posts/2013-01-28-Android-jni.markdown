---
layout: post
title:  "Android JNI"
date:   2013-01-28 15:47:34
categories: Android JNI
---


JNINativeMethod struct
----------------------

{% highlight c %}
typedef struct {
const char* name;
const char* signature;
void* fnPtr;
} JNINativeMethod;
{% endhighlight %}


name: java function name
signature: use a string description function's parameter and return type
fnPtr: a function pointer point to native function, it's first add (void *)

How to write the second paramter?
---------------------------------

{% highlight c %}
static JNINativeMethod methods[] = {
{ "_setDataSource", "(Ljava/lang/String;[Ljava/lang/String;[Ljava/lang/String;)V", (void *)android_media_MediaPlayer_setDataSourceAndHeaders },
{ "setDataSource", "(Ljava/io/FileDescriptor;)V", (void *)android_media_MediaPlayer_setDataSourceFD },
};
{% endhighlight %}

* () express jni function paramter and back express return value(V: void Function())
* Primitive types

![Screenshot_from_2013-01-28_14_27_12.png]({{ site.url }}/images/Screenshot_from_2013-01-28_14_27_12.png)



* Reference types

![Screenshot_from_2013-01-28_14_46_52.png]({{ site.url }}/images/Screenshot_from_2013-01-28_14_46_52.png)

object type: To the beginning of the "L", ";" at the end, in the middle is "/" separated
array type: To the beginning of the "["
