---
layout: post
title: DirectX Tutroial 2 Vertext to Draw a Triangle
description: DirectX Tutroial
keywords: DirectX
categories : [DirectX]
tags : [C++, DirectX, Graphics]
---

This tutorials are based on the [DirectX Tutorial](http://www.directxtutorial.com/), show how to create a triangle using DirectX 9.

Set up the global variable
{% highlight C++ %}
LPDIRECT3D9             g_pD3D = NULL; // Used to create the D3DDevice
LPDIRECT3DDEVICE9       g_pd3dDevice = NULL; // Our rendering device
LPDIRECT3DVERTEXBUFFER9 g_pVB = NULL; // Buffer to hold vertices
{% endhighlight %}
create a structure as the vertex, here we include the location and the diffuse color.

Now we need to create the vertices using our new format. We do it by building a simple struct containing the variables we included in the FVF code.
{% highlight C++ %}
#define CUSTOMFVF (D3DFVF_XYZRHW | D3DFVF_DIFFUSE)
struct CUSTOMVERTEX
{
    FLOAT x, y, z, rhw;    // from the D3DFVF_XYZRHW flag
    DWORD color;    // from the D3DFVF_DIFFUSE flag
}
{% endhighlight %}
Use the structure to create the triangle
{% highlight C++ %}
CUSTOMVERTEX OurVertices[] =
{
    {320.0f, 50.0f, 1.0f, 1.0f, D3DCOLOR_XRGB(0, 0, 255),},
    {520.0f, 400.0f, 1.0f, 1.0f, D3DCOLOR_XRGB(0, 255, 0),},
    {120.0f, 400.0f, 1.0f, 1.0f, D3DCOLOR_XRGB(255, 0, 0),},
};
{% endhighlight %}
Now we need to get the triangle ready for DirectX3D to use. To do this, we create what is called a vertex buffer. A vertex buffer is simply an interface that stores a section in memory (either Video RAM or system memory) to holds information about the vertices/models in your game. 
{% highlight C++ %}
// Create the vertex buffer. Here we are allocating enough memory
// (from the default pool) to hold all our 3 custom vertices. We also
// specify the FVF, so the vertex buffer knows what data it contains.
if (FAILED(g_pd3dDevice->CreateVertexBuffer(3 * sizeof(CUSTOMVERTEX),
	0, D3DFVF_CUSTOMVERTEX,
	D3DPOOL_DEFAULT, &g_pVB, NULL)))
{
	return E_FAIL;
}
{% endhighlight %}
Now we fill the vertex buffer. To do this, we need to Lock() the VB to gain access to the vertices. This mechanism is required becuase vertex buffers may be in device memory.
{% highlight C++ %}
VOID* pVertices;
if (FAILED(g_pVB->Lock(0, sizeof(vertices), (void**)&pVertices, 0)))
	return E_FAIL;
// to copy the vertices to the vertex buffer
memcpy(pVertices, vertices, sizeof(vertices)); 
g_pVB->Unlock();
{% endhighlight %}
Then drawing the primitive
{% highlight C++ %}
VOID Render()
{
    // Clear the backbuffer to a blue color
    g_pd3dDevice->Clear( 0, NULL, D3DCLEAR_TARGET, D3DCOLOR_XRGB( 0, 0, 255 ), 1.0f, 0 );

    // Begin the scene
    if( SUCCEEDED( g_pd3dDevice->BeginScene() ) )
    {
        // tells Direct3D which vertex buffer we are drawing from
        g_pd3dDevice->SetStreamSource( 0, g_pVB, 0, sizeof( CUSTOMVERTEX ) );
        //  tells Direct3D what FVF code we are using currently
        g_pd3dDevice->SetFVF( D3DFVF_CUSTOMVERTEX );
        // do the actual rendering
        g_pd3dDevice->DrawPrimitive( D3DPT_TRIANGLELIST, 0, 1 );

        // End the scene
        g_pd3dDevice->EndScene();
    }

    // Present the backbuffer contents to the display
    g_pd3dDevice->Present( NULL, NULL, NULL, NULL );
}
{% endhighlight %}

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Learning/blob/master/Vertices.cpp)

If you run this program you should get something like this:

![](/images/directX/2.png)