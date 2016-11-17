---
layout: post
title: Irrlicht Tutroial 13 Loading Scenes from irr Files
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to save and load the full scene graph into an .irr file, an xml based format. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

load the scene from .irr file
{% highlight C++ %}
// load the scene
if (argc>1)
    smgr->loadScene(argv[1]);
else
    smgr->loadScene("../../media/example.irr");
{% endhighlight %}
Find all the scene inside, and create triangel selectors
{% highlight C++ %}
// Create a meta triangle selector to hold several triangle selectors.
scene::IMetaTriangleSelector * meta = smgr->createMetaTriangleSelector();
core::array<scene::ISceneNode *> nodes;
smgr->getSceneNodesFromType(scene::ESNT_ANY, nodes); // Find all nodes
for (u32 i=0; i < nodes.size(); ++i)
{
    scene::ISceneNode * node = nodes[i];
    scene::ITriangleSelector * selector = 0;

    switch(node->getType())
    {
    case scene::ESNT_CUBE:
    case scene::ESNT_ANIMATED_MESH:
        /* Because the selector won't animate with the mesh, and is only being used for camera collision, we'll just use an approximate bounding box */
        selector = smgr->createTriangleSelectorFromBoundingBox(node);
    break;

    case scene::ESNT_MESH:
    case scene::ESNT_SPHERE: // Derived from IMeshSceneNode
        selector = smgr->createTriangleSelector(((scene::IMeshSceneNode*)node)->getMesh(), node);
        break;

    case scene::ESNT_TERRAIN:
        selector = smgr->createTerrainTriangleSelector((scene::ITerrainSceneNode*)node);
        break;

    case scene::ESNT_OCTREE:
        selector = smgr->createOctreeTriangleSelector(((scene::IMeshSceneNode*)node)->getMesh(), node);
        break;

    default:
        // Don't create a selector for this node type
        break;
    }

    if(selector)
    {
        // Add it to the meta selector, which will take a reference to it
        meta->addTriangleSelector(selector);
        // And drop my reference to it, so that the meta selector owns it.
        selector->drop();
    }
}
{% endhighlight %}
Now that the mesh scene nodes have had triangle selectors created and added to the meta selector, create a collision response animator from that meta selector.
{% highlight C++ %}
scene::ISceneNodeAnimator* anim = smgr->createCollisionResponseAnimator(
    meta, camera, core::vector3df(5,5,5),
    core::vector3df(0,0,0));
meta->drop(); 
camera->addAnimator(anim);
anim->drop();
// And set the camera position so that it doesn't start off stuck in the geometry
camera->setPosition(core::vector3df(0.f, 20.f, 0.f));
// Point the camera at the cube node, by finding the first node of type ESNT_CUBE
scene::ISceneNode * cube = smgr->getSceneNodeFromType(scene::ESNT_CUBE);
if(cube)
    camera->setTarget(cube->getAbsolutePosition());
{% endhighlight %}
You can get the complete codes from [Github](https://github.com/Shanshan-IC/irrlicht/tree/master/examples/15.LoadIrrFile)