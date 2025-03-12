---
layout: default
title: Character
nav_order: 10
parent: Scripting API
---
# Character

## Description
The `Character` class is a comprehensive character controller that handles movement, animations, actions, and interactions for game characters. It supports both physics-based and action-based character types with a range of capabilities including walking, running, jumping, climbing, and swimming.

## Namespace
`Universe.Character`

## Enums

### CharacterType
Defines the type of character controller to use.

| Value | Description |
|-------|-------------|
| Physics | Character uses physics-based movement (affected by gravity, collisions, etc.) |
| Action | Character uses animation-driven movement (more suitable for cutscenes) |

## Properties
| Property           | Type           | Description                                                             |
|--------------------|----------------|-------------------------------------------------------------------------|
| type               | CharacterType  | Type of character controller to use                                     |
| radius             | float          | Collision radius for the character (default: 0.5)                       |
| height             | float          | Character's height (default: 3)                                         |
| stepHeight         | float          | Maximum height of steps the character can climb (default: 0.5)          |
| slope              | float          | Maximum slope angle in degrees the character can climb (default: 45)    |
| speed              | float          | Base movement speed multiplier (default: 1)                             |
| movementSpeed      | float          | Movement speed multiplier (default: 1)                                  |
| rotationSpeed      | float          | Rotation speed multiplier (default: 1)                                  |
| acceleration       | float          | Movement acceleration (default: 5)                                      |
| cameraBaseMovement | bool           | When true, movement direction is relative to camera (default: true)     |
| polarMovement      | bool           | When true, uses polar coordinates for movement (default: true)          |
| canControl         | bool           | When true, character can be controlled by input (default: true)         |
| canWalk            | bool           | When true, character can walk (default: true)                           |
| canRun             | bool           | When true, character can run (default: true)                            |
| canJump            | bool           | When true, character can jump (default: true)                           |
| canClimb           | bool           | When true, character can climb (default: true)                          |
| canSwim            | bool           | When true, character can swim (default: true)                           |
| canFly             | bool           | When true, character can fly (default: true)                            |
| alwaysRun          | bool           | When true, character always runs instead of walks (default: false)      |
| autoJump           | bool           | When true, character automatically jumps over obstacles (default: true) |
| overrideMotions    | MotionOverride | Custom animations to override default motions                           |
| data               | CharacterData  | Character's stats and attributes                                        |

## Events
| Event                | Parameters                                  | Description                                             |
|----------------------|---------------------------------------------|---------------------------------------------------------|
| MovementChangedEvent | (Movements movement)                        | Triggered when the character's movement type changes    |
| ActionChangedEvent   | (string action, float duration, bool state) | Triggered when the character performs or ends an action |


## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the character, registering it with the appropriate system based on type.

### OnDestroy
```csharp
void OnDestroy()
```
Cleans up event subscriptions when the character is destroyed.

### MovementChanged
```csharp
void MovementChanged(Movements movement)
```
Handles movement type changes.

### ActionChanged
```csharp
void ActionChanged(string action, float duration, bool state)
```
Handles action state changes.

### SetMovement
```csharp
void SetMovement(Movements movement)
```
Sets the character's current movement type.

### SetFacialExpression
```csharp
void SetFacialExpression(FacialExpression expression)
```
Sets the character's facial expression.

### Jump
```csharp
void Jump(bool state)
```
Makes the character jump.

### SetRunningState
```csharp
void SetRunningState(bool state)
```
Toggles between running and walking.

### SetInput
```csharp
void SetInput(float xAxis, float yAxis)
```
Sets the movement input for the character.

### AddMotion
```csharp
void AddMotion(UniAsset motion)
```
Adds an animation motion to the character.

### AddMotionWithName
```csharp
void AddMotionWithName(UniAsset motion, string name)
```
Adds a named animation motion to the character.

### PlayMotion
```csharp
void PlayMotion(string motion, bool stopPreviousAction, bool useGravity)
```
Plays a specific motion by name.

### PlayMotionAsset
```csharp
void PlayMotionAsset(UniAsset motion, bool stopPreviousAction, bool useGravity)
```
Plays a motion from an asset.

### SetRotation
```csharp
void SetRotation(vector3 rotation)
```
Sets the character's rotation.

### Start
```csharp
void Start()
```
Starts the character's movement.

### Stop
```csharp
void Stop()
```
Stops the character's movement.

### SetFollowerCamera
```csharp
void SetFollowerCamera(UniObject camera)
```
Sets a camera to follow the character.

### ResetTransform
```csharp
void ResetTransform(vector3 position, vector3 rotation)
```
Resets the character's position and rotation.

### SetIKState
```csharp
void SetIKState(bool enable)
```
Enables or disables inverse kinematics for the character.

### SetIKWeights
```csharp
void SetIKWeights(IKNode node, float positionWeight, float rotationWeight)
```
Sets weights for an IK node.

### SetIKGoal
```csharp
void SetIKGoal(IKNode node, UniObject target)
```
Sets a target for an IK node.

### AddVelocity
```csharp
void AddVelocity(vector3 velocity, bool local)
```
Adds velocity to the character.

### GetVelocity
```csharp
vector3 GetVelocity()
```
Gets the character's current velocity.

## Example Usage
```csharp
// Create a basic player character
Character player = new Character();
player.type = CharacterType.Physics;
player.radius = 0.5;
player.height = 2.0;
player.canJump = true;
player.canRun = true;
player.canClimb = true;
player.cameraBaseMovement = true; // Move relative to camera

// Set up the character controller
UniObject playerCamera = GetPlayerCamera();
player.SetFollowerCamera(playerCamera);

// Add custom motions
player.AddMotionWithName(idleAnimAsset, "Idle");
player.AddMotionWithName(runAnimAsset, "Run");
player.AddMotionWithName(jumpAnimAsset, "Jump");

// Start the character
player.Start();

// Respond to movement changes
player.MovementChangedEvent += (movement) => {
    if (movement == Movements.Falling) {
        PlayFallingSound();
    }
};
```

## Notes
- The Character system is quite comprehensive and forms the core of character control in the Universe framework
- Physics-based characters are affected by gravity and collisions, while Action-based characters are animation-driven
- The character controller integrates with animation, physics, and input systems
- For NPC characters, this is typically used in conjunction with NpcController
- Inverse Kinematics (IK) support allows for dynamic adjustment of animations to interact with the environment

## Related Components
- Works with `CharacterData.cs` for character attributes
- Works with `MotionOverride.cs` for custom animations
- Used by `NpcController.cs` for AI characters
- Integrates with `IKHandler.cs` for inverse kinematics

## Dependencies
- Uses `Universe.Core` namespace
- Uses `CharacterUtil` for core functionality
- Uses `UniObjectUtil` for object manipulation
