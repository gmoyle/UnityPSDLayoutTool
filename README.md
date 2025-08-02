What is the Unity PSD Layout Tool?
==================================

It is a tool used to automatically layout Photoshop Documents (.psd files) in the Unity Game Engine. 

Features
========
* Layout each PSD layer as Unity 4.3+ Sprites
  * Create Sprite animations using a set of layers as the frames in the animation
  * **Full Photoshop Blend Mode Support**: Automatically applies all 16 Photoshop blend modes to Unity materials with mathematically accurate shaders
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

Blend Mode Support
==================
The Unity PSD Layout Tool provides **complete Photoshop blend mode compatibility** with mathematically accurate shader implementations. All 16 standard Photoshop blend modes are supported and automatically applied during import.

## Supported Blend Modes

### Basic Blend Modes
| Blend Mode | Photoshop Key | Description | Implementation |
|------------|---------------|-------------|----------------|
| **Normal** | `norm` | Standard alpha blending | Unity default material |
| **Multiply** | `mult` | Darkens by multiplying colors | Custom multiply shader |
| **Screen** | `scrn` | Lightens by inverting, multiplying, and inverting again | Custom screen shader |
| **Overlay** | `over` | Combines multiply and screen based on base color | Custom overlay shader |

### Light Blend Modes
| Blend Mode | Photoshop Key | Description | Implementation |
|------------|---------------|-------------|----------------|
| **Soft Light** | `sLit` | Softer version of overlay | Custom soft light shader |
| **Hard Light** | `hLit` | Combines multiply and screen based on blend color | Custom hard light shader |
| **Color Dodge** | `cDdg` | Brightens base color by decreasing contrast | Custom color dodge shader |
| **Color Burn** | `cBrn` | Darkens base color by increasing contrast | Custom color burn shader |

### Comparative Blend Modes
| Blend Mode | Photoshop Key | Description | Implementation |
|------------|---------------|-------------|----------------|
| **Darken** | `dark` | Selects the darker of base and blend colors | Custom darken shader |
| **Lighten** | `lite` | Selects the lighter of base and blend colors | Custom lighten shader |
| **Difference** | `diff` | Subtracts darker color from lighter color | Custom difference shader |
| **Exclusion** | `smud` | Similar to difference but with lower contrast | Custom exclusion shader |

### HSV-Based Blend Modes
| Blend Mode | Photoshop Key | Description | Implementation |
|------------|---------------|-------------|----------------|
| **Hue** | `hue ` | Uses hue from blend, saturation/value from base | HSV color space conversion shader |
| **Saturation** | `sat ` | Uses saturation from blend, hue/value from base | HSV color space conversion shader |
| **Color** | `colr` | Uses hue/saturation from blend, value from base | HSV color space conversion shader |
| **Luminosity** | `lum ` | Uses value from blend, hue/saturation from base | HSV color space conversion shader |

## Technical Implementation

### Sprite Renderers
For sprite-based layouts, blend modes are applied by:
1. **Automatic Detection**: The tool reads the blend mode key from each PSD layer
2. **Material Creation**: Custom materials are created using the appropriate blend mode shader
3. **Shader Assignment**: The material is automatically assigned to the sprite renderer

### UI Elements
For Unity UI layouts, blend modes are handled with:
- **Limited Support**: Basic blend modes (Multiply, Screen, Overlay, Soft Light, Hard Light) work with UI materials
- **Fallback Behavior**: Advanced blend modes fall back to normal rendering for UI elements due to UI rendering pipeline limitations

### Shader Quality
- **Mathematical Accuracy**: All shaders implement the exact mathematical formulas used by Photoshop
- **Color Space Conversion**: HSV-based blend modes include proper RGB↔HSV conversion functions
- **Performance Optimized**: Shaders are optimized for real-time rendering while maintaining accuracy
- **Unity Compatible**: All shaders follow Unity's sprite shader conventions and support standard features

## Usage Notes

### Automatic Application
Blend modes are automatically applied during import - no manual configuration required:
```
1. Import your PSD file into Unity
2. Select the PSD file in the Project window
3. Use "Layout in Current Scene" or "Generate Prefab" 
4. Blend modes are automatically detected and applied
```

### Performance Considerations
- **Shader Compilation**: First use of each blend mode may cause a brief shader compilation
- **Draw Calls**: Each unique blend mode creates a separate draw call
- **Mobile Performance**: Complex blend modes (HSV-based) may impact performance on low-end mobile devices

### Troubleshooting
- **Missing Shaders**: If blend mode shaders are missing, the tool falls back to Unity's default sprite material
- **Warning Messages**: Check the Console for any blend mode application warnings
- **Unexpected Results**: Ensure your PSD layers use standard Photoshop blend modes (custom blend modes are not supported)
