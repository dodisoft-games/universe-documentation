---
layout: default
title: SmoothPath
nav_order: 43
parent: Scripting API
---
# SmoothPath

## Description
The `SmoothPath` class provides functionality for creating smooth interpolated paths between a series of points, with support for both position and rotation interpolation. It's useful for camera movements, object animations, and cinematic sequences.

## Namespace
`Universe.Helper`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| positions | List | List of position points along the path |
| rotations | List | List of rotation values at each point |
| times | List | List of time values for each point |
| duration | float | Total duration of the path traversal |
| index | int | Current index in the path |
| count | int | Total number of points in the path |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the lists needed for the path.

### SetPoints
```csharp
void SetPoints(list pts, float totalTime)
```
Sets up the path using a list of point objects and a total duration.

#### Parameters
- `pts`: List of point objects (UniObjects) defining the path
- `totalTime`: Total time to traverse the entire path

### CalculateDistances
```csharp
void CalculateDistances()
```
Calculates the distances between points and assigns appropriate time values.

### FindIndexOnTime
```csharp
int FindIndexOnTime(float time)
```
Finds the appropriate segment index for a given time.

#### Parameters
- `time`: The time value to find the index for

#### Returns
- The index of the segment containing the specified time

### GetPositionAtTime
```csharp
vector3 GetPositionAtTime(float time)
```
Gets the interpolated position at a specific time along the path.

#### Parameters
- `time`: The time value (0 to duration)

#### Returns
- The interpolated position at the specified time

### GetSmoothPosition
```csharp
vector3 GetSmoothPosition(float time, float damp)
```
Gets a smoothed position with damping for more fluid movement.

#### Parameters
- `time`: The current time value
- `damp`: Amount of damping to apply

#### Returns
- The smoothed position

### GetRotationAtTime
```csharp
quaternion GetRotationAtTime(float time)
```
Gets the interpolated rotation at a specific time along the path.

#### Parameters
- `time`: The time value (0 to duration)

#### Returns
- The interpolated rotation at the specified time

### GetSmoothRotation
```csharp
quaternion GetSmoothRotation(float time, float damp)
```
Gets a smoothed rotation with damping for more fluid rotation.

#### Parameters
- `time`: The current time value
- `damp`: Amount of damping to apply

#### Returns
- The smoothed rotation

## Example Usage
```csharp
// Create a camera path with several points
SmoothPath cameraPath = new SmoothPath();

// Create a list of path points
List pathPoints = new List();
pathPoints.Add(cameraPoint1);
pathPoints.Add(cameraPoint2);
pathPoints.Add(cameraPoint3);
pathPoints.Add(cameraPoint4);

// Set up the path with a 10-second duration
cameraPath.SetPoints(pathPoints.lst, 10.0);

// In an update method, move a camera along the path
void UpdateCameraPosition(float currentTime) {
    // Get the position and rotation at the current time
    vector3 position = cameraPath.GetPositionAtTime(currentTime);
    quaternion rotation = cameraPath.GetRotationAtTime(currentTime);
    
    // Apply to camera
    camera.position = position;
    camera.SetRotation(rotation);
}

// For smoother camera movement with damping
void UpdateSmoothCameraPosition(float currentTime) {
    vector3 position = cameraPath.GetSmoothPosition(currentTime, 0.5);
    quaternion rotation = cameraPath.GetSmoothRotation(currentTime, 0.3);
    
    camera.position = position;
    camera.SetRotation(rotation);
}
```

## Technical Details
- Path points are stored as separate position and rotation lists
- Time values are calculated based on the distance between points and the total duration
- Positions are linearly interpolated between path points
- Rotations are spherically interpolated (slerp) between path points
- The time values are not evenly distributed; longer segments take proportionally more time
- The `GetSmoothPosition` and `GetSmoothRotation` methods provide averaging between time points for smoother transitions

## Use Cases
- Camera movement paths for cinematic sequences
- Object animations along complex paths
- Character movement along predefined routes
- Spline-based vehicle or character movement
- Smooth transitions between key positions and orientations
- Animation of UI elements along paths

## Notes
- For best results, path points should be reasonably spaced
- Extremely sharp turns or sudden changes in direction might need additional points for smoothness
- The path should have at least two points for interpolation to work
- Time values are calculated proportionally to segment lengths, so longer segments take more time
- For very precise control, consider adjusting point positions
- This implementation uses linear interpolation for positions and spherical interpolation for rotations

## Related Components
- Works with `CinematicMotion.cs` for complex camera movements
- Can be used with any object that needs to follow a path

## Dependencies
- Uses `Universe.Core` namespace
- Uses `List` class for storing path data
- Uses `VectorUtil` and `QuaternionUtil` for mathematical operations
- Uses `Math` for various mathematical functions
