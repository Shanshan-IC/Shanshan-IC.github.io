---
layout: post
title: Irrlicht Tutroial 1 Hello World
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to set up IDE for suing Irrlicht Engine. Let's start with "Hello World".

include the header file, and use irr namespace

{% highlight C++%}
#include <irrlicht.h>
using namespace irr;
{% endhighlight %}

To use the Irrlicht .DLL file, we need to link with the Irrrlicht.lib, you could do it easily in Visual Studio Property Linker, or you could do the following steps:

{% highlight C++%}
#ifdef _IRR_WINDOWS_
#pragma comment(lib, "Irrlicht.lib")
#pragma comment(linker, "/subsystem:windows /ENTRY:mainCRTStartup")
#endif
{% endhighlight %}

Then it's our main part.

We create a device.

{% highlight C++%}
/* use EDT_SOFTWARE as device type, windows size is (640, 480), amount of color bits per pixel is 16. */
IrrlichtDevice *device =
        createDevice( video::EDT_SOFTWARE, dimension2d<u32>(640, 480), 16,
            false, false, false, 0);

if (!device)
        return 1;
{% endhighlight %}



