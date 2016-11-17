---
layout: post
title: Irrlicht Tutroial 4 Movement
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how manual movement of nodes using the keyboard. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

we need an object which is derived from the irr::IEventReceiver object. There is only one method to override: irr::IEventReceiver::OnEvent(). This method will be called by the engine once when an event happens. What we really want to know is whether a key is being held down, and so we will remember the current state of each key.
{% highlight C++%}
class MyEventReceiver : public IEventReceiver {
public:
	virtual bool onEvent(const SEvent& event) {
		if (event.type == irr::EET_KEY_INPUT_EVENT)
			KeyIsDown[event.KeyInput.Key] = event.KeyInput.PressedDown;
		return false;
	}

	// check whether a key is begin held down
	virtual bool IsKeyDown(EKEY_CODE keyCode) const {
        return KeyIsDown[keyCode];
    }

    MyEventReceiver() {
    	for (u32 i=0; i<KEY_KEY_CODES_COUNT; ++i)
    	KeyIsDown[i] = false;
    }
private:
	bool KeyIsDown[KEY_KEY_CODES_COUNT];
}
{% endhighlight %}
Then it's the main part, just like the pevious example, create the device, video driver, and scene manager and camera. And create the event receiver.
(MyEventReceiver receiver;)

Create a node moved with the WSAD keys, and set the position and material
{% highlight C++%}
scene::ISceneNode *node = smgr->addSphereNode();
if (node) {
	node->setPosition(core::vector3df(0,0,30));
    node->setMaterialTexture(0, driver->getTexture("../../media/wall.bmp"));
    node->setMaterialFlag(video::EMF_LIGHTING, false);
}
{% endhighlight %}
Create another node, moveable using a scene node animator 
{% highlight C++%}
scene::ISceneNode* n = smgr->addCubeSceneNode();
if (n) {
n->setMaterialTexture(0, driver->getTexture("../../media/t351sml.jpg"));
    n->setMaterialFlag(video::EMF_LIGHTING, false);
    scene::ISceneNodeAnimator* anim =
        smgr->createFlyCircleAnimator(core::vector3df(0,0,30), 20.0f);
    if (anim)
    {
        n->addAnimator(anim);
        anim->drop();
    }
}
{% endhighlight %}
The last scene node is to show possibilities of scene node animators is
	a b3d model, which uses a 'fly straight' animator to run between to points.
{% highlight C++%}
scene::IAnimatedMeshSceneNode* anms =
	smgr->addAnimatedMeshSceneNode(smgr->getMesh("../../media/ninja.b3d"));

if (anms)
{
	scene::ISceneNodeAnimator* anim =
		smgr->createFlyStraightAnimator(core::vector3df(100, 0, 60),
		core::vector3df(-100, 0, 60), 3500, true);
	if (anim)
	{
		anms->addAnimator(anim);
		anim->drop();
	}

	/*
	To make the model look right we disable lighting, set the
	frames between which the animation should loop, rotate the
	model around 180 degrees, and adjust the animation speed and
	the texture. To set the right animation (frames and speed), we
	would also be able to just call
	*/
	anms->setMaterialFlag(video::EMF_LIGHTING, false);
	anms->setFrameLoop(0, 13);
	anms->setAnimationSpeed(15);
	anms->setScale(core::vector3df(2.f, 2.f, 2.f));
	anms->setRotation(core::vector3df(0, -90, 0));
}
{% endhighlight %}
Add the camera and make the mouse cursor invisible
{% highlight C++%}
smgr->addCameraSceneNodeFPS();
device->getCurSorControal()->setVisible(false);
{% endhighlight %}
Add a logo
{% highlight C++%}
device->getGUIEnvironment()->addImage(
	driver->getTexture("../../media/irrlichtlogoalpha2.tga"),
	core::position2d<s32>(10,20));

gui::IGUIStaticText* diagnostics = device->getGUIEnvironment()->addStaticText(
	L"", core::rect<s32>(10, 10, 400, 20));
diagnostics->setOverrideColor(video::SColor(255, 255, 255, 0));
{% endhighlight %}
Then draw everything
{% highlight C++ %}
while (device->run()) {
	/* Check if keys W, S, A or D are being held down, and move the sphere node around respectively. */
	// Work out a frame delta time.
    const u32 now = device->getTimer()->getTime();
    const f32 frameDeltaTime = (f32)(now - then) / 1000.f; // Time in seconds
    core::vector3df nodePosition = node->getPosition();

    if(receiver.IsKeyDown(irr::KEY_KEY_W))
        nodePosition.Y += MOVEMENT_SPEED * frameDeltaTime;
    else if(receiver.IsKeyDown(irr::KEY_KEY_S))
        nodePosition.Y -= MOVEMENT_SPEED * frameDeltaTime;

    if(receiver.IsKeyDown(irr::KEY_KEY_A))
        nodePosition.X -= MOVEMENT_SPEED * frameDeltaTime;
    else if(receiver.IsKeyDown(irr::KEY_KEY_D))
        nodePosition.X += MOVEMENT_SPEED * frameDeltaTime;

    node->setPosition(nodePosition);

	driver->beginScene(true, true, video::SColor(0, 100, 100, 100));
	smgr->drawAll();
	device->getGUIEnvironment()->drawAll(); // draw the logo
	driver->endScene();
}
device->drop();
{% endhighlight %}

You can get the complete codes from [Github](https://github.com/Shanshan-IC/irrlicht/tree/master/examples/04.Movement)