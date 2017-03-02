---
layout: post
title: "Irrlicht Tutroial 08 Special Effects"
categories : Irrlicht
tags : CPP Irrlicht Graphics
---
* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to use stencil buffer shadows, the particle system, billboards, dynamic light, and the water surface scene node. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

Special effect 1: Water surface and hill plan mesh 
```cpp
mesh = smgr->addHillPlaneMesh( "myHill",
    core::dimension2d<f32>(20,20),
    core::dimension2d<u32>(40,40), 0, 0,
    core::dimension2d<f32>(0,0),
    core::dimension2d<f32>(10,10));
node = smgr->addWaterSurfaceSceneNode(mesh->getMesh(0), 3.0f, 300.0f, 30.0f);
node->setPosition(core::vector3df(0,7,0));
node->setMaterialTexture(0, driver->getTexture("../../media/stones.jpg"));
node->setMaterialTexture(1, driver->getTexture("../../media/water.jpg"));
node->setMaterialType(video::EMT_REFLECTION_2_LAYER);
```
Add a lightnode, and make it flying, and attach billboard
```cpp
node = smgr->addLightSceneNode(0, core::vector3df(0,0,0),
    video::SColorf(1.0f, 0.6f, 0.7f, 1.0f), 800.0f);
scene::ISceneNodeAnimator* anim = 0;
anim = smgr->createFlyCircleAnimator (core::vector3df(0,150,0),250.0f);
node->addAnimator(anim);
anim->drop();
node = smgr->addBillboardSceneNode(node, core::dimension2d<f32>(50, 50));
node->setMaterialFlag(video::EMF_LIGHTING, false);
node->setMaterialType(video::EMT_TRANSPARENT_ADD_COLOR);
node->setMaterialTexture(0, driver->getTexture("../../media/particlewhite.bmp"));
```
set a nice material to the particle system, we have a cool looking camp fire. 
```cpp
scene::IParticleSystemSceneNode* ps = smgr->addParticleSystemSceneNode(false);
scene::IParticleEmitter* em = ps->createBoxEmitter(
    core::aabbox3d<f32>(-7,0,-7,7,1,7), // emitter size
    core::vector3df(0.0f,0.06f,0.0f),   // initial direction
    80,100,                             // emit rate
    video::SColor(0,255,255,255),       // darkest color
    video::SColor(0,255,255,255),       // brightest color
    800,2000,0,                         // min and max age, angle
    core::dimension2df(10.f,10.f),         // min size
    core::dimension2df(20.f,20.f));        // max size

ps->setEmitter(em); // this grabs the emitter
em->drop(); // so we can drop it here without deleting it

scene::IParticleAffector* paf = ps->createFadeOutParticleAffector();

ps->addAffector(paf); // same goes for the affector
paf->drop();
ps->setPosition(core::vector3df(-70,60,40));
ps->setScale(core::vector3df(2,2,2));
ps->setMaterialFlag(video::EMF_LIGHTING, false);
ps->setMaterialFlag(video::EMF_ZWRITE_ENABLE, false);
ps->setMaterialTexture(0, driver->getTexture("../../media/fire.bmp"));
ps->setMaterialType(video::EMT_TRANSPARENT_ADD_COLOR);
```
 add a volumetric light node, which adds a glowing fake area light to the scene.
```cpp
scene::IVolumeLightSceneNode * n = smgr->addVolumeLightSceneNode(0, -1,
            32,                              // Subdivisions on U axis
            32,                              // Subdivisions on V axis
            video::SColor(0, 255, 255, 255), // foot color
            video::SColor(0, 0, 0, 0));      // tail color

if (n)
{
    n->setScale(core::vector3df(56.0f, 56.0f, 56.0f));
    n->setPosition(core::vector3df(-120,50,40));

    // load textures for animation
    core::array<video::ITexture*> textures;
    for (s32 g=7; g > 0; --g)
    {
        core::stringc tmp;
        tmp = "../../media/portal";
        tmp += g;
        tmp += ".bmp";
        video::ITexture* t = driver->getTexture( tmp.c_str() );
        textures.push_back(t);
    }

    // create texture animator
    scene::ISceneNodeAnimator* glow = smgr->createTextureAnimator(textures, 150);

    // add the animator
    n->addAnimator(glow);

    // drop the animator because it was created with a create() function
    glow->drop();
}
```
a dynamic shadow be casted from an animated character.
```cpp
// add animated character

mesh = smgr->getMesh("../../media/dwarf.x");
scene::IAnimatedMeshSceneNode* anode = 0;

anode = smgr->addAnimatedMeshSceneNode(mesh);
anode->setPosition(core::vector3df(-50,20,-60));
anode->setAnimationSpeed(15);

// add shadow
anode->addShadowVolumeSceneNode();
smgr->setShadowColor(video::SColor(150,0,0,0));

// make the model a little bit bigger and normalize its normals
// because of the scaling, for correct lighting
anode->setScale(core::vector3df(2,2,2));
anode->setMaterialFlag(video::EMF_NORMALIZE_NORMALS, true);
```
You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/08.SpecialFX