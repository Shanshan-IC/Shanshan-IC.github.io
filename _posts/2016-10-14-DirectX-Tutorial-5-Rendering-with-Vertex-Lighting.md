---
layout: post
title: DirectX Tutroial 5 Rendering with Vertex Lighting
categories : [DirectX]
tags : [C++, DirectX, Graphics]
---

* content
{:toc}

This tutorials are based on the [DirectX Tutorial](http://www.directxtutorial.com/), show how to use lights to illuminate your 3D scene.

Direct3D uses lights to approximate real-world lighting. It does this using a system of calculation that is much less time-consuming, and that can therefore be run in real-time. This system is built up of a set of types of lighting and types of light sources.

## type of lighting

There are three types of lighting that can be used to approximate real-world light. They are called diffuse lighting, ambient lighting and specular lighting.

Diffuse lighting is light that more or less falls directly onto a surface. Diffuse lighting is light that more or less falls directly onto a surface. If you hold up your hand in a room with one light source, you will see that one side of your hand is lit, it is.

![](/images/directX/11.png)

Ambient lighting consists of light that is everywhere. Generally speaking, it is quite dark (though not totally dark). When you hold your hand up in that room with one light source, the dark side of your hand is ambiently lit, and the light that is reflected there is refered to as ambient light.

![](/images/directX/12.png)

Specular lighting is often refered to as specular highlight or reflection. When light reflects off an object, ususally most of the light will go in one specific direction. The result is that each object has a little shine on it that comes from the light source.

![](/images/directX/13.png)

## Types of Light Sources

In order to produce the three types of light, there are several types of lights (or light sources) that emanate light.

	Ambient Lights
	Directional Lights
	Point Lights
	Spot Lights

## Materials

A material is a description of how surfaces reflect light, and which colors are involved. In other words, you won't necessarily see this color. You will only see it when you shine a light on it.

![](/images/directX/14.png)

Let's go practice.

## Creating Lights

1. Setting Up a New Flexible Vertex Format
```cpp
struct CUSTOMVERTEX {FLOAT X, Y, Z; D3DVECTOR NORMAL;};
#define CUSTOMFVF (D3DFVF_XYZ | D3DFVF_NORMAL)

typedef struct D3DVECTOR {
    float x, y, z;
} D3DVECTOR, *LPD3DVECTOR;
```
2. Turning the Lighting On
```cpp
d3ddev->SetRenderState(D3DRS_LIGHTING, TRUE);
```
3. Setting the Ambient Light
```cpp
d3ddev->SetRenderState(D3DRS_AMBIENT, D3DCOLOR_XRGB(50, 50, 50));    // ambient light
```
4. Creating and Setting the Diffuse Light
```cpp
// this is the function that sets up the lights and materials
void init_light(void)
{
    D3DLIGHT9 light;    // create the light struct

    ZeroMemory(&light, sizeof(light));    // clear out the light struct for use
    light.Type = D3DLIGHT_DIRECTIONAL;    // make the light type 'directional light'
    light.Diffuse = D3DXCOLOR(0.5f, 0.5f, 0.5f, 1.0f);    // set the light's color
    light.Direction = D3DXVECTOR3(-1.0f, -0.3f, -1.0f);

    d3ddev->SetLight(0, &light);    // send the light struct properties to light #0
    d3ddev->LightEnable(0, TRUE);    // turn on light #0
    ZeroMemory(&material, sizeof(D3DMATERIAL9));    // clear out the struct for use
}
```
5. Creating and Setting the Material
```cpp
material.Diffuse = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);    // set diffuse color to white
material.Ambient = D3DXCOLOR(1.0f, 1.0f, 1.0f, 1.0f);    // set ambient color to white
d3ddev->SetMaterial(&material);    // set the globably-used material to &material
```

## Set the texture

```cpp
// Use D3DX to create a texture from a file based image
if (FAILED(D3DXCreateTextureFromFile(g_pd3dDevice, L"banana.bmp", &g_pTexture)))
{
    // If texture is not in current folder, try parent folder
    if (FAILED(D3DXCreateTextureFromFile(g_pd3dDevice, L"banana.bmp", &g_pTexture)))
    {
        MessageBox(NULL, L"Could not find banana.bmp", L"Textures.exe", MB_OK);
        return E_FAIL;
    }
}
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Learning/blob/master/Rendering%20with%20Vertex%20Lighting.cpp)

If you run this program you should get something like this:

![](/images/directX/16.png)