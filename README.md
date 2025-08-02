What is the Unity PSD Layout Tool?
==================================

It is a tool used to automatically layout Photoshop Documents (.psd files) in the Unity Game Engine. 

Features
========
* Layout each PSD layer as Unity 4.3+ Sprites
  * Create Sprite animations using a set of layers as the frames in the animation
  * **Photoshop Blend Mode Support**: Automatically applies layer blend modes (Normal, Multiply, Screen, Overlay, etc.) to Unity materials
  * **Layer Opacity Support**: Preserves Photoshop layer opacity settings in Unity
  * **Invisible Layer Filtering**: Skips invisible layers during import to match Photoshop visibility
* Layout each PSD Layer as Unity 4.6+ UI elements
  * Create Button objects using a set of layers as the button states
  * **UI Text Support**: Creates proper UI Text components from Photoshop text layers
* Generate a single prefab with the entire layout (Sprites or UI)
* Export each PSD Layer as a .png file on the hard drive
  * Useful for simply updating textures without creating an entire layout

How to Install
==============
Simply copy the files into your project.  A .unitypackage file will be provided in the future.

How to Use
==========
The PSD Layout Tool is implemented as a Unity Custom Inspector.  If you select a PSD file that you have in your project (Assets folder) special buttons will appear above the default importer settings.

![](screenshots/inspector.png?raw=true)

* **Maximum Depth**
  * The maximum depth value (Z position) to use when laying the layers out.  The front-most layer (minimum depth) is always 0.
* **Pixels to Unity Units**
  * The scale to use when generating Unity Sprites, in pixels to Unity world units (meters).
* **Use Unity UI**
  * Check to generate Unity 4.6+ UI elements instead of "normal" GameObjects.
* **Export Layers as Textures**
  * Creates a .png image file for each layer in the PSD file, using the same folder structure.
* **Layout in Current Scene**
  * Creates a Unity 4.3+ Sprite object for each layer in the PSD file.  It is laid out to match the PSD's layout and folder structure.
* **Generate Prefab**
  * Identical to the previous option, but it generates a .prefab file instead of putting the objects in the scene.

Special Tags
==========
Layers can have special tags applied to them that flags them to have the layout tool perform special operations on them.

### Group Layer Tags ###

|        Tag        | Description |
| ----------------- | ----------- |
|  &#124;Animation  |  Creates a Sprite animation using all of the children layers as frames |
|  &#124;FPS=##     |  The number of frames per second to use for a Sprite animation.  Defaults to 30 if not present  | 
|  &#124;Button     |  Creates a Button object using any tagged children layers as the button states |

### Art Layer Tags ###

|        Tag          | Description |
| -----------------   | ----------- |
|  &#124;Disabled     |  Represents the disabled state of a button     |
|  &#124;Highlighted  |  Represents the highlighted state of a button  | 
|  &#124;Pressed      |  Represents the pressed state of a button  | 
|  &#124;Default      |  Represents the default/enabled/normal/up state of a button  | 
|  &#124;Enabled      |  Represents the default/enabled/normal/up state of a button  |
|  &#124;Normal       |  Represents the default/enabled/normal/up state of a button  |
|  &#124;Up           |  Represents the default/enabled/normal/up state of a button  |
|  &#124;Text         |  Represents a **texture** that is the text of a button (normal text layers import without this tag)  |

Photoshop Compatibility
=======================
Smart Objects are supported, and do not need to be flattened/rasterized in Photoshop before importing.
