---
layout: default
title: Vector3
nav_order: 51
parent: Scripting API
---
# Vector3

## Description
The `Vector3` class provides a comprehensive object-oriented interface for working with 3D vectors. It encapsulates x, y, and z components and offers a wide range of vector operations including creation, manipulation, and mathematical functions.

## Namespace
`Universe.Core`

## Properties

| Property | Type  | Description                   |
|----------|-------|-------------------------------|
| x        | float | The X component of the vector |
| y        | float | The Y component of the vector |
| z        | float | The Z component of the vector |

## Methods

### Vector3
```csharp
void Vector3(float xV, float yV, float zV)
```
Constructor that initializes the vector with specific values.

#### Parameters
- `xV`: Value for the X component
- `yV`: Value for the Y component
- `zV`: Value for the Z component

### New
```csharp
Vector3 New(float xV, float yV, float zV)
```
Sets the vector components to new values and returns the vector.

#### Parameters
- `xV`: Value for the X component
- `yV`: Value for the Y component
- `zV`: Value for the Z component

#### Returns
- The vector itself (for method chaining)

### Zero
```csharp
Vector3 Zero()
```
Sets the vector to (0, 0, 0) and returns it.

#### Returns
- The vector itself (for method chaining)

### Right
```csharp
Vector3 Right()
```
Sets the vector to (1, 0, 0) and returns it.

#### Returns
- The vector itself (for method chaining)

### Left
```csharp
Vector3 Left()
```
Sets the vector to (-1, 0, 0) and returns it.

#### Returns
- The vector itself (for method chaining)

### Up
```csharp
Vector3 Up()
```
Sets the vector to (0, 1, 0) and returns it.

#### Returns
- The vector itself (for method chaining)

### Down
```csharp
Vector3 Down()
```
Sets the vector to (0, -1, 0) and returns it.

#### Returns
- The vector itself (for method chaining)

### Forward
```csharp
Vector3 Forward()
```
Sets the vector to (0, 0, 1) and returns it.

#### Returns
- The vector itself (for method chaining)

### Backward
```csharp
Vector3 Backward()
```
Sets the vector to (0, 0, -1) and returns it.

#### Returns
- The vector itself (for method chaining)

### One
```csharp
Vector3 One()
```
Sets the vector to (1, 1, 1) and returns it.

#### Returns
- The vector itself (for method chaining)

### FromVector
```csharp
Vector3 FromVector(vector3 vector)
```
Sets the vector components from an existing vector3 and returns it.

#### Parameters
- `vector`: Source vector to copy from

#### Returns
- The vector itself (for method chaining)

### Add
```csharp
Vector3 Add(Vector3 vector)
```
Adds another vector to this one and returns the result.

#### Parameters
- `vector`: Vector to add

#### Returns
- The vector itself (for method chaining)

### ToVector
```csharp
vector3 ToVector()
```
Converts the Vector3 object to a native vector3 value.

#### Returns
- A native vector3 value

### Normalize
```csharp
Vector3 Normalize()
```
Normalizes the vector (scales to unit length) and returns it.

#### Returns
- The vector itself (for method chaining)

### Normalized
```csharp
Vector3 Normalized()
```
Returns a new normalized copy of the vector without modifying the original.

#### Returns
- A new Vector3 with unit length

### Magnitude
```csharp
float Magnitude()
```
Calculates the length/magnitude of the vector.

#### Returns
- The length of the vector

### Cross
```csharp
Vector3 Cross(Vector3 vector)
```
Calculates the cross product with another vector.

#### Parameters
- `vector`: The vector to cross with

#### Returns
- A new Vector3 representing the cross product

### Project
```csharp
Vector3 Project(Vector3 normal)
```
Projects this vector onto another vector.

#### Parameters
- `normal`: The vector to project onto

#### Returns
- A new Vector3 representing the projection

### Dot
```csharp
float Dot(Vector3 vector)
```
Calculates the dot product with another vector.

#### Parameters
- `vector`: The vector to dot with

#### Returns
- The scalar dot product

### Lerp
```csharp
Vector3 Lerp(Vector3 to, float phase)
```
Linearly interpolates to another vector by the specified amount.

#### Parameters
- `to`: Target vector
- `phase`: Interpolation amount (0-1)

#### Returns
- A new Vector3 with the interpolated values

### SmoothLerp
```csharp
Vector3 SmoothLerp(Vector3 to, float phase)
```
Smoothly interpolates to another vector using a smooth step function.

#### Parameters
- `to`: Target vector
- `phase`: Interpolation amount (0-1)

#### Returns
- A new Vector3 with the smoothly interpolated values

## Example Usage
```csharp
// Create vectors
Vector3 position = new Vector3(10, 5, 3);
Vector3 direction = new Vector3().Forward(); // (0, 0, 1)

// Basic operations
Vector3 targetPosition = new Vector3(15, 8, 12);
Vector3 moveDirection = new Vector3();
moveDirection.FromVector(targetPosition.ToVector() - position.ToVector());
moveDirection.Normalize(); // Convert to unit vector

// Calculate distance
float distance = position.ToVector() - targetPosition.ToVector()).Magnitude();

// Vector operations
Vector3 up = new Vector3().Up();
Vector3 right = new Vector3().Right();
Vector3 forward = right.Cross(up); // Cross product to find forward

// Dot product for angle calculation
float dotProduct = moveDirection.Dot(forward);
float angle = Math.Acos(dotProduct) * 57.2957795; // Convert to degrees

// Projection
Vector3 movementOnXZ = moveDirection.Project(new Vector3().New(1, 0, 1).Normalize());

// Interpolation for smooth movement
Vector3 newPosition = position.Lerp(targetPosition, 0.1); // Move 10% toward target

// Create a smooth path
Vector3 smoothPoint = position.SmoothLerp(targetPosition, 0.5);
```

## Technical Details
- The `Vector3` class is an object-oriented wrapper around the native `vector3` type
- Many methods return the instance itself to allow method chaining
- Methods that create new vectors (like `Normalized()`) create new `Vector3` instances
- The class uses `VectorUtil` for many mathematical operations
- Certain methods modify the vector in place (`Normalize()`, `Add()`, etc.)
- Other methods return new vectors without modifying the original (`Normalized()`, `Cross()`, etc.)
- The `ToVector()` method converts to the native `vector3` type for compatibility with other functions

## Use Cases
- Representing positions in 3D space
- Defining directions and orientations
- Calculating movements and trajectories
- Performing geometric calculations
- Working with physics forces and velocities
- Defining offsets and displacements
- Interpolating between positions for smooth movement

## Notes
- For best performance, reuse Vector3 instances when possible
- The convention follows a right-handed coordinate system
- Use the appropriate directional constants (Up, Forward, etc.) for standard directions
- Be careful not to normalize zero vectors, as this will result in NaN values
- The `SmoothLerp` function provides a more natural-looking interpolation than linear interpolation
- For frequent vector math, consider using the native `vector3` type directly with `VectorUtil`

## Related Components
- Used throughout the framework for positions, directions, and orientations
- Works with `Quaternion.cs` for rotations
- Compatible with most components that work with positions and directions

## Dependencies
- Uses `VectorUtil` for vector operations
- Uses `Math` for mathematical functions like square root and trigonometry
