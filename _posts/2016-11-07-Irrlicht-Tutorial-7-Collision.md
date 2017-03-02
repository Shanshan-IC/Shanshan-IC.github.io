---
layout: post
title: "Irrlicht Tutroial 7 Collision"
categories : Irrlicht
tags : CPP Irrlicht Graphics
---

* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show Automatic collision detection for moving through 3d worlds with stair climbing and sliding, and manual scene node and triangle picking using a ray. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

Add the file archieve and get node and mesh
```cpp
device->getFileSystem()->addFileArchive("../../media/map-20kdm2.pk3");
scene::IAnimatedMesh* q3levelmesh = smgr->getMesh("20kdm2.bsp");
scene::IMeshSceneNode* q3node = 0;
// set it pickable, but without getting highlighted
if (q3levelmesh)
	q3node = smgr->addOctreeSceneNode(q3levelmesh->getMesh(0), 0, IDFlag_IsPickable);
```
We create a triangle selector. A triangle selector is a class which can fetch the triangles from scene nodes for doing different things with them. Here we choose OctreeTriangleSelector, which optimizes the triangle output a little bit by reducing it like an octree. Then attach it to the q3node.
```cpp
scene::ITriangleSelector* selector = 0;
if (q3node)
{
	q3node->setPosition(core::vector3df(-1350, -130, -1400));
	/* 128 means: If a node gets less polys the this value, it will not be splitted into smaller nodes. */
	selector = smgr->createOctreeTriangleSelector(
		q3node->getMesh(), q3node, 128);
	q3node->setTriangleSelector(selector);
	// We're not done with this selector yet, so don't drop it.
}
```
Set a node, and add the collision response animator
```cpp
scene::ICameraSceneNode* camera =
	smgr->addCameraSceneNodeFPS(0, 100.0f, .3f, ID_IsNotPickable, 0, 0, true, 3.f);
camera->setPosition(core::vector3df(50, 50, -60));
camera->setTarget(core::vector3df(-70, 30, -60));
// not allow mouse cursor control
device->getCursorControl()->setVisible(false);
if (selector)
{
	scene::ISceneNodeAnimator* anim = smgr->createCollisionResponseAnimator(
		selector, camera, core::vector3df(30, 50, 30),
		core::vector3df(0, -10, 0), core::vector3df(0, 30, 0));
	selector->drop(); 
	camera->addAnimator(anim);
	anim->drop();  
}
```
Add a billing board
```cpp
scene::IBillboardSceneNode * bill = smgr->addBillboardSceneNode();
bill->setMaterialType(video::EMT_TRANSPARENT_ADD_COLOR );
bill->setMaterialTexture(0, driver->getTexture("../../media/particle.bmp"));
bill->setMaterialFlag(video::EMF_LIGHTING, false);
bill->setMaterialFlag(video::EMF_ZBUFFER, false);
bill->setSize(core::dimension2d<f32>(20.0f, 20.0f));
bill->setID(ID_IsNotPickable); 
```
Add nodes and animate
```cpp
scene::IAnimatedMeshSceneNode* node = 0;
video::SMaterial material;
// Add an MD2 node, which uses vertex-based animation.
node = smgr->addAnimatedMeshSceneNode(smgr->getMesh("../../media/faerie.md2"),
	0, IDFlag_IsPickable | IDFlag_IsHighlightable);
node->setPosition(core::vector3df(-90, -15, -140)); // Put its feet on the floor.
node->setScale(core::vector3df(1.6f)); // Make it appear realistically scaled
node->setMD2Animation(scene::EMAT_POINT);
node->setAnimationSpeed(20.f);
material.setTexture(0, driver->getTexture("../../media/faerie2.bmp"));
material.Lighting = true;
material.NormalizeNormals = true;
node->getMaterial(0) = material;

// Now create a triangle selector for it.  The selector will know that it
// is associated with an animated node, and will update itself as necessary.
selector = smgr->createTriangleSelector(node);
node->setTriangleSelector(selector);
selector->drop(); 

// And this B3D file uses skinned skeletal animation.
node = smgr->addAnimatedMeshSceneNode(smgr->getMesh("../../media/ninja.b3d"),
	0, IDFlag_IsPickable | IDFlag_IsHighlightable);
node->setScale(core::vector3df(10));
node->setPosition(core::vector3df(-75, -66, -80));
node->setRotation(core::vector3df(0, 90, 0));
node->setAnimationSpeed(8.f);
node->getMaterial(0).NormalizeNormals = true;
node->getMaterial(0).Lighting = true;
// Just do the same as we did above.
selector = smgr->createTriangleSelector(node);
node->setTriangleSelector(selector);
selector->drop();

// This X files uses skeletal animation, but without skinning.
node = smgr->addAnimatedMeshSceneNode(smgr->getMesh("../../media/dwarf.x"),
	0, IDFlag_IsPickable | IDFlag_IsHighlightable);
node->setPosition(core::vector3df(-70, -66, -30)); // Put its feet on the floor.
node->setRotation(core::vector3df(0, -90, 0)); // And turn it towards the camera.
node->setAnimationSpeed(20.f);
node->getMaterial(0).Lighting = true;
selector = smgr->createTriangleSelector(node);
node->setTriangleSelector(selector);
selector->drop();

// And this mdl file uses skinned skeletal animation.
node = smgr->addAnimatedMeshSceneNode(smgr->getMesh("../../media/yodan.mdl"),
	0, IDFlag_IsPickable | IDFlag_IsHighlightable);
node->setPosition(core::vector3df(-90, -25, 20));
node->setScale(core::vector3df(0.8f));
node->getMaterial(0).Lighting = true;
node->setAnimationSpeed(20.f);

// Just do the same as we did above.
selector = smgr->createTriangleSelector(node);
node->setTriangleSelector(selector);
selector->drop();

material.setTexture(0, 0);
material.Lighting = false;

// Add a light, so that the unselected nodes aren't completely dark.
scene::ILightSceneNode * light = smgr->addLightSceneNode(0, core::vector3df(-60, 100, 400),
	video::SColorf(1.0f, 1.0f, 1.0f, 1.0f), 600.0f);
light->setID(ID_IsNotPickable); 

// Remember which scene node is highlighted
scene::ISceneNode* highlightedSceneNode = 0;
scene::ISceneCollisionManager* collMan = smgr->getSceneCollisionManager();
```
The drawing part
```cpp
while (device->run()) {
	driver->beginScene(true, true, 0);
	smagr->drawAll();

	// unlight
	if (highlightedSceneNode)
	{
		highlightedSceneNode->setMaterialFlag(video::EMF_LIGHTING, true);
		highlightedSceneNode = 0;
	}

	/* All intersections in this example are done with a ray cast out from the camera to a distance of 1000. */
	core::line3d<f32> ray;
	ray.start = camera->getPosition();
	ray.end = ray.start + (camera->getTarget() - ray.start).normalize() * 1000.0f;

	core::vector3df intersection; // trace the intersections
	core::triangle3df hitTriangle; // show hitted triangle

	/* This call is all you need to perform ray/triangle collision on every scene node that has a triangle selector, including the Quake level mesh.  It finds the nearest collision point/triangle, and returns the scene node containing that point. Irrlicht provides other types of selection, including ray/triangle selector, ray/box and ellipse/triangle selector, plus associated helpers. */
	scene::ISceneNode * selectedSceneNode =
		collMan->getSceneNodeAndCollisionPointFromRay(
		ray,
		intersection, // This will be the position of the collision
		hitTriangle, // This will be the triangle hit in the collision
		IDFlag_IsPickable, 
		0); 

	// If the ray hit anything, move the billboard to the collision position
	// and draw the triangle that was hit.
	if (selectedSceneNode)
	{
		bill->setPosition(intersection);

		// We need to reset the transform before doing our own rendering.
		driver->setTransform(video::ETS_WORLD, core::matrix4());
		driver->setMaterial(material);
		driver->draw3DTriangle(hitTriangle, video::SColor(0, 255, 0, 0));

		// We can check the flags for the scene node that was hit to see if it should be highlighted. 
		if ((selectedSceneNode->getID() & IDFlag_IsHighlightable) == IDFlag_IsHighlightable)
		{
			highlightedSceneNode = selectedSceneNode;
			// Highlighting: it will be drawn with full brightness.
			highlightedSceneNode->setMaterialFlag(video::EMF_LIGHTING, false);
		}
	}
}
```
You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/07.Collision)