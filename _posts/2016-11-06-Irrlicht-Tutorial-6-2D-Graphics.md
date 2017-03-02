---
layout: post
title: Irrlicht Tutroial 6 2D Graphics
description: Irrlicht Tutroial
keywords: Irrlicht
categories : Irrlicht
tags : CPP Irrlicht Graphics
---

* content
{:toc}

This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to draw images, keycolor based sprites, transparent rectangles, and different fonts. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

All 2d graphics in this example are put together into one texture, 2ddemo.png. Because we want to draw colorkey based sprites, we need to load this texture and tell the engine, which part of it should be transparent based on a colorkey.

You just ask for the color in this position, that's it.
```cpp
video::ITexture* images = driver->getTexture("../../media/2ddemo.png");
driver->makeColorKeyTexture(images, core::position2d<s32>(0,0));
```
Load two fonts 
```cpp
gui::IGUIFont* font = device->getGUIEnvironment()->getBuiltInFont();
gui::IGUIFont* font2 =
  device->getGUIEnvironment()->getFont("../../media/fonthaettenschweiler.bmp");

core::rect<s32> imp1(349,15,385,78);
core::rect<s32> imp2(387,15,423,78);
```
Prepare a nicely filtering 2d render mode for special cases.
```cpp
driver->getMaterial2D().TextureLayer[0].BilinearFilter=true;
driver->getMaterial2D().AntiAliasing=video::EAAM_FULL_BASIC;
```
This case only use 2d without any 3d
```cpp
while(device->run() && driver)
{
	if (device->isWindowActive())
	{
		u32 time = device->getTimer()->getTime();
		driver->beginScene(true, true, video::SColor(255,120,102,136));
```
draw 3 sprites
```cpp
		// draw fire & dragons background world
		driver->draw2DImage(images, core::position2d<s32>(50,50),
			core::rect<s32>(0,0,342,224), 0,
			video::SColor(255,255,255,255), true);

		// draw flying imp
		driver->draw2DImage(images, core::position2d<s32>(164,125),
			(time/500 % 2) ? imp1 : imp2, 0,
			video::SColor(255,255,255,255), true);

		// draw second flying imp with colorcylce
		driver->draw2DImage(images, core::position2d<s32>(270,105),
			(time/500 % 2) ? imp1 : imp2, 0,
			video::SColor(255,(time) % 255,255,255), true);
```
Draw some texts
{% highlight Java %}
		if (font)
			font->draw(L"This demo shows that Irrlicht is also capable of drawing 2D graphics.",
				core::rect<s32>(130,10,300,50),
				video::SColor(255,255,255,255));
		if (font2)
			font2->draw(L"Also mixing with 3d graphics is possible.",
				core::rect<s32>(130,20,300,60),
				video::SColor(255,time % 255,time % 255,255));
```
Draw the logo
```cpp
		driver->enableMaterial2D();
		driver->draw2DImage(images, core::rect<s32>(10,10,108,48),
			core::rect<s32>(354,87,442,118));
		driver->enableMaterial2D(false);
```
Finally draw a half-transparent rect under the mouse cursor.
```cpp
		core::position2d<s32> m = device->getCursorControl()->getPosition();
		driver->draw2DRectangle(video::SColor(100,255,255,255),
			core::rect<s32>(m.X-20, m.Y-20, m.X+20, m.Y+20));

		driver->endScene();
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/06.2DGraphics)