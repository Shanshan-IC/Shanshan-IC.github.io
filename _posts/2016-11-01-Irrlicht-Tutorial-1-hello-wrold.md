---
layout: post
title: Irrlicht Tutroial 1 Hello World
categories : Irrlicht
tags : CPP Irrlicht Graphics
---

* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to set up IDE for suing Irrlicht Engine. Let's start with "Hello World".

include the header file, and use irr namespace

```cpp
#include <irrlicht.h>
using namespace irr;
```

To use the Irrlicht .DLL file, we need to link with the Irrrlicht.lib, you could do it easily in Visual Studio Property Linker, or you could do the following steps:

```cpp
#ifdef _IRR_WINDOWS_
#pragma comment(lib, "Irrlicht.lib")
#pragma comment(linker, "/subsystem:windows /ENTRY:mainCRTStartup")
#endif
```

Then it's our main part.

We create a device.

```cpp
/* use EDT_SOFTWARE as device type, windows size is (640, 480), amount of color bits per pixel is 16. */
IrrlichtDevice *device =
    createDevice( video::EDT_SOFTWARE, dimension2d<u32>(640, 480), 16,
            false, false, false, 0);
if (!device)
    return 1;
```

Set the caption of the windows

```cpp
device->setWindowCaption(L"Hello World! - Irrlicht Engine Demo");
```

Get a pointer to the VideoDriver, the SceneManager and the graphical user interface environment

```cpp
IVideoDriver* driver = device->getVideoDriver();
ISceneManager* smgr = device->getSceneManager();
IGUIEnvironment* guienv = device->getGUIEnvironment();
```

Add a hello world label to the window, using the GUI environment. The text is placed at the position (10,10) as top left corner and (260,22) as lower right corner.

```cpp
guienv->addStaticText(L"Hello World! This is the Irrlicht Software renderer!", rect<s32>(10,10,260,22), true);
```

In order to get interesting, we use the mesh from the scene manager and then add a scenenode to display it with addAnimatedMeshSceneNode(). In the mean time, check it.

```cpp
IAnimatedMesh* mesh = smgr->getMesh("../../media/sydney.md2");
if (!mesh)
{
    device->drop();
    return 1;    
}
IAnimatedMeshSceneNode* node = smgr->addAnimatedMeshSceneNode( mesh );
```

Change its material to make it nicer, We disable lighting because we do not have a dynamic light in here, and the mesh would be totally black otherwise. Then we set the frame loop, such that the predefined STAND animation is used. And last, we apply a texture to the mesh. 

```cpp
if (node) {
	node -> setMaterialFlag(EMF_LIGHTING, false);
	node -> setMD2Animation(scene::EMAT_STAND);
	node->setMaterialTexture( 0, driver->getTexture("../../media/sydney.bmp") );
}
```

Place a camera into the position (0, 30, -40), target is at (0,5,0)

```cpp
smgr -> addCameraSceneNode(0, vector3df(0, 30, -40), vector3df(0, 5, 0))
```

Let's draw Everything.

```cpp
while(device->run()) {
	driver -> beginScene(true, true, SColor(255, 100, 101, 140));
	smgr -> drawAll();
	guienv -> drawAll();
	driver -> endScene();
}
```

After we are done, we have to delete the Device and every object you created.

```cpp
device -> drop();
return 0;
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/01.HelloWorld)
