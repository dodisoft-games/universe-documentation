---
layout: default
title: IKHandler
nav_order: 19
parent: Scripting API
---
# IKHandler

## Description
The `IKHandler` class manages Inverse Kinematics (IK) for character limbs and head. It provides smooth transitions for IK constraints, allowing characters to naturally interact with objects in the environment, such as looking at points of interest, placing hands on objects, or properly placing feet on surfaces.

## Namespace
`Universe.Character`

## Enums

### IKNode
Defines the character body parts that can be controlled with IK.

| Value | Description |
|-------|-------------|
| Head | The character's head/neck |
| LeftFoot | The character's left foot |
| RightFoot | The character's right foot |
| LeftHand | The character's left hand |
| RightHand | The character's right hand |

## Properties
| Property | Type | Description |
|----------|------|-------------|
| character | Character | Reference to the character to apply IK to |
| node | IKNode | The IK node/body part to control |
| positionWeigth | float | Strength of the position constraint (0-1, default: 1) |
| rotationWeight | float | Strength of the rotation constraint (0-1, default: 1) |
| target | UniObject | The target object for the IK constraint |
| setOnStart | bool | Whether to set the IK constraint automatically on start (default: true) |
| delay | float | Time in seconds for smooth transitions (default: 0.5) |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Sets up the IK constraint if `setOnStart` is true.

### SetIK
```csharp
void SetIK()
```
Enables the IK constraint and transitions to full weight over the specified delay time.

### ResetIK
```csharp
void ResetIK()
```
Transitions the IK constraint weights to zero over the specified delay time.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Handles the smooth transition of IK weights.

## Example Usage
```csharp
// Make a character look at an object of interest
IKHandler headIK = new IKHandler();
headIK.character = playerCharacter;
headIK.node = IKNode.Head;
headIK.target = interestingObject;
headIK.positionWeigth = 0.8; // Not full constraint
headIK.rotationWeight = 1.0; // Full rotation constraint
headIK.delay = 0.3; // Quick transition

// Make a character place hand on object
IKHandler handIK = new IKHandler();
handIK.character = npcCharacter;
handIK.node = IKNode.RightHand;
handIK.target = doorHandle;
handIK.setOnStart = false; // Don't set immediately
handIK.delay = 1.0; // Slow, natural transition

// Later, when character should grab the handle:
handIK.SetIK();

// And when they should let go:
handIK.ResetIK();
```

## Implementation Details
- The IK system uses the character's built-in IK capabilities through the `Character.SetIKState()`, `Character.SetIKGoal()`, and `Character.SetIKWeights()` methods
- The transition weights are smoothly interpolated over the specified delay time
- A value of -1 for targetValue will completely disable IK
- The actual IK implementation details are handled in the Character class

## Use Cases
- Characters looking at points of interest or other characters
- Hand placement for interaction with objects (grabbing, touching)
- Foot placement on uneven terrain
- Complex animations like climbing, leaning, or reaching
- Procedural animation adjustments

## Notes
- For IK to work, the character model must have a proper rigging that supports IK
- Setting appropriate weight values is important for natural-looking results
- Multiple IK handlers can be used on different nodes of the same character
- For complex IK scenarios, consider implementing a custom solution with greater control

## Related Components
- Works with `Character.cs` for IK functionality
- References the `IKNode` enum for target body parts

## Dependencies
- Requires a properly set up `Character` instance
- Uses `Time.GameTime()` for timing
- Uses `Math` functions for interpolation
