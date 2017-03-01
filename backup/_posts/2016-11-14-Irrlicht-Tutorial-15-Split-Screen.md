---
layout: post
title: Irrlicht Tutroial 15 Split Screen
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to use splitscreen. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

We'll create a viewport divided into 4 parts, with 3 fixed cameras and one user-controlled.
{% highlight C++ %}
//cameras
ICameraSceneNode *camera[4]={0,0,0,0};
// Create 3 fixed and one user-controlled cameras
//Front
camera[0] = smgr->addCameraSceneNode(0, vector3df(50,0,0), vector3df(0,0,0));
//Top
camera[1] = smgr->addCameraSceneNode(0, vector3df(0,50,0), vector3df(0,0,0));
//Left
camera[2] = smgr->addCameraSceneNode(0, vector3df(0,0,50), vector3df(0,0,0));
//User-controlled
camera[3] = smgr->addCameraSceneNodeFPS();
// don't start at sydney's position
if (camera[3])
camera[3]->setPosition(core::vector3df(-50,0,-50));
{% endhighlight %}
In order to split windows, we just need to set to the different camera and view point
{% highlight C++ %}
while(device->run())
{
    //Set the viewpoint to the whole screen and begin scene
    driver->setViewPort(rect<s32>(0,0,ResX,ResY));
    driver->beginScene(true,true,SColor(255,100,100,100));
    if (SplitScreen)
    {
        //Activate camera1
        smgr->setActiveCamera(camera[0]);
        //Set viewpoint to the first quarter (left top)
        driver->setViewPort(rect<s32>(0,0,ResX/2,ResY/2));
        //Draw scene
        smgr->drawAll();
        //Activate camera2
        smgr->setActiveCamera(camera[1]);
        //Set viewpoint to the second quarter (right top)
        driver->setViewPort(rect<s32>(ResX/2,0,ResX,ResY/2));
        //Draw scene
        smgr->drawAll();
        //Activate camera3
        smgr->setActiveCamera(camera[2]);
        //Set viewpoint to the third quarter (left bottom)
        driver->setViewPort(rect<s32>(0,ResY/2,ResX/2,ResY));
        //Draw scene
        smgr->drawAll();
        //Set viewport the last quarter (right bottom)
        driver->setViewPort(rect<s32>(ResX/2,ResY/2,ResX,ResY));
    }
    //Activate camera4
    smgr->setActiveCamera(camera[3]);
    //Draw scene
    smgr->drawAll();
    driver->endScene();
}
device->drop();
{% endhighlight %}
You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/18.SplitScreen)