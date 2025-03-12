---
layout: default
title: CameraFollower
nav_order: 6
parent: Scripting API
---
# CameraFollower

## Description
The `CameraFollower` class provides functionality for a camera to follow a target object with smooth movement and positioning. It's useful for creating third-person camera systems or any camera that needs to track an object.

## Namespace
`Universe.Helper`

## Properties
| Property  | Type      | Description                                                              |
|-----------|-----------|--------------------------------------------------------------------------|
| target    | UniObject | The object to follow                                                     |
| safeZone  | float     | Minimum distance to maintain from the target (default: 1)                |
| distance  | float     | Desired follow distance from the target (default: 3)                     |
| height    | float     | Height offset above the target (default: 2)                              |
| moveSpeed | float     | Speed at which the camera moves to catch up with the target (default: 1) |
| lookSpeed | float     | Speed at which the camera rotates to look at the target (default: 8)     |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Gets a reference to the object this script is attached to.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the camera position and rotation to follow the target.

## Example Usage
```csharp
// Create a third-person camera that follows the player
CameraFollower thirdPersonCam = new CameraFollower();
thirdPersonCam.target = playerCharacter;
thirdPersonCam.distance = 5; // Further back
thirdPersonCam.height = 2.5; // Slightly higher
thirdPersonCam.moveSpeed = 3; // More responsive movement
thirdPersonCam.lookSpeed = 5; // Moderate rotation speed

// Create a top-down camera
CameraFollower topDownCam = new CameraFollower();
topDownCam.target = playerCharacter;
topDownCam.distance = 1; // Closer horizontally
topDownCam.height = 15; // High above
topDownCam.moveSpeed = 2;
topDownCam.lookSpeed = 10; // Quick to reorient
```

## Implementation Details
- The camera will position itself behind the target by calculating the target's forward direction
- The `safeZone` ensures the camera maintains at least this distance from the target
- When `moveSpeed` is greater than 0, the camera position will smoothly interpolate to follow the target
- When `lookSpeed` is greater than 0, the camera will gradually rotate to look at the target
- Setting either speed to 0 will disable the respective movement/rotation
- The camera avoids moving straight up or down by projecting the direction onto the up vector

## Notes
- This component should be attached to a camera object
- For best results, the camera should have a clear `Camera` component 
- For first-person camera handling, consider using `FPSCameraOrbit` instead

## Dependencies
- Uses `UniObjectUtil` to access transform information
- Uses `VectorUtil` for mathematical operations
