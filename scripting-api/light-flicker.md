---
layout: default
title: LightFlicker
nav_order: 24
parent: Scripting API
---
# LightFlicker

## Description
The `LightFlicker` class adds dynamic flickering effects to light sources, simulating the natural variations seen in flames, old light bulbs, or damaged electrical sources. It can create both subtle variations and more dramatic cutoffs.

## Namespace
`Universe.Tools`

## Properties
| Property  | Type  | Description                                              |
|-----------|-------|----------------------------------------------------------|
| flactuate | float | Intensity of the fluctuation effect (default: 1)         |
| speed     | float | Speed of the fluctuation transitions (default: 10)       |
| cutOff    | bool  | Whether the light should occasionally cut off completely |

## Fields
| Field       | Type  | Description                                              |
|-------------|-------|----------------------------------------------------------|
| light       | Light | Reference to the Light component to affect               |
| intensity   | float | Base intensity of the light                              |
| toIntensity | float | Target intensity during transitions                      |
| range       | float | Base range of the light                                  |
| toRange     | float | Target range during transitions                          |
| changeTime  | float | Time for the next fluctuation change                     |
| nextCutOff  | float | Time for the next cutoff event                           |
| emit        | bool  | Whether the light is currently emitting (during cutoffs) |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Gets a reference to the Light component and stores the base values.

### OnUpdate
```csharp
void OnUpdate()
```
Called every frame. Updates the light properties with random variations to create the flickering effect.

## Example Usage
```csharp
// Create a subtle candle flicker
Light candleLight = new Light();
candleLight.type = LightType.Point;
candleLight.intensity = 0.7;
candleLight.range = 5;
candleLight.color = [1, 0.7, 0.3, 1]; // Orange-yellow

LightFlicker candleFlicker = new LightFlicker();
candleFlicker.flactuate = 0.5; // Subtle variations
candleFlicker.speed = 5; // Moderately slow changes
candleFlicker.cutOff = false; // No complete cutoffs

// Create a damaged electrical light
Light electricLight = new Light();
electricLight.type = LightType.Point;
electricLight.intensity = 1.2;
electricLight.range = 8;
electricLight.color = [0.9, 0.95, 1, 1]; // Slightly blue-white

LightFlicker electricFlicker = new LightFlicker();
electricFlicker.flactuate = 2; // Stronger variations
electricFlicker.speed = 15; // Rapid changes
electricFlicker.cutOff = true; // Occasional complete cutoffs

// Create a campfire with medium flicker
Light fireLight = new Light();
fireLight.type = LightType.Point;
fireLight.intensity = 1.5;
fireLight.range = 10;
fireLight.color = [1, 0.6, 0.2, 1]; // Orange

LightFlicker fireFlicker = new LightFlicker();
fireFlicker.flactuate = 1; // Medium variations
fireFlicker.speed = 8; // Moderate speed
fireFlicker.cutOff = false; // No complete cutoffs
```

## Implementation Details
- The flickering effect varies both the intensity and range of the light
- Changes in intensity are proportional to the base intensity value
- Changes in range are smaller than intensity changes to create a more natural effect
- When `cutOff` is enabled, the light will randomly turn off completely for short periods
- The actual fluctuation amount is determined by `flactuate / 10` for intensity and `flactuate / 40` for range
- New target values are selected approximately every 0.25 seconds
- When cut off, the light stays off for 0.1-0.2 seconds and then on for 0.1-1 seconds

## Use Cases
- Candles, torches, and other flame light sources
- Damaged electrical lights
- Car headlights on rough terrain
- Magic or supernatural light effects
- Old, unstable light bulbs
- Emergency lighting or warning beacons

## Notes
- For subtle effects, use lower `flactuate` values (0.2-0.5)
- For dramatic effects, use higher values (1.5-3) and enable `cutOff`
- The `speed` parameter affects how quickly the light transitions between states
- For performance reasons, avoid having too many flickering lights in a scene
- Flickering shadows can be computationally expensive, consider using shadowless lights for minor light sources

## Related Components
- Works with `Light.cs` to create the flickering effect

## Dependencies
- Uses `Universe.Core` namespace
- Requires a `Light` component on the same object
- Uses `UniObjectUtil.GetScriptByName()` to find the Light component
- Uses `Time.GameTime()` and `Time.DeltaTime()` for timing
- Uses `Math.Random()` and `Math.Lerp()` for value generation and interpolation
