---
layout: default
title: Camera
nav_order: 7
parent: Scripting API
---
# Camera

## Description
The `Camera` class provides the foundation for creating camera objects in the game world. It defines basic camera properties such as field of view and background settings.

## Namespace
`Universe.Core`

## Enums

### Background
Defines the type of background the camera should render.

| Value | Description |
|-------|-------------|
| Skybox | Uses a skybox texture for the background |
| Color | Uses a solid color for the background |

## Properties

| Property    | Type       | Description                                                        |
|-------------|------------|--------------------------------------------------------------------|
| name        | string     | Name identifier for the camera (default: "Main Camera")            |
| fieldOfView | float      | The camera's field of view in degrees (default: 60)                |
| background  | Background | Type of background to render (Skybox or Color)                     |
| backColor   | rgba       | Background color when using Color background type (default: white) |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the camera with the rendering system.

## Example Usage
```csharp
// Create a standard game camera
Camera mainCamera = new Camera();
mainCamera.name = "Player Camera";
mainCamera.fieldOfView = 75; // Wider field of view
mainCamera.background = Background.Skybox;

// Create a UI camera with solid background
Camera uiCamera = new Camera();
uiCamera.name = "UI Camera";
uiCamera.fieldOfView = 60;
uiCamera.background = Background.Color;
uiCamera.backColor = [0, 0, 0, 1]; // Black background
```

## Notes
- Multiple cameras can exist in a scene, but typically only one is active for rendering
- Cameras need to be positioned and oriented using the parent object's transform
- For more advanced camera behaviors like following or orbit, use helper classes like `CameraFollower` or `FPSCameraOrbit`

## Related Components
- Works with `CameraFollower.cs` for following behaviors
- Works with `FPSCameraOrbit.cs` for first-person perspective
- Used by `Character.cs` through the `SetFollowerCamera()` method

## Dependencies
- Uses `CameraUtil.AddCamera()` to register with the rendering system
