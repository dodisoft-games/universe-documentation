---
layout: default
title: MeshCollider
nav_order: 27
parent: Scripting API
---
# MeshCollider

## Description
The `MeshCollider` class implements a collision volume that precisely matches the shape of a 3D mesh. It provides the most accurate collision detection for complex shapes but is typically more computationally expensive than primitive colliders like Box, Sphere, or Capsule.

## Namespace
`Universe.Core`

## Properties

| Property | Type     | Description                                                                                            |
|----------|----------|--------------------------------------------------------------------------------------------------------|
| trigger  | bool     | When true, the collider acts as a trigger that detects overlaps but doesn't create physical collisions |
| convex   | bool     | When true, the mesh is treated as a convex shape, allowing it to be used as a dynamic collider         |
| attitude | Attitude | The physical material properties of the collider (affects bounce, friction, etc.)                      |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the mesh collider with the physics system.

## Example Usage
```csharp
// Create a detailed terrain collider
MeshCollider terrainCollider = new MeshCollider();
terrainCollider.trigger = false; // Solid physical collider
terrainCollider.convex = false; // Complex concave shape
terrainCollider.attitude = Attitude.Natural; // Standard physics properties

// Create a convex collider for a rock
MeshCollider rockCollider = new MeshCollider();
rockCollider.trigger = false;
rockCollider.convex = true; // Make it suitable for physics interactions
rockCollider.attitude = Attitude.SemiBouncing; // Slightly bouncy

// Create a trigger zone with complex shape
MeshCollider triggerZone = new MeshCollider();
triggerZone.trigger = true; // Just for overlap detection
triggerZone.convex = false; // Can be any shape when used as trigger
```

## Technical Details
- For non-trigger colliders, the collision mesh uses the same geometry as the visual mesh of the object
- When `convex` is true, the mesh is treated as if it were a convex hull of the original shape
- Convex mesh colliders can be used with dynamic physics objects (those with Physics component)
- Concave (non-convex) mesh colliders can only be used with static objects unless they're triggers
- Mesh colliders provide the most accurate collision detection but at a higher performance cost

## Use Cases
- Complex terrain or level geometry
- Detailed props and environment objects
- Custom-shaped trigger areas
- Static world objects with irregular shapes
- Convex dynamic objects when primitive colliders aren't sufficient

## Notes
- For performance reasons, use simpler colliders (Box, Sphere, Capsule) when possible
- Very high-poly meshes should be simplified for collision to improve performance
- For characters and most dynamic objects, Capsule or Box colliders are recommended
- Concave mesh colliders with many polygons can significantly impact physics performance
- Using many mesh colliders can increase memory usage and physics computation cost

## Related Components
- Alternative to `BoxCollider.cs`, `SphereCollider.cs`, and `CapsuleCollider.cs`
- Works with `Physics.cs` for physical interactions

## Dependencies
- Uses `ColliderUtil.AddMeshCollider()` to register with the physics system
