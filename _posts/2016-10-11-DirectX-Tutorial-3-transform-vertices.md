---
layout: post
title: "DirectX Tutroial 3 Transform Vertices"
categories : DirectX
tags : CPP DirectX Graphics
---
* content
{:toc}

This tutorials are based on the [DirectX Tutorial](http://www.directxtutorial.com/), show how to transform vertices, or convert them from 3D coordinates to screen coordinates using DirectX 9.

## Description

let's take a look at everything that happens to translate something from 3D coordinates to a flat image. There is a sequence of actions which must occur before an object appears on the screen properly. This sequence of actions is known as the Geometry Pipeline. It is called a pipeline because vertices are put through each step one at a time, and at each step along the "pipe", the vertex is rendered into its flat image form.

![](/images/directX/3.png)

Before we go to the details, let me explain the three transforms in a very easy way.
When we are going to take a pictures, there are four steps:
	
>	put the staff you are going to photo in the position (world transformation)
>
>	modify the camera angle (view transformation)
>
>	modify the focal distance (project transformation)
>
>	take a picture

## World Transformation

Changes coordinates from model space to world space. In other words, it places a model in a world at an exact point defined by coordinates. 

Of course, being able to move an object into world space is always useful, but it can get rather limiting if your model is always facing the same direction. A spaceship that can only face East is rather dull and does not elicit much thrill or adrenaline (or so I find).

And so another part of World Transformation is rotation. Rotation is the process of spinning 3D objects along an axis.

Another important part of World Transformation is scaling. Scaling is the action of making a 3D object larger or smaller.

## View Transformation

View transformation is a process which sets up the 3D coordinate system to point in the proper direction. What this means is that the directions of each axis are going to change to point in different directions. 

Direct3D uses the concept of a virtual camera. This camera has an exact position and points at an exact vector. When world transformation is done, the 3D axes have no alignment to how the scene will be viewed.

![](/images/directX/4.png)

In order for Direct3D and the video card to quickly process the 3D scene, the 3D axes must align with the camera. Specifically, the origin is repositioned to where the camera is, and the z-axis points directly down the line of sight.

![](/images/directX/5.png)

## Projection Transformation

If view transformation can be thought of as a camera, then this step can be thought of as a lens. Once view transformation is completed, we have to change the 3D scene into one big 2D image so it can be drawn on the screen. The process that does this is called projection transformation. It is simply the converting of 3D coordinates to screen coordinates.

Let's see how to do them in DirectX3D.

## Setting the World Transformation

1. Transformation

```cpp
D3DXMATRIX matTranslate;    // a matrix to store the translation information

// build a matrix to move the model 12 units along the x-axis and 4 units along the y-axis
// store it to matTranslate
D3DXMatrixTranslation(&matTranslate, 12.0f, 4.0f, 0.0f);

// tell Direct3D about our matrix
d3ddev->SetTransform(D3DTS_WORLD, &matTranslate);
```

2. Rotation

```cpp
D3DXMATRIX matRotateX;    // a matrix to store the rotation information
// build a matrix to rotate the model 3.14 radians
D3DXMatrixRotationX(&matRotateX, 3.14f);

// tell Direct3D about our matrix
d3ddev->SetTransform(D3DTS_WORLD, &matRotateX);
```

3. Scaling 

```cpp
D3DXMATRIX matScale;    // a matrix to store the scaling information

// build a matrix to double the size of the model
// store it to matScale
D3DXMatrixScaling(&matScale, 2.0f, 2.0f, 2.0f);

// tell Direct3D about our matrix
d3ddev->SetTransform(D3DTS_WORLD, &matScale);
```

If you want to combine all of them, you can just do this:

```cpp
d3ddev->SetTransform(D3DTS_WORLD,
    &(matTranslate * matRotateX * matRotateY * matRotateZ * matScale));
```

## Setting the View Transformation

Setting the view transformation can be considered to be similar to setting up a virtual camera. All a programmer does with this is feed the camera position, direction and rotation into a single matrix. 

```cpp
D3DXMATRIX matView;    // the view transform matrix

D3DXMatrixLookAtLH(&matView,
    &D3DXVECTOR3 (100.0f, 100.0f, 100.0f),    // the camera position
    &D3DXVECTOR3 (0.0f, 0.0f, 0.0f),    // the look-at position
    &D3DXVECTOR3 (0.0f, 1.0f, 0.0f));    // the up direction

d3ddev->SetTransform(D3DTS_VIEW, &matView);    // set the view transform to matView
```

## Setting the Projection Transformation

If view transformation can be considered the camera setup, then projection transformation can be thought of as the camera lens. It is probably the most complex type of transformation. It is simple in code (as it only needs one matrix, set by a single function), but it has a lot of factors which control it.

```cpp
D3DXMATRIX matProjection;    // the projection transform matrix

D3DXMatrixPerspectiveFovLH(&matProjection,
   D3DXToRadian(45),    // the horizontal field of view
   (FLOAT)SCREEN_WIDTH / (FLOAT)SCREEN_HEIGHT,    // aspect ratio
   1.0f,    // the near view-plane
   100.0f);    // the far view-plane
d3ddev->SetTransform(D3DTS_PROJECTION, &matProjection);    // set the projection transform
```

We don't have any code to add lights just yet, and without these, nothing will appear at all. Let's change that by turning off the lights just for now, and having everything show up normally (as if everything were lit automatically). 

```cpp
d3ddev->SetRenderState(D3DRS_LIGHTING, FALSE);    // turn off the 3D lightings
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Learning/blob/master/TransformingVertices.cpp)

If you run this program you should get something like this:

![](/images/directX/6.png)