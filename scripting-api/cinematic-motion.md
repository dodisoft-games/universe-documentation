---
layout: default
title: CinematicMotion
nav_order: 11
parent: Scripting API
---
# CinematicMotion

## Description
The `CinematicMotion` class provides functionality for creating smooth camera or object movements along predefined paths for cinematic sequences. It supports different look modes, timing control, and triggering events when specific points are reached.

## Namespace
`Universe.Helper`

## Enums

### CinematicLookMode
Defines how the object's rotation is determined during the movement.

| Value | Description |
|-------|-------------|
| LookForwardPath | Object looks toward the next point on the path |
| LerpPointRotations | Object smoothly transitions between the rotations defined at each point |
| FollowAnObject | Object continuously looks at another object |
| DoNotModify | Object's rotation remains unchanged |

## Properties

| Property             | Type              | Description                                                       |
|----------------------|-------------------|-------------------------------------------------------------------|
| target               | UniObject         | The object to move along the path                                 |
| lookMode             | CinematicLookMode | How the object's rotation is controlled                           |
| followObject         | UniObject         | Object to look at when using FollowAnObject mode                  |
| duration             | float             | Total time to complete the path in seconds (default: 5)           |
| ease                 | float             | Smoothing factor for movement and rotation (default: 1)           |
| startDelay           | float             | Delay before starting the motion in seconds                       |
| stopDelay            | float             | Delay after completing the path before transitioning              |
| activateOnCompletion | UniObject         | Object to activate when the motion completes                      |
| deactivateTarget     | bool              | Whether to deactivate the target object when the motion completes |
| transitionObject     | UniObject         | Object to activate shortly before completion                      |


## Events

| Event               | Parameters                  | Description                                   |
|---------------------|-----------------------------|-----------------------------------------------|
| OnPointReachedEvent | (int index, bool completed) | Triggered when a point on the path is reached |


## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Initiates the navigation along the path.

### StartNavigation
```csharp
void StartNavigation()
```
Sets up the path and begins the motion sequence.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the target's position and rotation along the path.

## Example Usage
```csharp
// Create a cinematic camera flythrough
CinematicMotion cameraFlythrough = new CinematicMotion();
cameraFlythrough.target = cinematicCamera;
cameraFlythrough.duration = 10.0; // 10 seconds for the full path
cameraFlythrough.lookMode = CinematicLookMode.LookForwardPath;
cameraFlythrough.ease = 2.0; // Smoother movement
cameraFlythrough.startDelay = 1.0; // Start after 1 second
cameraFlythrough.activateOnCompletion = gameplayCamera; // Switch back to gameplay camera when done
cameraFlythrough.deactivateTarget = true; // Disable the cinematic camera when done

// Add path points as child objects to the CinematicMotion object
// Each child object's position and rotation will be used as a point on the path

// Create a character animation sequence
CinematicMotion characterSequence = new CinematicMotion();
characterSequence.target = npcCharacter;
characterSequence.lookMode = CinematicLookMode.FollowAnObject;
characterSequence.followObject = player; // NPC will look at the player while moving
characterSequence.transitionObject = dialogTrigger; // Activate dialog shortly before completion
```

## Implementation Details
- The path is created from child objects of the CinematicMotion object
- Time distribution along the path is based on point distances (further points take longer to reach)
- The transition object is activated 1 second before the end of the sequence
- When the sequence completes, the object is optionally deactivated, and another object can be activated

## Notes
- This component is ideal for cutscenes, camera flythroughs, and scripted character movements
- For proper path visualization, consider adding visual indicators for path points in your editor
- The path uses a `SmoothPath` class internally to handle interpolation between points

## Dependencies
- Uses `UniObjectUtil` for object manipulation
- Uses `SmoothPath` for path calculation and interpolation
- Uses `Time` for timing and delta time calculations
- Uses `VectorUtil` and `QuaternionUtil` for mathematical operations
