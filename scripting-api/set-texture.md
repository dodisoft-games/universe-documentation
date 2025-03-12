---
layout: default
title: SetTexture
nav_order: 41
parent: Scripting API
---
# SetTexture

## Description
The `SetTexture` class provides a simple way to assign a texture to an object's material. It allows changing the visual appearance of an object without creating and configuring an entire material.

## Namespace
`Universe.Helper`

## Properties

| Property | Type     | Description                              |
|----------|----------|------------------------------------------|
| texture  | UniAsset | The texture asset to apply to the object |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Applies the specified texture to the object's material.

## Example Usage
```csharp
// Set a basic texture on a wall
SetTexture wallTexture = new SetTexture();
wallTexture.texture = brickTextureAsset;

// Apply a special texture to an object
SetTexture specialTexture = new SetTexture();
specialTexture.texture = glowingTextureAsset;

// Change the texture on a terrain section
SetTexture grassTexture = new SetTexture();
grassTexture.texture = grassTextureAsset;
```

## Technical Details
- The texture is applied during initialization and doesn't change afterwards
- The method uses `UniObjectUtil.SetTexture(this, texture)` to apply the texture
- This component changes only the main/diffuse texture, not other material properties
- The texture asset must be a valid image file loaded as a UniAsset

## Use Cases
- Applying different textures to architectural elements
- Setting character or NPC appearances
- Creating variety in repeated objects with the same geometry
- Implementing simple texture changes without material creation
- Applying decals or overlays to surfaces

## Notes
- For more complex material configurations, consider using a custom script
- This component only sets the main texture, not normal maps, emission maps, etc.
- The texture is applied only once during initialization
- To change textures dynamically, you need to call the UniObjectUtil.SetTexture method directly
- Large textures can impact performance and memory usage, especially on mobile platforms

## Related Components
- Can be used with `SetShader.cs` to configure both texture and shader
- Complements visual appearance components

## Dependencies
- Uses `UniObjectUtil.SetTexture()` to apply the texture
- Requires a valid texture asset in the `texture` property
