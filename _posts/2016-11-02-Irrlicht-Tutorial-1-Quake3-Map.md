---
layout: post
title: Irrlicht Tutroial 2  Quake 3 map
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to load a Quake 3 map into the engine, to create a scencenode for optimizing and the speed of rendering, and how to create a user controlled camera. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

Like the previous example, We create a device, the difference is that we ask the user to select which video driver to use. You just need to include the <driverChoice.h>

To display the Quake 3 map, we first need to load it. Quake 3 maps are packed into .pk3 files which are nothing else than .zip files. So we add the .pk3 file to our irr::io::IFileSystem. After it was added, we are able to read from the files in that archive as if they are directly stored on the disk.

{% highlight C++%}
device->getFileSystem()->addFileArchive("../../media/map-20kdm2.pk3");
{% endhighlight %}

Now we can load the mesh by calling irr::scene::ISceneManager::getMesh(). We get a pointer returned to an irr::scene::IAnimatedMesh. As you might know, Quake 3 maps are not really animated, they are only a huge chunk of static geometry with some materials attached. Hence the IAnimatedMesh consists of only one frame, so we get the "first frame" of the "animation", which is our quake level and create an Octree scene node with it, using irr::scene::ISceneManager::addOctreeSceneNode(). The Octree optimizes the scene a little bit, trying to draw only geometry which is currently visible. An alternative to the Octree would be a irr::scene::IMeshSceneNode, which would always draw the complete geometry of the mesh, without optimization. 

{% highlight C++%}
IAnimatedMesh* mesh = smgr->getMesh("20kdm2.bsp");
scene::ISceneNode* node = 0;
if (mesh) {
    node = smgr->addOctreeSceneNode(mesh->getMesh(0), 0, -1, 1024);   
}
if (node) {
	node->setPosition(core::vector3df(-1300,-144,-1249));
}
{% endhighlight %}

create a camera which behaves like the ones in first person shooter games (FPS)

{% highlight C++%}
smgr->addCameraSceneNodeFPS();
{% endhighlight %}

The mouse cursor needs not be visible

{% highlight C++%}
device->getCursorControl()->setVisible(false);
{% endhighlight %}

In the end draw Everything.

You can get the complete codes from [Github](https://github.com/Shanshan-IC/irrlicht/tree/master/examples/02.Quake3Map)
