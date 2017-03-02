---
layout: post
title: "DirectX Tutroial 6 More on Lighting"
categories : DirectX
tags : CPP DirectX Graphics
---

* content
{:toc}

This tutorials are based on the [DirectX Tutorial](http://www.directxtutorial.com/), talking about point lights and spot lights.

## Point Lights

A point light, as discussed in the previous lesson, is a light which has an exact location, and emanates light in all directions from that location.

Unlike a directional light, a point light does not go on indefinitely. As the light travels away from the source, it gets dispersed, spreading out in every direction equally. Therefore, the farther an object is from a directional light, the less illuminated that object will be. 

1. range
```cpp
light.Range = 100.0f;
```

2. Attenuation

I am going to give you the algebraic function (not C++ function) for attenuation,

Atten = 1 / (att0 + att1 * d + att2 * d2)

>	Atten: It is a number between 1.0 and 0.0 which indicates the intensity of light. 1.0 is full intensity, while 0.0 is no intensity (no light).
>
>	d: the distance between the vertex and the light
>
>	att0: a constant modifier. if you put 0.5 in this value, you will get a half-lit light that will extend all the way to the maximum range of the light.
>
>	att1: If used by itself, it is an inverse function, meaning that the light will dissipate more slowly as the distance increases. 
>
>	att2:  If used by itself, it is an inverse square function, meaning that the light will not only dissipate more slowly as the distance increases, but the dissipation will be very rapid at first, then sharply slow down. 

Coding a Point Light
```cpp
void init_light(void)
{
    D3DLIGHT9 light;
    D3DMATERIAL9 material;

    ZeroMemory(&light, sizeof(light));
    light.Type = D3DLIGHT_POINT;    // make the light type 'point light'
    light.Diffuse = D3DXCOLOR(0.5f, 0.5f, 0.5f, 1.0f);
    light.Position = D3DXVECTOR3(0.0f, 5.0f, 0.0f);
    light.Range = 100.0f;    // a range of 100
    light.Attenuation0 = 0.0f;    // no constant inverse attenuation
    light.Attenuation1 = 0.125f;    // only .125 inverse attenuation
    light.Attenuation2 = 0.0f;    // no square inverse attenuation

    d3ddev->SetLight(0, &light);
    d3ddev->LightEnable(0, TRUE);

    ZeroMemory(&material, sizeof(D3DMATERIAL9));
    material.Diffuse = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);
    material.Ambient = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);

    d3ddev->SetMaterial(&material);
}
```

## Spot Lights

The spotlight is the least-used, least-efficient, and least-simple type of light there is. It actually requires the entire D3DLIGHT9 struct to be filled. 

In Direct3D, this is recreated using two values to show how wide these two circles are. As you can see, Theta represents the inner circle and Phi represents the outer circle. Phi and Theta are both float values which hold the angle used to determine the size of each circle.

![](/images/directX/17.png)

Falloff: You will see that the bright circle actually fades away into the dark circle.

![](/images/directX/18.png)

Coding a Spot Light
```cpp
void init_light(void)
{
    D3DLIGHT9 light;
    D3DMATERIAL9 material;

    ZeroMemory(&light, sizeof(light));
    light.Type = D3DLIGHT_SPOT;    // make the light type 'spot light'
    light.Diffuse = D3DXCOLOR(0.5f, 0.5f, 0.5f, 1.0f);
    light.Position = D3DXVECTOR3(-12.0f, 0.0f, 30.0f);
    light.Direction = D3DXVECTOR3(0.0f, 0.0f, -1.0f);
    light.Range = 100.0f;    // a range of 100
    light.Attenuation0 = 0.0f;    // no constant inverse attenuation
    light.Attenuation1 = 0.125f;    // only .125 inverse attenuation
    light.Attenuation2 = 0.0f;    // no square inverse attenuation
    light.Phi = D3DXToRadian(40.0f);    // set the outer cone to 30 degrees
    light.Theta = D3DXToRadian(20.0f);    // set the inner cone to 10 degrees
    light.Falloff = 1.0f;    // use the typical falloff

    d3ddev->SetLight(0, &light);
    d3ddev->LightEnable(0, TRUE);

    ZeroMemory(&material, sizeof(D3DMATERIAL9));
    material.Diffuse = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);
    material.Ambient = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);

    d3ddev->SetMaterial(&material);
}
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Learning/blob/master/Rendering%20with%20Vertex%20Lighting.cpp)

If you run this program you should get something like this:

![](/images/directX/19.png)