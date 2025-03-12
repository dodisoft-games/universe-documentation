---
layout: default
title: SetShader
nav_order: 40
parent: Scripting API
---
# SetShader

## Description
The `SetShader` class provides a simple way to assign a specific shader type to an object's material. It allows changing the rendering characteristics of an object without needing to create and configure an entire material.

## Namespace
`Universe.Helper`

## Enums

### Shaders
Defines the types of shaders available for assignment.

| Value | Description |
|-------|-------------|
| Opaque | Standard opaque shader, suitable for most solid objects |
| Transparent | Shader that supports transparency/alpha, for glass, water, etc. |
| Particle | Specialized shader for particle effects |

## Properties

| Property | Type    | Description                            |
|----------|---------|----------------------------------------|
| shader   | Shaders | The shader type to apply to the object |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Applies the specified shader to the object's material.

## Example Usage
```csharp
// Set a standard opaque shader
SetShader rockShader = new SetShader();
rockShader.shader = Shaders.Opaque;

// Set a transparent shader for glass
SetShader glassShader = new SetShader();
glassShader.shader = Shaders.Transparent;

// Set a particle shader for effects
SetShader fireEffectShader = new SetShader();
fireEffectShader.shader = Shaders.Particle;
```

## Technical Details
- The shader is applied during initialization and doesn't change afterwards
- The method uses `UniObjectUtil.GetUniObject(this)` to get the target object
- The actual shader application is handled by the object's `SetShader` method
- This component changes only the shader type, not other material properties
- The available shader types are predefined in the `Shaders` enum

## Use Cases
- Setting transparent shaders for windows, glass, or water
- Setting particle shaders for effects like fire, smoke, or magic
- Ensuring correct shader properties for different object types
- Quick shader assignment without material creation
- Converting between opaque and transparent rendering

## Notes
- For more complex material configurations, consider using a custom script
- This component only sets the shader type, not specific shader parameters
- The shader is applied only once during initialization
- To change shaders dynamically, you need to call the object's SetShader method directly
- Material/shader changes can affect performance, especially on mobile platforms

## Related Components
- Can be used with `SetTexture.cs` to configure both texture and shader
- Complements rendering and visual effect components

## Dependencies
- Uses `UniObjectUtil.GetUniObject()` to get a reference to the target object
