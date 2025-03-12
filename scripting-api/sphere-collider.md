---
layout: default
title: SphereCollider
nav_order: 44
parent: Scripting API
---
# SphereCollider

## Description
The `SphereCollider` class implements a spherical collision volume for physics interactions. It's useful for simple objects, characters, or trigger areas that can be approximated with a sphere shape. Sphere colliders are computationally efficient and provide smooth collision responses.

## Namespace
`Universe.Core`

## Properties
| Property | Type     | Description                                                                                            |
|----------|----------|--------------------------------------------------------------------------------------------------------|
| trigger  | bool     | When true, the collider acts as a trigger that detects overlaps but doesn't create physical collisions |
| center   | vector3  | The local center position offset of the sphere collider                                                |
| radius   | float    | The radius of the sphere (default: 0.5)                                                                |
| attitude | Attitude | The physical material properties of the collider (affects bounce, friction, etc.)                      |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the sphere collider with the physics system.

## Example Usage
```csharp
// Create a basic sphere collider for a ball
SphereCollider ballCollider = new SphereCollider();
ballCollider.radius = 0.25; // 25cm radius
ballCollider.trigger = false; // Solid physical collider
ballCollider.attitude = Attitude.HighBouncing; // Bouncy material

// Create a larger trigger area for detection
SphereCollider detectionZone = new SphereCollider();
detectionZone.radius = 5; // 5 meter detection radius
detectionZone.center = [0, 1, 0]; // Centered 1 meter above the object's origin
detectionZone.trigger = true; // Just for overlap detection

// Create a character collider
SphereCollider characterCollider = new SphereCollider();
characterCollider.radius = 0.5; // Body radius
characterCollider.center = [0, 1, 0]; // Centered at character's middle
characterCollider.attitude = Attitude.SemiAbsorbing; // Some bounce absorption
```

## Technical Details
- A sphere collider is defined by a center point and a radius
- The center is specified in local coordinates relative to the object's position
- Sphere colliders are the simplest and most efficient 3D collision shape
- They provide consistent collision response from all directions
- When `trigger` is true, collisions will generate trigger events but won't cause physical reactions
- The `attitude` property affects physical properties like bounciness

## Use Cases
- Simple rounded objects like balls, projectiles, or gems
- Character colliders for basic collision detection
- Trigger zones for ability effects, sound triggers, or detection areas
- Approximating simple objects for better performance
- Smooth-rolling objects that need consistent collision behavior
- Particle collision in physics simulations

## Notes
- For character colliders, consider using CapsuleCollider which better fits humanoid shapes
- Sphere colliders are very efficient for performance, so prefer them for simple objects
- For complex shapes, consider using multiple sphere colliders or switch to mesh colliders
- The sphere's radius affects both the collision detection and physics behavior
- For most accurate results, position the center at the object's visual center

## Related Components
- Alternative to `BoxCollider.cs`, `CapsuleCollider.cs`, and `MeshCollider.cs`
- Works with `Physics.cs` for physical interactions

## Dependencies
- Uses `ColliderUtil.AddSphereCollider()` to register with the physics system
