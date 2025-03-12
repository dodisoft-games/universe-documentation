---
layout: default
title: Quaternion
nav_order: 36
parent: Scripting API
---
# Quaternion

## Description
The `Quaternion` class provides a simplified interface for working with rotations in 3D space. While it uses the name "Quaternion," it actually stores Euler angles (x, y, z) internally and provides conversions to and from quaternion representation. This offers a more intuitive way to handle rotations for many common use cases.

## Namespace
`Universe.Core`

## Properties
| Property | Type  | Description                           |
|----------|-------|---------------------------------------|
| x        | float | Rotation around the X axis in degrees |
| y        | float | Rotation around the Y axis in degrees |
| z        | float | Rotation around the Z axis in degrees |

## Methods

### Quaternion
```csharp
void Quaternion(float xV, float yV, float zV)
```
Constructor that initializes the Quaternion with the specified Euler angles.

#### Parameters
- `xV`: Rotation around the X axis in degrees
- `yV`: Rotation around the Y axis in degrees
- `zV`: Rotation around the Z axis in degrees

### ToEuler
```csharp
vector3 ToEuler()
```
Converts the stored angles to a vector3 representing Euler angles.

#### Returns
- A vector3 containing the x, y, and z rotation values

### ToQuaternion
```csharp
quaternion ToQuaternion()
```
Converts the stored Euler angles to an actual quaternion representation.

#### Returns
- A quaternion representation of the rotation

## Example Usage
```csharp
// Create a rotation representing 90 degrees around the Y axis
Quaternion yRotation = new Quaternion(0, 90, 0);

// Convert to a vector3 for use with other systems
vector3 eulerAngles = yRotation.ToEuler();

// Convert to a true quaternion for use with quaternion-based math
quaternion quatRotation = yRotation.ToQuaternion();

// Create a rotation for a camera looking slightly up and to the right
Quaternion cameraRotation = new Quaternion(-15, 30, 0);

// Create a complex rotation
Quaternion complexRotation = new Quaternion(45, 180, 30);
```

## Technical Details
- Despite the class name, this isn't a true quaternion implementation but a convenience wrapper
- The internal representation uses Euler angles (x, y, z) in degrees
- The `ToQuaternion()` method performs the actual conversion to quaternion format
- Euler angles can suffer from gimbal lock, which the true quaternion representation avoids
- Rotations generally follow the Yaw (Y), Pitch (X), Roll (Z) convention

## Use Cases
- Specifying simple rotations in a more intuitive way
- Converting between Euler angles and quaternions
- Setting up initial orientations for objects
- Defining rotation offsets
- Working with systems that use different rotation representations

## Notes
- For complex rotation operations (interpolation, composition, etc.), it's better to use the quaternion utility functions directly
- Euler angles are more intuitive but can suffer from gimbal lock when two rotation axes align
- The order of rotation application matters with Euler angles
- Consider using `QuaternionUtil` functions for more advanced rotation operations
- This class is primarily a convenience wrapper to make rotations more approachable

## Related Components
- Used throughout the framework for representing rotations
- Works with `QuaternionUtil` for advanced quaternion operations

## Dependencies
- Uses `VectorUtil.New()` for creating vector3 values
- Uses `QuaternionUtil.Euler()` for converting to quaternion representation
