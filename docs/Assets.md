# Asset Management Guide for Multi-Platform App Development

## Overview

This guide outlines our streamlined approach to asset management for cross-platform app development. Our system is designed to balance flexibility across different devices while minimizing asset complexity.

Your app will run seamlessly across:
- iOS (iPhone, iPad)
- Android (phones and tablets)
- Mac
- Windows
- Linux

## Configuration System

### The config.json File

All settings related to display and layout are controlled through the `config.json` file. This configuration is set at **build time** and determines how your app will handle different aspect ratios, orientations, and resolution targets.

```json
{
  "portrait": true,
  "landscape": false,
  "19_9": true,
  "16_9": true,
  "4_3": true,
  "resolution": "medium"
}
```

### Configuration Options

| Parameter | Description | Options |
|-----------|-------------|---------|
| `portrait` | Enable portrait orientation | `true` or `false` |
| `landscape` | Enable landscape orientation | `true` or `false` |
| `19_9` | Support for 19:9 aspect ratio (modern phones) | `true` or `false` |
| `16_9` | Support for 16:9 aspect ratio (standard displays) | `true` or `false` |
| `4_3` | Support for 4:3 aspect ratio (tablets, productivity) | `true` or `false` |
| `resolution` | Target resolution for the app | `"low"`, `"medium"`, `"high"`, or `"ultra"` |

## Resolution Settings

| Setting | Target Resolution | Best For |
|---------|------------------|----------|
| `"low"` | 720p equivalent | Fast-paced games, maximum performance |
| `"medium"` | 1080p equivalent | Balanced performance and quality |
| `"high"` | 1440p equivalent | Detailed graphics, modern devices |
| `"ultra"` | 4K equivalent | Maximum visual fidelity, high-end devices |

## Asset Organization

Structure your assets according to this folder hierarchy:

```
/views
  /common       # Scale independent assets
    /common         # Rotation-independent assets
    /portrait
    /landscape
  /19_9
    /common
    /portrait
    /landscape
  /16_9
    /common
    /portrait
    /landscape
  /4_3
    /common
    /portrait
    /landscape
```

If your app supports only a single scale and rotation -or- all images are scale and rotation independent then all images can the stored in the root asset folder:
```
/objects         # all images store in the root of the objects folder
```

If your app support 2 aspect ratios with only a single rotatation the images can be stored at the root of each of the sub folders:
```
/views            # common images stored here
  /19_9           # 19:9 specific images
  /4_3            # 4:3 specific images
```

## How It Works

### Build Time vs. Runtime

- **Build Time**: The `resolution` setting determines the target resolution for your entire application.
- **Runtime**: The engine detects the device's aspect ratio and orientation, then loads assets from the appropriate subfolder.

### Asset Selection Process

1. When your app launches, the engine identifies the device's aspect ratio and orientation
2. It selects the appropriate asset folder based on this identification
3. Assets are scaled to match the hardware resolution determined by your `resolution` setting

### Smart Scaling

The engine will intelligently scale your assets to match the device's actual resolution while maintaining your target performance level:

- If a user has a high-resolution device but you've set `"resolution": "low"`, your assets will be upscaled to fit the screen but maintain the performance benefits of lower-resolution assets
- If a user has a lower-resolution device but you've set `"resolution": "high"`, your assets will be rendered at the maximum resolution the device supports

## Best Practices

### Universal Assets

Place assets that work across all aspect ratios and can be simply scaled in the `/common` folder:
- UI elements
- Character sprites
- Icons
- Small decorative elements

### Layout-Specific Assets

Place assets that need to be tailored to specific aspect ratios in the appropriate `/layouts` subfolder:
- Background images
- Level designs
- Screen-filling UI layouts
- Position-sensitive elements

### Resolution Considerations

- **Fast-paced games**: Use the `"low"` or `"medium"` setting to prioritize performance
- **Detail-oriented games**: Use the `"high"` or `"ultra"` setting for maximum visual clarity
- **General apps**: The `"medium"` setting offers a good balance for most applications

## Support Notes

- Modern smartphones typically use 19:9 or 20:9 aspect ratios (our system uses 19:9 with slight letterboxing when needed)
- Most monitors and TVs use 16:9
- Tablets, Surface devices, and some professional displays use 4:3 or similar
- Most laptops use 16:9 or 16:10 (16:10 devices will display 16:9 content with slight letterboxing)

By supporting these three core aspect ratios (19:9, 16:9, and 4:3), your app will provide good coverage across virtually all modern devices while maintaining a manageable asset library.

## System folders
Assets that are used by the engine can optionally be stored in ./system sub folders:
```
/objects         # all images store in the root of the objects folder
  /system        # cursor images
```
