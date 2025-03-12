---
layout: default
title: Light
nav_order: 25
parent: Scripting API
---
# Light

## Description
The `Light` class represents a light source in the game world. It supports different light types (spot, directional, point, and area) with configurable properties like intensity, range, angle, and color.

## Namespace
`Universe.Core`

## Enums

### LightType
Defines the type of light source.

| Value | Description |
|-------|-------------|
| Spot | Cone-shaped light that emanates from a point in a specific direction |
| Directional | Light that comes from a specific direction (like the sun) and affects all objects |
| Point | Light that emanates in all directions from a single point |
| Area | Light that emanates from a rectangular area |

## Properties
| Property  | Type      | Description                                           |
|-----------|-----------|-------------------------------------------------------|
| type      | LightType | The type of light (default: Directional)              |
| intensity | float     | Brightness of the light (default: 1)                  |
| range     | float     | Maximum distance the light reaches (default: 10)      |
| angle     | float     | Angle of the light cone for spot lights (default: 90) |
| shadows   | bool      | Whether the light casts shadows (default: true)       |
| color     | rgba      | Color of the light (default: white)                   |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the light with the lighting system.

## Example Usage
```csharp
// Create a directional sunlight
Light sunLight = new Light();
sunLight.type = LightType.Directional;
sunLight.intensity = 1.2;
sunLight.shadows = true;
sunLight.color = [1, 0.98, 0.95, 1]; // Slightly warm white

// Create a point light for a lamp
Light lampLight = new Light();
lampLight.type = LightType.Point;
lampLight.intensity = 0.8;
lampLight.range = 15;
lampLight.shadows = true;
lampLight.color = [1, 0.9, 0.7, 1]; // Warm yellowish light

// Create a spotlight for a flashlight
Light flashlight = new Light();
flashlight.type = LightType.Spot;
flashlight.intensity = 1.5;
flashlight.range = 20;
flashlight.angle = 35; // Narrow beam
flashlight.shadows = true;
flashlight.color = [1, 1, 1, 1]; // White light
```

## Technical Details
- Directional lights affect the entire scene and typically represent sunlight or moonlight
- Point lights emit in all directions and are good for lamps, torches, or explosions
- Spot lights emit in a cone shape and are useful for flashlights, car headlights, or focused beams
- Area lights emit from a rectangular surface and are useful for light panels, windows, or screens
- The actual range and intensity behavior may be affected by the renderer's lighting model
- The `angle` property only applies to spot lights and represents the full cone angle in degrees

## Notes
- For proper light and shadow effects, configure the lighting settings in the project
- Too many shadow-casting lights can impact performance, especially on mobile devices
- Consider using LightFlicker for dynamic lighting effects like torches or fires
- For global lighting and atmospheric effects, use the Environment class

## Related Components
- Can be used with `LightFlicker.cs` for dynamic lighting effects
- Works with `Environment.cs` for global lighting settings

## Dependencies
- Uses `LightUtil.AddLight()` to register with the lighting system
