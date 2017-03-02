---
layout: post
title: "Irrlicht Tutroial 12 Render to Texture"
categories : Irrlicht
tags : CPP Irrlicht Graphics
---

* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to render to a texture. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

To test out the render to texture feature, we need to create a render target texture. Note that don't use sizes bigger than the frame buffer for this, because the render target shares the zbuffer with the frame buffer. Because we want to render the scene not from the user camera into the texture, we add another fixed camera to the scene. 
```cpp
// create render target
video::ITexture* rt = 0;
scene::ICameraSceneNode* fixedCam = 0;

if (driver->queryFeature(video::EVDF_RENDER_TO_TARGET))
{
    rt = driver->addRenderTargetTexture(core::dimension2d<u32>(256,256), "RTT1");
    test->setMaterialTexture(0, rt); 

    // add fixed camera
    fixedCam = smgr->addCameraSceneNode(0, core::vector3df(10,10,-80),
        core::vector3df(-10,10,-100));
}
else
{
    // create problem text
    gui::IGUISkin* skin = env->getSkin();
    gui::IGUIFont* font = env->getFont("../../media/fonthaettenschweiler.bmp");
    if (font)
        skin->setFont(font);

    gui::IGUIStaticText* text = env->addStaticText(
        L"Your hardware or this renderer is not able to use the "\
        L"render to texture feature. RTT Disabled.",
        core::rect<s32>(150,20,470,60));

    text->setOverrideColor(video::SColor(100,255,255,255));
}

scene::ICameraSceneNode* fpsCamera = smgr->addCameraSceneNodeFPS();
fpsCamera->setPosition(core::vector3df(-50,50,-150));
device->getCursorControl()->setVisible(false);
```
And in the run loop, set render target texture

driver->setRenderTarget(rt, true, true, video::SColor(0,0,0,255));

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/13.RenderToTexture)