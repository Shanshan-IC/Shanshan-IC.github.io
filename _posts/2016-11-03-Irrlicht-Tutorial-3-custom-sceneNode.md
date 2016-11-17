---
layout: post
title: Irrlicht Tutroial 3 Custom SceneNde
description: Irrlicht Tutroial
keywords: Irrlicht
categories : [Irrlicht]
tags : [C++, Irrlicht, Graphics]
---

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to create a custom scene node and display it. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

create a pyramid, we create a class derived from the irr::scene::ISceneNode class and has to override some methods.

{% highlight C++ %}
class CSampleSceneNode : public scene::ISceneNode {
	core::aabbox3d<f32> Box;//bouding box
	video::S3DVertex Vertices[4];//4 vertices
	video::SMaterial Material;//materials

public:
	CSampleSceneNode(scene::ISceneNode* parent, scene::ISceneManager* mgr, s32 id)
		: scene::ISceneNode(parent, mgr, id)
	{
		Material.Wireframe = false;
		Material.Lighting = false;
		// position, normals, and colors, texture
		Vertices[0] = video::S3DVertex(0,0,10, 1,1,0,
				video::SColor(255,0,255,255), 0, 1);
		Vertices[1] = video::S3DVertex(10,0,-10, 1,0,0,
				video::SColor(255,255,0,255), 1, 1);
		Vertices[2] = video::S3DVertex(0,20,0, 0,1,1,
				video::SColor(255,255,255,0), 1, 0);
		Vertices[3] = video::S3DVertex(-10,0,-10, 0,0,1,
				video::SColor(255,0,255,0), 0, 0);

	/*
	The Irrlicht Engine needs to know the bounding box of a scene node.
	It will use it for automatic culling and other things. Hence, we
	need to create a bounding box from the 4 vertices we use.
	*/
		Box.reset(Vertices[0].Pos);
		for (s32 i=1; i<4; ++i)
			Box.addInternalPoint(Vertices[i].Pos);
	}

	/*
	normal scene nodes render their content one after another, while stencil buffer shadows would like to be drawn after all other scene nodes. And camera or light scene nodes need to be rendered before all other scene nodes (if at all). So here we simply register the scene node to render normally. If we would like to let it be rendered like cameras or light, we would have to call SceneManager->registerNodeForRendering(this, SNRT_LIGHT_AND_CAMERA)
	*/
	virtual void OnRegisterSceneNode()
	{
		if (IsVisible)
			SceneManager->registerNodeForRendering(this);

		ISceneNode::OnRegisterSceneNode();
	}

	// override render()
	virtual void render()
    {
        u16 indices[] = {   0,2,3, 2,1,3, 1,0,3, 2,0,1  };
        video::IVideoDriver* driver = SceneManager->getVideoDriver();

        driver->setMaterial(Material);
        driver->setTransform(video::ETS_WORLD, AbsoluteTransformation);
        driver->drawVertexPrimitiveList(&Vertices[0], 4, &indices[0], 4, video::EVT_STANDARD, scene::EPT_TRIANGLES, video::EIT_16BIT);
    }

    // get private value
    virtual const core::aabbox3d<f32>& getBoundingBox() const
    {
        return Box;
    }

    virtual u32 getMaterialCount() const
    {
        return 1;
    }

    virtual video::SMaterial& getMaterial(u32 i)
    {
        return Material;
    }   
}
{% endhighlight %}
Then it's the main part, just like the pevious example, create the device, video driver, and scene manager and camera.

Next, Create the nodes.
{% highlight C++%}
CSampleSceneNode *myNode =
new CSampleSceneNode(smgr->getRootSceneNode(), smgr, 666);
// except this, we also show how to create 
// sphere, 0.2 is its radius
scene::ISceneNode *sphereNode = smgr->addSphereSceneNode(0.2);
// cube
scene::ISceneNode *cubeNode=smgr->addCubeSceneNode(100.0f);
// cylinder
const IGeometryCreator* igCreator = smgr->getGeometryCreator();
IMesh* cylinder = igCreator->createCylinderMesh(1.0f, 5.0f, 30, video::SColor(255, 255, 255, 255), false);
scene::IMeshSceneNode* cylinderNode = smgr->addMeshSceneNode(cylinder);
{% endhighlight %}
Add an animator to the scence node to rotate it
{% highlight C++ %}
scene::ISceneNodeAnimator* anim =
	smgr->createRotationAnimator(core::vector3df(0.8f, 0, 0.8f));
if (anim) {
	myNode->addAnimator(anim);
	anim->drop();
	anim = 0;
}
// when it's done, drop the node
myNode->drop();
myNode=0;
{% endhighlight %}
Then draw everything
{% highlight C++ %}
while (device->run()) {
	driver->beginScene(true, true, video::SColor(0, 100, 100, 100));
	smgr->drawAll();
	driver->endScene();
}
device->drop();
{% endhighlight %}

You can get the complete codes from [Github](https://github.com/Shanshan-IC/irrlicht/tree/master/examples/03.CustomSceneNode)
