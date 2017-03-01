---
layout: post
title: Visual Studio Tips Updated
description: Visual Studio Tips
keywords: Visual Studio
categories : [C++]
tags : [C++, Visual Studio]
---
    Check memory management to check the process

    Debug -> Windows -> Memory 
    
    then you can get the memory details

    1. check the keyboard is called

{% highlight java %}
LRESULT CALLBACK d3d::WndProc(HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam)
{
    switch (msg)
    {
    case WM_DESTROY:
        ::PostQuitMessage(0);
        break;
    case WM_CHAR:
        switch (wParam) {
            case('R'):
                Mtrls = d3d::RED_MTRL;
                break;
            case('r') :
                Mtrls = d3d::RED_MTRL;
                break;
        }
    }
    return ::DefWindowProc(hwnd, msg, wParam, lParam);
}
// note the breaks do not forget!!!!
{% endhighlight %}




