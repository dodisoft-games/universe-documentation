---
layout: default
title: Environment
nav_order: 16
parent: Scripting API
---
# Environment

## Description
The `Environment` class provides functionality for controlling global environmental lighting and fog settings. It allows easy configuration of ambient lighting gradients and fog density to create different atmospheric effects.

## Namespace
`Universe.Helper`

## Properties
| Property    | Type  | Description                                                                        |
|-------------|-------|------------------------------------------------------------------------------------|
| fog         | bool  | Enables or disables fog in the scene                                               |
| fogDensity  | float | Density of the fog when enabled (default: 0.02)                                    |
| fogColor    | rgba  | Color of the fog (default: white)                                                  |
| skyColor    | rgba  | Color of the ambient light from the sky/above (default: white)                     |
| medianColor | rgba  | Color of the ambient light from the sides (default: light gray [0.8, 0.8, 0.8, 1]) |
| groundColor | rgba  | Color of the ambient light from below (default: dark gray [0.2, 0.2, 0.2, 1])      |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Applies all environment settings to the scene.

## Example Usage
```csharp
// Create a sunny day environment
Environment sunnyDay = new Environment();
sunnyDay.fog = false;
sunnyDay.skyColor = [0.8, 0.9, 1.0, 1.0]; // Light blue sky
sunnyDay.medianColor = [0.7, 0.7, 0.7, 1.0];
sunnyDay.groundColor = [0.3, 0.3, 0.3, 1.0];

// Create a foggy environment
Environment foggyDay = new Environment();
foggyDay.fog = true;
foggyDay.fogDensity = 0.03; // Thicker fog
foggyDay.fogColor = [0.8, 0.8, 0.9, 1.0]; // Bluish-gray fog
foggyDay.skyColor = [0.7, 0.7, 0.8, 1.0]; // Overcast sky
foggyDay.medianColor = [0.6, 0.6, 0.6, 1.0];
foggyDay.groundColor = [0.2, 0.2, 0.2, 1.0];

// Create a sunset environment
Environment sunset = new Environment();
sunset.fog = true;
sunset.fogDensity = 0.01; // Light atmospheric fog
sunset.fogColor = [1.0, 0.6, 0.4, 1.0]; // Orange-red fog
sunset.skyColor = [1.0, 0.5, 0.3, 1.0]; // Orange-red sky
sunset.medianColor = [0.7, 0.4, 0.3, 1.0];
sunset.groundColor = [0.3, 0.2, 0.2, 1.0];
```

## Technical Details
- The ambient light uses a gradient system with three colors: sky (above), median (middle/sides), and ground (below)
- These colors create a more natural lighting effect than a single ambient color
- Fog creates distance-based color blending toward the fog color
- Higher fog density values make the fog effect stronger and reduce visibility distance

## Use Cases
- Creating different times of day
- Simulating weather conditions
- Setting mood and atmosphere for different environments
- Creating visual distance cues through fog

## Notes
- Only one Environment component should be active at a time
- Changes to the Environment settings at runtime will only take effect if the OnStart method is called
- For dynamic time-of-day systems, you might need to modify the environment properties and call the LightUtil methods directly

## Dependencies
- Uses `LightUtil` to apply environmental settings
