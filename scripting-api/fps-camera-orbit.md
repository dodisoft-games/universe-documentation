---
layout: default
title: FPSCameraOrbit
nav_order: 18
parent: Scripting API
---
# FPSCameraOrbit

## Description
The `FPSCameraOrbit` class implements a first-person camera system with mouse-look functionality. It handles camera rotation around a character, positioning and smoothing, and can be configured with sensitivity and angle constraints.

## Namespace
`Universe.Helper`

## Properties
| Property     | Type      | Description                                                          |
|--------------|-----------|----------------------------------------------------------------------|
| character    | UniObject | The character object that the camera orbits around                   |
| fpsCamera    | UniObject | The camera object to control                                         |
| bindTarget   | UniObject | Position target for the camera (where the camera should be)          |
| lookTarget   | UniObject | Look target for the camera (what the camera should look at)          |
| xSensitivity | float     | Horizontal rotation sensitivity (default: 10)                        |
| ySensitivity | float     | Vertical rotation sensitivity (default: 10)                          |
| minY         | float     | Minimum vertical angle in degrees (default: -75)                     |
| maxY         | float     | Maximum vertical angle in degrees (default: 75)                      |
| moveSpeed    | float     | Speed at which the camera moves to its target position (default: 4)  |
| lookSpeed    | float     | Speed at which the camera rotates to look at its target (default: 4) |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the component by getting a reference to the object it's attached to.

### UpdateRotation
```csharp
void UpdateRotation(vector3 rotation)
```
Updates the camera rotation based on input (typically from mouse movement).

#### Parameters
- `rotation`: Rotation delta values, typically from mouse input

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates camera position and look direction based on configuration.

## Example Usage
```csharp
// Create standard first-person camera setup
FPSCameraOrbit fpsController = new FPSCameraOrbit();
fpsController.character = playerCharacter;
fpsController.fpsCamera = mainCamera;
fpsController.xSensitivity = 8;
fpsController.ySensitivity = 8;
fpsController.minY = -60;
fpsController.maxY = 60;

// Connect to input system
InputController input = new InputController();
input.OnAxisEvent += (panel, sender, action, direction) => {
    if (action == "Look") {
        fpsController.UpdateRotation(direction);
    }
};

// Create a camera with position smoothing
FPSCameraOrbit smoothCamera = new FPSCameraOrbit();
smoothCamera.character = playerCharacter;
smoothCamera.fpsCamera = mainCamera;
smoothCamera.bindTarget = cameraSocket; // Position where camera should be
smoothCamera.moveSpeed = 5; // Higher for faster camera movement
```

## Implementation Details
- The vertical (pitch) rotation is applied to the FPSCameraOrbit object
- The horizontal (yaw) rotation is applied to the character
- The `y` field stores the current vertical angle, clamped between minY and maxY
- If bindTarget is set and moveSpeed > 0, the camera will smoothly move toward that position
- If lookTarget is set and lookSpeed > 0, the camera will smoothly rotate to look at that target

## Use Cases
- First-person games and perspectives
- Orbit cameras for character customization
- Over-the-shoulder third-person cameras
- Aim-down-sights camera transitions

## Notes
- For proper first-person controls, this component should be connected to an input system
- The min/max Y values prevent the camera from flipping over (common in FPS games)
- For third-person cameras, consider using CameraFollower instead
- The character should have proper rotation methods to work with the horizontal rotation

## Dependencies
- Uses `UniObjectUtil` to access transform information
- Uses `Time.DeltaTime()` for smooth movement
- Uses `VectorUtil` for vector operations
