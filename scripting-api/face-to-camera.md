---
layout: default
title: FaceToCamera
nav_order: 17
parent: Scripting API
---
# FaceToCamera

## Description
The `FaceToCamera` class makes an object automatically rotate to face the active camera. This is useful for billboarding effects like particle sprites, UI elements in 3D space, or objects that should always face the player.

## Namespace
`Universe.Helper`

## Fields

| Field | Type      | Description                                        |
|-------|-----------|----------------------------------------------------|
| uni   | UniObject | Reference to the object this script is attached to |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Gets a reference to the UniObject this script is attached to.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the object's rotation to face away from the active camera's position.

## Example Usage
```csharp
// Make a health bar always face the camera
FaceToCamera healthBarBillboard = new FaceToCamera();

// Make a 2D sprite in 3D space always face the camera
FaceToCamera spriteController = new FaceToCamera();

// Make an information sign always readable to the player
FaceToCamera signController = new FaceToCamera();
```

## Implementation Details
- The object will rotate so that its forward direction points away from the camera
- The rotation happens every frame in the `OnUpdate` method
- The script uses a "look at" approach where the object points toward a position that's on the opposite side of the object from the camera
- If no active camera is found, the rotation remains unchanged

## Use Cases
- 2D sprites in a 3D world (like particles, icons, or markers)
- UI elements positioned in 3D space
- Trees or other objects using billboard techniques for optimization
- Signs or text that should always be readable to the player
- Character name tags or status indicators

## Notes
- For objects that should face the camera but maintain their up direction, a different approach would be needed
- This is a simple approach that works well for most billboarding needs
- For more complex billboard effects with constraints, consider implementing a custom solution

## Dependencies
- Uses `UniObjectUtil` to access the object's transform
- Uses `CameraUtil.GetActiveCameraPosition()` to find the current camera position
