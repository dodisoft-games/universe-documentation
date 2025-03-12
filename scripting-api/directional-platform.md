---
layout: default
title: DirectionalPlatform
nav_order: 14
parent: Scripting API
---
# DirectionalPlatform

## Description
The `DirectionalPlatform` class creates oscillating platforms that move and rotate in a sinusoidal pattern. This is useful for creating moving platforms, pendulums, elevators, or other cyclic motion elements in a game.

## Namespace
`Universe.Tools`

## Properties
| Property    | Type    | Description                                   |
|-------------|---------|-----------------------------------------------|
| moveDelta   | vector3 | Maximum movement distance in each axis        |
| rotateDelta | vector3 | Maximum rotation angles in each axis          |
| speed       | float   | Speed of the oscillation (default: 1)         |
| span        | float   | Phase offset for the oscillation (default: 0) |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Initializes the platform's starting position and rotation.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the platform's position and rotation based on a sine wave function.

## Example Usage
```csharp
// Create a horizontal swinging platform
DirectionalPlatform swingPlatform = new DirectionalPlatform();
swingPlatform.moveDelta = [5, 0, 0]; // Move 5 units left and right
swingPlatform.rotateDelta = [0, 0, 15]; // Rotate 15 degrees around Z axis
swingPlatform.speed = 0.5; // Slower oscillation
swingPlatform.span = 0; // Start at neutral position

// Create a vertical elevator
DirectionalPlatform elevator = new DirectionalPlatform();
elevator.moveDelta = [0, 8, 0]; // Move 8 units up and down
elevator.rotateDelta = [0, 0, 0]; // No rotation
elevator.speed = 0.3; // Slow oscillation
elevator.span = 0.5; // Start halfway through the cycle

// Create a complex motion platform
DirectionalPlatform complexPlatform = new DirectionalPlatform();
complexPlatform.moveDelta = [3, 2, 1]; // Move in all directions
complexPlatform.rotateDelta = [10, 5, 15]; // Rotate in all axes
complexPlatform.speed = 0.7; // Medium speed
complexPlatform.span = 0.25; // Start at 1/4 of the cycle
```

## Implementation Details
- The platform's position oscillates using a sine wave: `position + sin(time * speed) * moveDelta`
- The platform's rotation oscillates similarly: `rotation * quaternion(sin(time * speed) * rotateDelta)`
- The platform synchronizes with server time in networked games
- The actual movement is handled through a connected `MovingPlatform` component

## Notes
- This component requires a `MovingPlatform` component on the same object
- In networked games, the platform will synchronize its motion to ensure consistent behavior for all players
- The oscillation is continuous and does not stop; for platforms that stop at endpoints, consider using a different solution
- For complex paths, consider using `CinematicMotion` instead

## Related Components
- Works with `MovingPlatform.cs` which handles the actual physics movement

## Dependencies
- Uses `UniObjectUtil` for object manipulation
- Uses `Time` for timing calculations
- Uses `QuaternionUtil` for rotation operations
- Uses `StorageUtil` and `NetworkUtil` for network synchronization
