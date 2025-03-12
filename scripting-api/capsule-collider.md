---
layout: default
title: CapsuleCollider
nav_order: 8
parent: Scripting API
---
# CapsuleCollider

## Description
The `CapsuleCollider` class implements a capsule-shaped collision volume for physics interactions. A capsule is a cylinder with hemispherical ends, making it ideal for character controllers and objects where smooth collision responses are desired.

## Namespace
`Universe.Core`

## Enums

### Axis
Defines the orientation axis of the capsule.

| Value | Description |
|-------|-------------|
| X | The capsule's length runs along the X axis |
| Y | The capsule's length runs along the Y axis (default) |
| Z | The capsule's length runs along the Z axis |

## Properties
| Property  | Type     | Description                                                                                            |
|-----------|----------|--------------------------------------------------------------------------------------------------------|
| trigger   | bool     | When true, the collider acts as a trigger that detects overlaps but doesn't create physical collisions |
| direction | Axis     | The axis along which the capsule is oriented (default: Y)                                              |
| center    | vector3  | The local center position offset of the capsule collider                                               |
| radius    | float    | The radius of the capsule (default: 0.5)                                                               |
| height    | float    | The total height of the capsule including the two hemisphere ends (default: 2)                         |
| attitude  | Attitude | The physical material properties of the collider (affects bounce, friction, etc.)                      |


## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the capsule collider with the physics system.

## Example Usage
```csharp
// Create a character controller collider
CapsuleCollider characterCollider = new CapsuleCollider();
characterCollider.radius = 0.5;
characterCollider.height = 2.0; // Typical human height
characterCollider.direction = Axis.Y; // Up/down orientation
characterCollider.center = [0, 1, 0]; // Center at character's middle (assuming origin is at feet)
characterCollider.trigger = false; // Solid physical collider
characterCollider.attitude = Attitude.SemiAbsorbing; // Slight bounce absorption

// Create a trigger zone
CapsuleCollider detectionZone = new CapsuleCollider();
detectionZone.radius = 5;
detectionZone.height = 3;
detectionZone.trigger = true; // Just for overlap detection
```

## Notes
- Capsule colliders are ideal for character controllers as they handle slopes and stair-stepping well
- The actual capsule consists of a cylinder with length (height - 2*radius) and two hemisphere ends
- When `direction` is Axis.Y, the capsule extends along the Y axis
- For proper collision detection, at least one of the colliding objects should have a `Physics` component
- When `trigger` is true, collisions will generate trigger events but won't cause physical reactions

## Related Components
- Works well with `Character.cs` for character collision
- Complements `Physics.cs` for physical interactions

## Dependencies
- Uses `ColliderUtil.AddCapsuleCollider()` to register with the physics system
