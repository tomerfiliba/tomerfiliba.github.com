---
layout: recipe-page
title: ctypes - Pointer from Address
---

There are times you need to construct a `ctypes` pointer from an integer address you have, 
say the `id` of a python object. I scratched my head for quite a while until I found out a how 
to do it properly (with some help from the *stackoverflow* guys). Here's what I got:

{% highlight python %}
import ctypes

def deref(addr, typ):
    return ctypes.cast(addr, ctypes.POINTER(typ)).contents
{% endhighlight %}

Example
=======

{% highlight pycon %}
# get the ref count of an object (in a very nasty way :)
>>> x="hello world"
>>> deref(id(x), ctypes.c_int)
c_long(1)
>>> y=x
>>> z=x
>>> deref(id(x), ctypes.c_int)
c_long(3)
{% endhighlight %}

Some words of caution:
* I'm relying here on `id` returning the address of an object. This is a weak assumption, 
  but it holds (and is likely to continue to hold) for CPython. 
* There are APIs for what I showed in the example above... use them instead!

I'm using this code to dig into the vicious 
[OVERLAPPED](http://msdn.microsoft.com/en-us/library/ms684342(v=vs.85%29.aspx) structure that's held 
inside [PyOVERLAPPED](http://docs.activestate.com/activepython/2.4/pywin32/PyOVERLAPPED.html) 
for really low-level hacking... Anyway, if anyone finds this recipe useful, feel free to use it.
