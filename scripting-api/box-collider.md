---
layout: default
title: BoxCollider
nav_order: 4
parent: Scripting API
---
# BoxCollider

## Description
The `BoxCollider` class implements a box-shaped collision volume for physics interactions. It can be used for detecting collisions with other objects or as a physical boundary for physics simulations.

## Namespace
`Universe.Core`

## Properties
| Property | Type     | Description                                                                                            |
|----------|----------|--------------------------------------------------------------------------------------------------------|
| trigger  | bool     | When true, the collider acts as a trigger that detects overlaps but doesn't create physical collisions |
| center   | vector3  | The local center position offset of the box collider                                                   |
| size     | vector3  | The dimensions of the box in local space (default: [1, 1, 1])                                          |
| attitude | Attitude | The physical material properties of the collider (affects bounce, friction, etc.)                      |


## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the box collider with the physics system.

## Example Usage
```csharp
// Create a basic box collider
BoxCollider wallCollider = new BoxCollider();
wallCollider.size = [10, 3, 0.5]; // A wall 10 units wide, 3 units tall, and 0.5 units thick
wallCollider.trigger = false; // Solid physical collider
wallCollider.attitude = Attitude.Natural; // Normal physical properties

// Create a trigger area
BoxCollider triggerZone = new BoxCollider();
triggerZone.size = [5, 3, 5]; // 5x5 area with 3 units height
triggerZone.trigger = true; // Trigger that detects overlaps
```

## Notes
- Box colliders need to be attached to an object with a position and rotation
- For proper collision detection, at least one of the colliding objects should have a `Physics` component
- When `trigger` is true, collisions will generate trigger events but won't cause physical reactions
- Box colliders are efficient and should be preferred over more complex collision shapes when appropriate

## Dependencies
- Uses `ColliderUtil.AddBoxCollider()` to register with the physics system
- Works with `Physics.cs` for physical interactions
