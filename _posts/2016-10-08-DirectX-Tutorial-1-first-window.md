---
layout: post
title: "DirectX Tutroial 1 First Window"
categories : DirectX
tags : CPP DirectX Graphics
---
* content
{:toc}

This tutorials are based on the [DirectX Tutorial](http://www.directxtutorial.com/), show how to set up IDE for using DirectX 9.

## Steps

The basic Direct3D Program, includes four basic steps:

* Create the global variable and function prototypes

```cpp
// include the basic windows header files and the Direct3D header file
#include <windows.h>
#include <windowsx.h>
#include <d3d9.h>

// include the Direct3D Library file
#pragma comment (lib, "d3d9.lib")

// global declarations
LPDIRECT3D9 d3d;    // the pointer to our Direct3D interface
LPDIRECT3DDEVICE9 d3ddev;    // the pointer to the device class

// function prototypes
void initD3D(HWND hWnd);    // sets up and initializes Direct3D
void render_frame(void);    // renders a single frame
void cleanD3D(void);    // closes Direct3D and releases memory

// the WindowProc function prototype
LRESULT CALLBACK WindowProc(HWND hWnd, UINT message, WPARAM wParam, LPARAM lParam);
```

* Create a function to initialize Direct3D and create the Direct3D Device

```cpp
// this function initializes and prepares Direct3D for use
void initD3D(HWND hWnd)
{
    d3d = Direct3DCreate9(D3D_SDK_VERSION);    // create the Direct3D interface

    D3DPRESENT_PARAMETERS d3dpp;    // create a struct to hold various device information

    ZeroMemory(&d3dpp, sizeof(d3dpp));    // clear out the struct for use
    d3dpp.Windowed = TRUE;    // program windowed, not fullscreen
    d3dpp.SwapEffect = D3DSWAPEFFECT_DISCARD;    // discard old frames
    d3dpp.hDeviceWindow = hWnd;    // set the window to be used by Direct3D

    // create a device class using this information and information from the d3dpp stuct
    d3d->CreateDevice(D3DADAPTER_DEFAULT,
          D3DDEVTYPE_HAL,
          hWnd,
          D3DCREATE_SOFTWARE_VERTEXPROCESSING,
          &d3dpp,
          &d3ddev);
}
```

Create a function to render a frame

```cpp
// this is the function used to render a single frame
void render_frame(void)
{
    // clear the window to a deep blue
    d3ddev->Clear(0, NULL, D3DCLEAR_TARGET, D3DCOLOR_XRGB(0, 40, 100), 1.0f, 0);

    d3ddev->BeginScene();    // begins the 3D scene

    // do 3D rendering on the back buffer here

    d3ddev->EndScene();    // ends the 3D scene

    d3ddev->Present(NULL, NULL, NULL, NULL);    // displays the created frame
}
```

Create a function to close Direct3D
```cpp
// this is the function that cleans up Direct3D and COM
void cleanD3D(void)
{
    d3ddev->Release();    // close and release the 3D device
    d3d->Release();    // close and release Direct3D
}
```

You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Learning/blob/master/firstDirectXWindow.cpp)

If you run this program you should get something like this:

![](/images/directX/1.png)