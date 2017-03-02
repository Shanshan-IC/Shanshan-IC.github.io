---
layout: post
title: "Irrlicht Tutroial 11 Terrain Rendering"
categories : Irrlicht
tags : CPP Irrlicht Graphics
---

* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to use the terrain renderer. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

the Terrain Renderer in Irrlicht is based on Spintz' GeoMipMapSceneNode
```cpp
// add terrain scene node
scene::ITerrainSceneNode* terrain = smgr->addTerrainSceneNode(
"../../media/terrain-heightmap.bmp",
0,                  // parent node
-1,                 // node id
core::vector3df(0.f, 0.f, 0.f),     // position
core::vector3df(0.f, 0.f, 0.f),     // rotation
core::vector3df(40.f, 4.4f, 40.f),  // scale
video::SColor ( 255, 255, 255, 255 ),   // vertexColor
5,                  // maxLOD
scene::ETPS_17,             // patchSize
4                   // smoothFactor
);

terrain->setMaterialFlag(video::EMF_LIGHTING, false);
terrain->setMaterialTexture(0,
driver->getTexture("../../media/terrain-texture.jpg"));
terrain->setMaterialTexture(1,
driver->getTexture("../../media/detailmap3.jpg"));
terrain->setMaterialType(video::EMT_DETAIL_MAP);
terrain->scaleTexture(1.0f, 20.0f);
```
To be able to do collision with the terrain, we create a triangle selector. 
```cpp
// create triangle selector for the terrain 
scene::ITriangleSelector* selector = smgr->createTerrainTriangleSelector(terrain, 0);
terrain->setTriangleSelector(selector);

// create collision response animator and attach it to the camera
scene::ISceneNodeAnimator* anim = smgr->createCollisionResponseAnimator(
selector, camera, core::vector3df(60,100,60),
core::vector3df(0,0,0),
core::vector3df(0,50,0));
selector->drop();
camera->addAnimator(anim);
anim->drop();
```
Add skybox and skydome for switching the modes
```cpp
// create skybox and skydome
driver->setTextureCreationFlag(video::ETCF_CREATE_MIP_MAPS, false);
scene::ISceneNode* skybox=smgr->addSkyBoxSceneNode(
    driver->getTexture("../../media/irrlicht2_up.jpg"),
    driver->getTexture("../../media/irrlicht2_dn.jpg"),
    driver->getTexture("../../media/irrlicht2_lf.jpg"),
    driver->getTexture("../../media/irrlicht2_rt.jpg"),
    driver->getTexture("../../media/irrlicht2_ft.jpg"),
    driver->getTexture("../../media/irrlicht2_bk.jpg"));
scene::ISceneNode* skydome=smgr->addSkyDomeSceneNode(driver->getTexture("../../media/skydome.jpg"),16,8,0.95f,2.0f);

driver->setTextureCreationFlag(video::ETCF_CREATE_MIP_MAPS, true);

// create event receiver
MyEventReceiver receiver(terrain, skybox, skydome);
device->setEventReceiver(&receiver);
```
You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/12.TerrainRendering)