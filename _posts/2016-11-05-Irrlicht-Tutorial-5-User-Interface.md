---
layout: post
title: "Irrlicht Tutroial 5 User Interface"
categories : Irrlicht
tags : CPP Irrlicht Graphics
---
* content
{:toc}
  
This tutorials are based on the [irrlicht tutorial](http://irrlicht.sourceforge.net/docu), show how to create and use windows, buttons, scroll bars, static texts, and list boxes.. You have to read the previous tutorials, because the tutorials will skips the knowledgement that we have already talked about before.

Declare a structure to hold some context for the event receiver and some values that we'll use to identify individual GUI controls.
```cpp
struct SAppContext
{
    IrrlichtDevice *device;
    s32             counter;
    IGUIListBox*    listbox;
};

enum
{
    GUI_ID_QUIT_BUTTON = 101,
    GUI_ID_NEW_WINDOW_BUTTON,
    GUI_ID_FILE_OPEN_BUTTON,
    GUI_ID_TRANSPARENCY_SCROLL_BAR
};
```
Change the transparency of the windows when you drag the scrollbar
```cpp
void setSkinTransparency(s32 alpha, irr::gui::IGUISkin * skin)
{
    for (s32 i=0; i<irr::gui::EGDC_COUNT ; ++i)
    {
        video::SColor col = skin->getColor((EGUI_DEFAULT_COLOR)i);
        col.setAlpha(alpha);
        skin->setColor((EGUI_DEFAULT_COLOR)i, col);
    }
}
```
In this example, We only react to gui events, and if it's such an event, we get the id of the caller (the gui element which caused the event) and get the pointer to the gui environment.
```cpp
class MyEventReceiver : public IEventReceiver
{
public:
MyEventReceiver(SAppContext & context) : Context(context) { }
//SEvents hold information about an event
virtual bool onEvent(const SEvent& event) {
	// We only react to gui events
	if (event.EventType == EET_GUI_EVENT) {
		s32 id = event.GUIEvent.Caller->getID();
		IGUIEnvironment* env = Context.device->getGUIEnvironment();
		switch(event.GUIEvent.EventType) {
			/* GUI_ID_TRANSPARENCY_SCROLL_BAR to change the transparency of the skins, as long as we get the scroll value as the alpha value */
			case EGET_SCROLL_BAR_CHANGED:
				if (id == GUI_ID_TRANSPARENCY_SCROLL_BAR)
				{
					s32 pos = ((IGUIScrollBar*)event.GUIEvent.Caller)->getPos();
					setSkinTransparency(pos, env->getSkin());
				}
				break;
			// if it is a button
			case EGET_BUTTON_CLICKED:
				switch(id) {
					case GUI_ID_QUIT_BUTTON:
						Context.device->closeDevice();
						return true;

					case GUI_ID_NEW_WINDOW_BUTTON:
					{
						// add the text to the list box
						Context.listbox->addItem(L"Window created"); 
						Context.counter += 30;
						if (Context.counter > 200)
							Context.counter = 0;
						// create a new window with name "test window"
						IGUIWindow* window = env->addWindow(
							rect<s32>(100 + Context.counter, 100 + Context.counter, 300 + Context.counter, 200 + Context.counter),
							false, // modal?
							L"Test window");
						env->addStaticText(L"Please close me",
							rect<s32>(35,35,140,50),
							true, // border?
							false, // wordwrap?
							window);
					}
					return true;

					case GUI_ID_FILE_OPEN_BUTTON:
						Context.listbox->addItem(L"File open");
						// file open dialog
						env->addFileOpenDialog(L"Please choose a file.", true, 0, -1, true);
						return true;
					default:
						return false;
				}
				break;

			case EGET_FILE_SELECTED:
			{
				IGUIFileOpenDialog* dialog =
					(IGUIFileOpenDialog*)event.GUIEvent.Caller;
				Context.listbox->addItem(dialog->getFileName());
			}
			break;

			default:
				break;
		}
	}
	return false;
}

private:
SAppContext & Context;
};
```
Then it's the main part, just like the pevious example. And add the GUI environment pointer.
```cpp
IGUIEnvironment* env = device->getGUIEnvironment();
```
Load Skin and font        
```cpp
	IGUISkin* skin = env->getSkin();
IGUIFont* font = env->getFont("../../media/fonthaettenschweiler.bmp");
if (font)
    skin->setFont(font);

skin->setFont(env->getBuiltInFont(), EGDF_TOOLTIP);
```
Add buttons
```cpp
env->addButton(rect<s32>(10,240,110,240 + 32), 0, GUI_ID_QUIT_BUTTON,
        L"Quit", L"Exits Program");
env->addButton(rect<s32>(10,280,110,280 + 32), 0, GUI_ID_NEW_WINDOW_BUTTON,
        L"New Window", L"Launches a new Window");
env->addButton(rect<s32>(10,320,110,320 + 32), 0, GUI_ID_FILE_OPEN_BUTTON,
        L"File Open", L"Opens a file");
```
Add scrollbar
```cpp
env->addStaticText(L"Transparent Control:", rect<s32>(150,20,350,40), true);
IGUIScrollBar* scrollbar = env->addScrollBar(true,
		rect<s32>(150, 45, 350, 60), 0, GUI_ID_TRANSPARENCY_SCROLL_BAR);
scrollbar->setMax(255);
scrollbar->setPos(255);
setSkinTransparency( scrollbar->getPos(), env->getSkin());
// set scrollbar position to alpha value of an arbitrary element
scrollbar->setPos(env->getSkin()->getColor(EGDC_WINDOW).getAlpha());
```
Add listbox and editbox
```cpp
env->addStaticText(L"Logging ListBox:", rect<s32>(50,110,250,130), true);
IGUIListBox * listbox = env->addListBox(rect<s32>(50, 140, 250, 210));
env->addEditBox(L"Editable Text", rect<s32>(350, 80, 550, 100));
```
```cpp
// Store the appropriate data in a context structure.
SAppContext context;
context.device = device;
context.counter = 0;
context.listbox = listbox;

// Then create the event receiver, giving it that context structure.
MyEventReceiver receiver(context);

// And tell the device to use our custom event receiver.
device->setEventReceiver(&receiver);


// create a nice Irrlicht Engine logo in the top left corner. 
env->addImage(driver->getTexture("../../media/irrlichtlogo2.png"),
		position2d<int>(10,10));
```
Done, Draw everything


You can get the complete codes from [Github](https://github.com/Shanshan-IC/DirectX-Irrlicht-Tutorial/tree/master/Irrlicht-examples/05.UserInterface)