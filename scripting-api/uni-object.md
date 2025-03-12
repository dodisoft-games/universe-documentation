---
layout: default
title: UniObject
nav_order: 50
parent: Scripting API
---
# UniObject

## Description
The `UniObject` class is the core object representation in the Universe framework. It encapsulates game objects with properties for positioning, rotation, and scaling, and provides methods for manipulating and querying objects in the game world.

## Properties
| Property   | Type     | Description                                                              |
|------------|----------|--------------------------------------------------------------------------|
| tag        | string   | Identifier tag for categorizing and finding objects                      |
| asset      | UniAsset | Reference to the asset used to create this object                        |
| position   | vector3  | Local position of the object                                             |
| rotation   | vector3  | Local rotation of the object in Euler angles                             |
| scale      | vector3  | Local scale of the object                                                |
| persistent | bool     | Whether the object should persist between scene changes (default: false) |

## Methods

### GetName
```csharp
string GetName()
```
Gets the name of the object.

#### Returns
- The object's name

### SetName
```csharp
string SetName(string name)
```
Sets the name of the object.

#### Parameters
- `name`: The new name for the object

### GetActivation
```csharp
bool GetActivation()
```
Checks if the object is active.

#### Returns
- `true` if the object is active, `false` otherwise

### SetActivation
```csharp
void SetActivation(bool enabled)
```
Sets the active state of the object.

#### Parameters
- `enabled`: Whether the object should be active

### GetScript
```csharp
uniscript GetScript(string name)
```
Gets a script component by name.

#### Parameters
- `name`: The name of the script to find

#### Returns
- The script component, or null if not found

### AddScript
```csharp
uniscript AddScript(string name)
```
Adds a script component to the object.

#### Parameters
- `name`: The name of the script to add

#### Returns
- The newly added script component

### RemoveScipt
```csharp
void RemoveScipt(string name)
```
Removes a script component by name.

#### Parameters
- `name`: The name of the script to remove

### RemoveScriptComponent
```csharp
void RemoveScriptComponent(uniscript script)
```
Removes a specific script component.

#### Parameters
- `script`: The script component to remove

### SetColor
```csharp
void SetColor(float r, float g, float b, float a)
```
Sets the color of the object's material.

#### Parameters
- `r`, `g`, `b`, `a`: Color components (red, green, blue, alpha)

### SetMaterial
```csharp
void SetMaterial(Shaders shader, UniAsset texture)
```
Sets the material and texture of the object.

#### Parameters
- `shader`: The shader type to use
- `texture`: The texture asset to apply

### SetShader
```csharp
void SetShader(Shaders shader)
```
Sets the shader of the object's material.

#### Parameters
- `shader`: The shader type to use

### LookAt
```csharp
void LookAt(UniObject target)
```
Rotates the object to face another object.

#### Parameters
- `target`: The object to look at

### LookAtPoint
```csharp
void LookAtPoint(vector3 target)
```
Rotates the object to face a point in space.

#### Parameters
- `target`: The point to look at

### LookAtSmooth
```csharp
void LookAtSmooth(UniObject target, float speed)
```
Smoothly rotates the object to face another object.

#### Parameters
- `target`: The object to look at
- `speed`: The rotation speed

### LookAtSmoothWithOffset
```csharp
void LookAtSmoothWithOffset(UniObject target, vector3 offset, float speed)
```
Smoothly rotates the object to face another object with an offset.

#### Parameters
- `target`: The object to look at
- `offset`: Position offset to apply
- `speed`: The rotation speed

### Rotate
```csharp
void Rotate(float x, float y, float z)
```
Rotates the object by the specified angles.

#### Parameters
- `x`, `y`, `z`: Rotation angles in degrees

### Translate
```csharp
void Translate(float x, float y, float z)
```
Moves the object by the specified amounts.

#### Parameters
- `x`, `y`, `z`: Translation distances

### GetWorldPosition
```csharp
vector3 GetWorldPosition()
```
Gets the world-space position of the object.

#### Returns
- The object's position in world space

### SetWorldPosition
```csharp
vector3 SetWorldPosition(vector3 pos)
```
Sets the world-space position of the object.

#### Parameters
- `pos`: The new world position

### Forward
```csharp
vector3 Forward()
```
Gets the forward direction vector of the object.

#### Returns
- The normalized forward vector

### Right
```csharp
vector3 Right()
```
Gets the right direction vector of the object.

#### Returns
- The normalized right vector

### Up
```csharp
vector3 Up()
```
Gets the up direction vector of the object.

#### Returns
- The normalized up vector

### Destroy
```csharp
void Destroy()
```
Destroys the object.

### GetRotation
```csharp
quaternion GetRotation()
```
Gets the rotation of the object as a quaternion.

#### Returns
- The object's rotation as a quaternion

### SetRotation
```csharp
void SetRotation(quaternion rot)
```
Sets the rotation of the object using a quaternion.

#### Parameters
- `rot`: The new rotation as a quaternion

### ReParent
```csharp
void ReParent(uniscript parent)
```
Changes the parent of the object.

#### Parameters
- `parent`: The new parent script (or its containing object)

### Reset
```csharp
void Reset()
```
Resets the object's position, rotation, and scale to default values.

### GetParent
```csharp
UniObject GetParent()
```
Gets the parent object.

#### Returns
- The parent object, or null if none

### GetChilds
```csharp
List GetChilds()
```
Gets a list of all child objects.

#### Returns
- A List containing all child objects

## Example Usage
```csharp
// Create and position an object
UniObject cube = CreateCube();
cube.position = [1, 0, 2];
cube.rotation = [0, 45, 0];
cube.scale = [2, 2, 2];

// Modify object properties
cube.tag = "obstacle";
cube.SetName("LargeCube");
cube.SetColor(1, 0, 0, 1); // Red color

// Manipulate object in the world
cube.Translate(0, 1, 0); // Move up by 1 unit
cube.Rotate(0, 45, 0); // Rotate 45 degrees around Y axis

// Make object face a target
UniObject player = GetPlayer();
cube.LookAt(player);

// Get object orientation vectors
vector3 forward = cube.Forward();
vector3 up = cube.Up();
vector3 right = cube.Right();

// Add and remove components
BoxCollider collider = cube.AddScript("Universe.Core.BoxCollider");
collider.size = [2, 2, 2];

Physics physics = cube.AddScript("Universe.Core.Physics");
physics.mass = 10;

// Remove a component by reference
cube.RemoveScriptComponent(physics);

// Get a component by name
BoxCollider existingCollider = cube.GetScript("Universe.Core.BoxCollider");

// Change parent-child relationships
cube.ReParent(parentObject);

// Get hierarchy information
UniObject parent = cube.GetParent();
List children = parentObject.GetChilds();

// Destroy the object when no longer needed
cube.Destroy();
```

## Technical Details
- UniObject is the fundamental object representation in the Universe framework
- It provides an abstracted interface to the underlying game engine objects
- Position, rotation, and scale use local coordinates relative to the parent
- Many methods defer to utility classes like `UniObjectUtil` for implementation
- World position is distinct from local position when objects have parents
- Direction vectors (Forward, Right, Up) depend on the object's current rotation

## Use Cases
- Representing and manipulating game entities
- Creating object hierarchies
- Managing components and behaviors
- Positioning and orienting objects in the game world
- Applying visual properties like materials and colors
- Looking at targets or orienting toward points
- Organizing objects with parent-child relationships

## Notes
- Most operations that modify the object happen immediately
- For smooth transitions, use methods with "Smooth" in the name
- The `tag` property is useful for object categorization and finding
- Local position/rotation are relative to the parent object
- For physics objects, consider using appropriate colliders and the Physics component
- The `persistent` flag should be used carefully to avoid memory leaks

## Related Components
- Works with all script components in the framework
- Parent class for all game objects

## Dependencies
- Uses `Universe.Core` and `Universe.Helper` namespaces
- Uses `UniObjectUtil` for object operations
- Uses `VectorUtil` for vector operations
- Uses `QuaternionUtil` for rotation operations
