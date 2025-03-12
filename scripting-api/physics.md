---
layout: default
title: Physics
nav_order: 35
parent: Scripting API
---
# Physics

## Description
The `Physics` class provides dynamic physical behavior for game objects, allowing them to be affected by forces, gravity, and collisions. It enables realistic movement, bouncing, and interaction with other physical objects in the game world.

## Namespace
`Universe.Core`

## Enums

### ForceMode
Defines how forces are applied to the object.

| Value | Description |
|-------|-------------|
| Acceleration | Force is applied as an acceleration, ignoring mass |
| Force | Force is applied with mass taken into account (F = m * a) |
| Impact | Applies an instant change in velocity (impulse) |
| Velocity | Directly sets the velocity, ignoring mass |

### Attitude
Defines the physical material properties of the object.

| Value | Description |
|-------|-------------|
| None | No specific physical material properties |
| ImpactAbsorbing | Heavily dampens collisions with almost no bounce |
| SemiAbsorbing | Moderately dampens collisions with low bounce |
| Natural | Standard physical properties with moderate bounce |
| SemiBouncing | Increased bounce with moderate energy conservation |
| HighBouncing | High bounce with high energy conservation |
| PerfectBouncing | Maximum bounce with near-perfect energy conservation |

## Properties

| Property      | Type      | Description                                               |
|---------------|-----------|-----------------------------------------------------------|
| eventReceiver | uniscript | Script that receives collision events                     |
| gravity       | bool      | Whether the object is affected by gravity (default: true) |
| freeze        | bool      | Whether the object's position and rotation are frozen     |
| mass          | float     | Mass of the object in kilograms (default: 1)              |
| friction      | float     | Friction coefficient of the object (default: 0.1)         |
| lockXPosition | bool      | Constrains movement along the X axis (default: false)     |
| lockYPosition | bool      | Constrains movement along the Y axis (default: false)     |
| lockZPosition | bool      | Constrains movement along the Z axis (default: false)     |
| lockXRotation | bool      | Constrains rotation around the X axis (default: false)    |
| lockYRotation | bool      | Constrains rotation around the Y axis (default: false)    |
| lockZRotation | bool      | Constrains rotation around the Z axis (default: false)    |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the physics component with the physics system.

### AddForce
```csharp
void AddForce(float x, float y, float z, ForceMode mode)
```
Adds a force to the object using individual components.

#### Parameters
- `x`: Force component along the X axis
- `y`: Force component along the Y axis
- `z`: Force component along the Z axis
- `mode`: How the force is applied (Acceleration, Force, Impact, or Velocity)

### AddForceVector
```csharp
void AddForceVector(vector3 force, ForceMode mode)
```
Adds a force to the object using a vector.

#### Parameters
- `force`: Force vector
- `mode`: How the force is applied

### GetVelocity
```csharp
vector3 GetVelocity()
```
Gets the current velocity of the object.

#### Returns
- The velocity vector

### SetVelocity
```csharp
void SetVelocity(vector3 velocity)
```
Sets the velocity of the object.

#### Parameters
- `velocity`: The new velocity vector

### AddTorque
```csharp
void AddTorque(float x, float y, float z, ForceMode mode)
```
Adds rotational force (torque) to the object using individual components.

#### Parameters
- `x`: Torque component around the X axis
- `y`: Torque component around the Y axis
- `z`: Torque component around the Z axis
- `mode`: How the torque is applied

### AddTorqueVector
```csharp
void AddTorqueVector(vector3 force, ForceMode mode)
```
Adds rotational force (torque) to the object using a vector.

#### Parameters
- `force`: Torque vector
- `mode`: How the torque is applied

### GetAngularVelocity
```csharp
vector3 GetAngularVelocity()
```
Gets the current rotational velocity of the object.

#### Returns
- The angular velocity vector

### SetAngularVelocity
```csharp
void SetAngularVelocity(vector3 velocity)
```
Sets the rotational velocity of the object.

#### Parameters
- `velocity`: The new angular velocity vector

## Example Usage
```csharp
// Create a basic physical object
Physics rockPhysics = new Physics();
rockPhysics.mass = 5; // 5kg rock
rockPhysics.friction = 0.3; // Moderate friction
rockPhysics.gravity = true;

// Create a floating object
Physics floatingOrb = new Physics();
floatingOrb.gravity = false; // Not affected by gravity
floatingOrb.friction = 0.01; // Very low friction
floatingOrb.mass = 0.5; // Lightweight

// Create a constrained object (like a sliding door)
Physics slidingDoor = new Physics();
slidingDoor.lockYPosition = true; // Can't move up/down
slidingDoor.lockZPosition = true; // Can't move forward/backward
slidingDoor.lockXRotation = true; // Can't rotate around X
slidingDoor.lockYRotation = true; // Can't rotate around Y
slidingDoor.lockZRotation = true; // Can't rotate around Z
slidingDoor.friction = 0.2;

// Apply forces to objects
void LaunchObject(Physics physics) {
    // Apply an upward and forward impulse
    physics.AddForce(0, 10, 5, ForceMode.Impact);
    // Add some spin
    physics.AddTorque(0, 5, 0, ForceMode.Impact);
}

// Create a bouncy ball
Physics bouncyBall = new Physics();
bouncyBall.mass = 0.2; // Lightweight
bouncyBall.friction = 0.05; // Low friction
// The actual bounciness would be set on the collider's attitude
```

## Technical Details
- The physics system uses a rigid body model for dynamics
- Forces and torques can be applied in different modes to achieve various effects
- Constraints can be used to limit movement to specific axes
- The `eventReceiver` receives collision callbacks when the object collides with others
- The actual collision shape is determined by attached collider components
- The `Attitude` enum affects collision response, but is set on colliders, not the Physics component

## Use Cases
- Dynamic objects that respond to forces and collisions
- Projectiles and thrown items
- Interactive props and objects
- Sliding or rolling mechanisms
- Constraints for mechanical systems
- Vehicles and character physics
- Destructible environmental elements

## Notes
- For character movement, consider using the Character component instead of direct physics
- Performance can be affected by many physical objects; use judiciously
- Constraints can help create mechanical systems like hinges, sliders, or revolute joints
- Physical simulations are approximate; very small or very fast objects may need special handling
- For the most realistic results, set appropriate mass values based on the object's size and material

## Related Components
- Works with `BoxCollider.cs`, `SphereCollider.cs`, `CapsuleCollider.cs`, or `MeshCollider.cs` for collision shape
- Can be used with `MovingPlatform.cs` for carried physics objects

## Dependencies
- Uses `PhysicsUtil` for core physics operations
