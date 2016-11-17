---
layout: post
title: Irrlicht Irrlicht Common Functions Notes Update
description: Irrlicht Tips backup
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

Irrlicht functions tips:

{% highlight C++ %}
// create a device
IrrlichtDevice *device = 
	createDevice( video::EDT_SOFTWARE, dimension2d<u32>(640, 480), 16, false, false, false, 0);

// Get a pointer to the VideoDriver, the SceneManager and the graphical user interface environment
IVideoDriver* driver = device->getVideoDriver();
ISceneManager* smgr = device->getSceneManager();
IGUIEnvironment* guienv = device->getGUIEnvironment();

// set the caption of windows 
device->setWindowCaption(L"Hello World! - Irrlicht Engine Demo");
// add label
guienv->addStaticText(L"Hello World! This is the Irrlicht Software renderer!",
		rect<s32>(10,10,260,22), true);
// add a logo 
guienv->addImage(
	driver->getTexture("../../media/irrlichtlogoalpha2.tga"),
	core::position2d<s32>(10,20));
// skin and font 
IGUISkin* skin = env->getSkin();
IGUIFont* font = env->getFont("../../media/fonthaettenschweiler.bmp");
if (font)
    skin->setFont(font);
skin->setFont(env->getBuiltInFont(), EGDF_TOOLTIP);
// add button, you set it by your self
env->addButton(rect<s32>(10,240,110,240 + 32), 0, GUI_ID_QUIT_BUTTON,
        L"Quit", L"Exits Program");
// add scrollbar
IGUIScrollBar* scrollbar = env->addScrollBar(true,
		rect<s32>(150, 45, 350, 60), 0, GUI_ID_TRANSPARENCY_SCROLL_BAR);
scrollbar->setMax(255);
scrollbar->setPos(255);
setSkinTransparency( scrollbar->getPos(), env->getSkin());
// set scrollbar position to alpha value of an arbitrary element
scrollbar->setPos(env->getSkin()->getColor(EGDC_WINDOW).getAlpha());
// add listbox
IGUIListBox * listbox = env->addListBox(rect<s32>(50, 140, 250, 210));
// add editbox
env->addEditBox(L"Editable Text", rect<s32>(350, 80, 550, 100));
// Notes: more interface functions, go for the sample 5: user interfaces
// add file to archieve
device->getFileSystem()->addFileArchive("../../media/map-20kdm2.pk3");

// get mesh, sometimes the .bsp file
IAnimatedMesh* mesh = smgr->getMesh("../../media/sydney.md2");
// hill mesh
mesh = smgr->addHillPlaneMesh( "myHill",
    core::dimension2d<f32>(20,20),
    core::dimension2d<u32>(40,40), 0, 0,
    core::dimension2d<f32>(0,0),
    core::dimension2d<f32>(10,10));

// add node
// IAnimatedMeshSceneNode: Scene node capable of displaying an animated mesh and its shadow 
IAnimatedMeshSceneNode* node = smgr->addAnimatedMeshSceneNode( mesh );
if (node) {
	node->setPosition(core::vector3df(0,0,30));
	node -> setMaterialFlag(EMF_LIGHTING, false);
	node -> setMD2Animation(scene::EMAT_STAND);
	node->setMaterialTexture( 0, driver->getTexture("../../media/sydney.bmp") );
}
// normal scene node: addOctreeSceneNode is for rendering using a octree to the scene graph.
scene::ISceneNode* node = 0;
if (mesh) {
    node = smgr->addOctreeSceneNode(mesh->getMesh(0), 0, -1, 1024);   
}
if (node) {
	node->setPosition(core::vector3df(-1300,-144,-1249));
}
// sphere, 0.2 is its radius
scene::ISceneNode *sphereNode = smgr->addSphereSceneNode(0.2);
// cube
scene::ISceneNode *cubeNode=smgr->addCubeSceneNode(100.0f);
// cylinder
const IGeometryCreator* igCreator = smgr->getGeometryCreator();
IMesh* cylinder = igCreator->createCylinderMesh(1.0f, 5.0f, 30, video::SColor(255, 255, 255, 255), false);
scene::IMeshSceneNode* cylinderNode = smgr->addMeshSceneNode(cylinder);
// water surface node
node = smgr->addWaterSurfaceSceneNode(mesh->getMesh(0), 3.0f, 300.0f, 30.0f);
// light node
node = smgr->addLightSceneNode(0, core::vector3df(0,0,0),
        video::SColorf(1.0f, 0.6f, 0.7f, 1.0f), 800.0f);
// terrain node
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
// skybox node
scene::ISceneNode* skybox=smgr->addSkyBoxSceneNode(
    driver->getTexture("../../media/irrlicht2_up.jpg"),
    driver->getTexture("../../media/irrlicht2_dn.jpg"),
    driver->getTexture("../../media/irrlicht2_lf.jpg"),
    driver->getTexture("../../media/irrlicht2_rt.jpg"),
    driver->getTexture("../../media/irrlicht2_ft.jpg"),
    driver->getTexture("../../media/irrlicht2_bk.jpg"));
// skydome node
scene::ISceneNode* skydome=smgr->addSkyDomeSceneNode(driver->getTexture("../../media/skydome.jpg"),16,8,0.95f,2.0f);

// billing board
scene::IBillboardSceneNode * bill = smgr->addBillboardSceneNode();

// Add an animator to the scence node 
// rotate it
scene::ISceneNodeAnimator* anim =
	smgr->createRotationAnimator(core::vector3df(0.8f, 0, 0.8f));
// flying circle
scene::ISceneNodeAnimator* anim =
        smgr->createFlyCircleAnimator(core::vector3df(0,0,30), 20.0f);
// flying straight between two points
scene::ISceneNodeAnimator* anim =
		smgr->createFlyStraightAnimator(core::vector3df(100, 0, 60),
		core::vector3df(-100, 0, 60), 3500, true);
// collision
scene::ISceneNodeAnimator* anim = smgr->createCollisionResponseAnimator(
		selector, camera, core::vector3df(30, 50, 30),
		core::vector3df(0, -10, 0), core::vector3df(0, 30, 0));
if (anim) {
	myNode->addAnimator(anim);
	anim->drop();
	anim = 0;
}
// when it's done, drop the node
myNode->drop();
myNode=0;

// draw 2D image, images is the image you load it from the computer
driver->draw2DImage(images, core::position2d<s32>(50,50),
			core::rect<s32>(0,0,342,224), 0,
			video::SColor(255,255,255,255), true);

// add triangle selector
scene::ITriangleSelector* selector = 0;
if (node)
{
	node->setPosition(core::vector3df(-1350, -130, -1400));
	selector = smgr->createOctreeTriangleSelector(
		node->getMesh(), node, 128);
	node->setTriangleSelector(selector);
}
// terrain triangle selector
scene::ITriangleSelector* selector = smgr->createTerrainTriangleSelector(terrain, 0);

// render to texture
ITexture* rt = driver->addRenderTargetTexture(core::dimension2d<u32>(256,256), "RTT1");
driver->setRenderTarget(rt, true, true, video::SColor(0,0,0,255));

// add a camera
smgr -> addCameraSceneNode(0, vector3df(0, 30, -40), vector3df(0, 5, 0))
// appropriate for first person shooters (FPS)
smgr->addCameraSceneNodeFPS();

// mouse cursor not visible
device->getCursorControl()->setVisible(false);

// draw everything
while(device->run()) {
	driver -> beginScene(true, true, SColor(255, 100, 101, 140));
	smgr -> drawAll();
	guienv -> drawAll();
	driver -> endScene();
}
device -> drop();
{% endhighlight %}

Specail Notes:

Maybe some beginner will be confused by some files used in Irrlicht, here we talked about pak, bsp file.

pak file:.pak file is a special compress file format, developed by Quake Game Company. It compresses multiple files, there are some differences between it and other compress file formats:
* file is compressed with the path in the computer
* It's good for the game developer because the convenient sources management, and complicated structure, that is not modified by the fresh learner.
* If you want to check it, you can just use the pak browser tools to check it.

