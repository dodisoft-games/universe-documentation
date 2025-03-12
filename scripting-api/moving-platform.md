---
layout: default
title: MovingPlatform
nav_order: 29
parent: Scripting API
---
# MovingPlatform

## Description
The `MovingPlatform` class is a core component for creating movable platforms that can carry characters and other objects. It handles the physics integration needed to ensure objects move correctly with the platform.

## Namespace
`Universe.Tools`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| position | vector3 | Current world position of the platform |
| rotation | quaternion | Current world rotation of the platform |
| uni | UniObject | Reference to the object this script is attached to |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Gets a reference to the object, stores its initial position and rotation, and registers the platform with the physics system.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the stored position and rotation of the platform to track its movement.

## Example Usage
```csharp
// Create a basic moving platform
MovingPlatform elevatorPlatform = new MovingPlatform();
// The platform will be registered with the physics system automatically
// Movement is typically controlled by another component like DirectionalPlatform or CinematicMotion

// Create a platform with custom movement logic
MovingPlatform customPlatform = new MovingPlatform();

// In a custom script:
void MoveCustomPlatform() {
    // Move the platform
    customPlatform.uni.position = CalculateNewPosition();
    customPlatform.uni.rotation = CalculateNewRotation();
    
    // The MovingPlatform component will handle the physics and carrying objects
}
```

## Technical Details
- The `MovingPlatform` component itself doesn't control movement; it only tracks changes
- The actual movement logic is typically implemented in other components like `DirectionalPlatform` or custom scripts
- The platform registers with `GameUtil.AddMovingPlatform()` to integrate with the physics system
- When a character or object stands on the platform, the physics system will move them along with the platform
- Position and rotation are tracked every frame to calculate velocity and apply it to objects on the platform

## Use Cases
- Elevators moving up and down
- Horizontal moving platforms between areas
- Rotating or tilting platforms
- Complex moving obstacles
- Moving vehicles or mounts that characters can ride
- Platforms that follow paths or splines

## Notes
- For simple oscillating movement, combine with `DirectionalPlatform`
- For complex path following, combine with `CinematicMotion`
- For networked games, ensure proper synchronization of platform movement
- Performance impact is generally low, but many platforms with complex colliders could affect physics performance
- Objects need appropriate colliders to be correctly carried by the platform

## Related Components
- Often used with `DirectionalPlatform.cs` for oscillating movement
- Can be used with `CinematicMotion.cs` for path-following movement
- Works with all collider types for platform collision shape

## Dependencies
- Uses `UniObjectUtil` to access transform information
- Uses `GameUtil.AddMovingPlatform()` to register with the physics system
