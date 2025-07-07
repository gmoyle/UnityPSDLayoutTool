# Unity PSD Layout Tool

[![Basic CI - No Unity License Required](https://github.com/gmoyle/UnityPSDLayoutTool/actions/workflows/basic-ci.yml/badge.svg)](https://github.com/gmoyle/UnityPSDLayoutTool/actions/workflows/basic-ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE.md)
[![Unity 2018.1+](https://img.shields.io/badge/Unity-2018.1%2B-blue.svg)](https://unity3d.com)

A lightweight Photoshop Unity import tool for rapid prototyping and scene building with cross-Unity version compatibility.

## 🎯 Features

* **Multi-Unity Support**: Works with Unity 2018.1+ (including 2019, 2020, 2021, 2022+)
* **Layout PSD layers as Unity Sprites** with proper positioning and pivot handling
  * Create Sprite animations using layer sets as animation frames
* **Unity UI Integration** - Generate Unity UI elements instead of standard GameObjects
  * Create Button objects with multiple states from layer groups
* **Flexible Output Options**:
  * Generate prefabs for reusable assets
  * Layout directly in current scene
  * Export individual layers as PNG textures
* **Enhanced Positioning**: Improved pivot and canvas-based positioning system
* **Package Manager Ready**: Distributed as a proper Unity package

## 📦 Installation

### Option 1: Unity Package Manager (Recommended)
1. Open Unity Package Manager
2. Click "+" → "Add package from git URL"
3. Enter: `https://github.com/gmoyle/UnityPSDLayoutTool.git`

### Option 2: Download Release
1. Go to [Releases](https://github.com/gmoyle/UnityPSDLayoutTool/releases)
2. Download the latest `.unitypackage` file
3. Import into your Unity project

### Option 3: Manual Installation
Simply copy the `Assets/PSD Layout Tool` folder into your project's Assets directory.

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

## 📷 Photoshop Compatibility

Photoshop's "Smart Objects" are not supported, and therefore must be flattened/rasterized in Photoshop before attempting to import.

1. Click **Layer** in the Photoshop menu
2. Click **Rasterize**
3. Click **All Layers**

![](screenshots/photoshop.jpg?raw=true)

## 🔧 Development & Contributing

### CI/CD Pipeline
This repository uses GitHub Actions for continuous integration:

- **Basic CI**: Runs on every push/PR - validates package structure and code syntax
- **Full CI**: Unity compilation testing across multiple versions (requires Unity license)
- **Release Automation**: Creates packages and GitHub releases on version tags

### Running Locally
1. Clone the repository
2. Open with Unity 2018.1 or newer
3. Make your changes
4. Test with sample PSD files

### Setting Up CI/CD
For full Unity testing capabilities, see [GitHub Secrets Setup](.github/SETUP_SECRETS.md).

### Creating a Release
1. Update version in `Assets/PSD Layout Tool/package.json`
2. Commit and push changes
3. Create a new tag: `git tag v1.0.4 && git push origin v1.0.4`
4. GitHub Actions will automatically create the release

## 📋 Version Compatibility

| Unity Version | Status | Notes |
|---------------|-----------|-------|
| 2022.x | ✅ Tested | Full support |
| 2021.x | ✅ Tested | Full support |
| 2020.x | ✅ Tested | Full support |
| 2019.x | ✅ Tested | Full support |
| 2018.1+ | ✅ Tested | Full support |
| 2017.x | ⚠️ Limited | May work but not tested |
| Unity 5 | ⚠️ Legacy | Legacy support only |
| Unity 4 | ⚠️ Legacy | Legacy support only |

## 🐛 Issues & Support

- **Bug Reports**: Please use [GitHub Issues](https://github.com/gmoyle/UnityPSDLayoutTool/issues)
- **Feature Requests**: Submit via GitHub Issues with the "enhancement" label
- **Questions**: Check existing issues first, then create a new one

## 📄 License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.

## 🙏 Acknowledgments

- Original work by [GlitchEnzo](https://github.com/GlitchEnzo/UnityPSDLayoutTool)
- Enhanced with Unity 2020+ compatibility and improved error handling
- CI/CD pipeline and package management improvements
