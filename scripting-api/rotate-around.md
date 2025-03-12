---
layout: default
title: RotateAround
nav_order: 37
parent: Scripting API
---
# RotateAround

## Description
The `RotateAround` class provides a simple way to make objects continuously rotate around their local axes. This is useful for creating spinning objects, rotating displays, or simple animations.

## Namespace
`Universe.Helper`

## Properties

| Property | Type    | Description                                           |
|----------|---------|-------------------------------------------------------|
| speed    | vector3 | Rotation speed around each axis in degrees per second |

## Methods

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Applies rotation based on the speed values.

## Example Usage
```csharp
// Create a simple rotating object (like a spinning coin)
RotateAround coinRotation = new RotateAround();
coinRotation.speed = [0, 90, 0]; // Rotate 90 degrees per second around Y axis

// Create an object that tumbles in multiple axes
RotateAround tumblingObject = new RotateAround();
tumblingObject.speed = [30, 45, 15]; // Rotation around all three axes

// Create a slowly rotating display pedestal
RotateAround displayRotation = new RotateAround();
displayRotation.speed = [0, 15, 0]; // Slow rotation around Y axis

// Create a rapidly spinning propeller
RotateAround propellerSpin = new RotateAround();
propellerSpin.speed = [0, 0, 360]; // Fast rotation around Z axis
```

## Technical Details
- Rotation is applied every frame in the `OnUpdate` method
- The rotation is relative to the object's local coordinate system
- The speed vector components represent degrees per second around each axis
- Positive values rotate in the clockwise direction around the axis
- Rotation is applied in the order: X, Y, Z

## Use Cases
- Spinning collectibles or power-ups
- Rotating displays for items or characters
- Propellers, fans, or wheels
- Orbiting objects like planets or satellites
- Simple idle animations
- Loading indicators or UI elements
- Environmental objects like windmills or gears

## Notes
- This is a simple component that provides continuous rotation at a fixed rate
- For more complex rotation behaviors, consider implementing a custom script
- To change rotation speed at runtime, simply modify the `speed` property
- To temporarily stop rotation, set `speed` to [0, 0, 0]
- For rotation around a point rather than the object's center, a different approach is needed

## Related Components
- Can be used with any object that needs simple rotation
- Complements other animation and movement components

## Dependencies
- Uses `UniObjectUtil.Rotate()` for the actual rotation
- Uses `VectorUtil` to extract components from the speed vector
