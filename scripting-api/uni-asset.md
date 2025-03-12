---
layout: default
title: UniAsset
nav_order: 49
parent: Scripting API
---
# UniAsset

## Description
The `UniAsset` class represents a reference to an external asset resource such as a model, texture, audio clip, or animation. It provides basic information about the asset and allows scripts to refer to resources without loading them directly.

## Properties
None declared in the class definition, but this class serves as a reference type for assets.

## Methods

### GetAssetName
```csharp
string GetAssetName()
```
Gets the name of the asset.

#### Returns
- The name of the asset as a string

### GetAssetType
```csharp
string GetAssetType()
```
Gets the type of the asset (e.g., "Texture", "Model", "Audio", etc.).

#### Returns
- The type of the asset as a string

## Example Usage
```csharp
// Reference assets in a component
AudioPlayer soundEffect = new AudioPlayer();
soundEffect.clip = explosionSoundAsset; // UniAsset reference

// Get information about an asset
string assetName = explosionSoundAsset.GetAssetName(); // e.g., "explosion_1"
string assetType = explosionSoundAsset.GetAssetType(); // e.g., "Audio"

// Use asset references in a character component
Character playerCharacter = new Character();
MotionOverride customMotions = new MotionOverride();
customMotions.idle = idleAnimationAsset; // UniAsset reference
customMotions.walk = walkAnimationAsset; // UniAsset reference
customMotions.run = runAnimationAsset; // UniAsset reference
playerCharacter.overrideMotions = customMotions;

// Reference textures
SetTexture wallTexture = new SetTexture();
wallTexture.texture = brickTextureAsset; // UniAsset reference

// Log asset information for debugging
void LogAssetInfo(UniAsset asset) {
    Debug.Log("Asset: " + asset.GetAssetName());
    Debug.Log("Type: " + asset.GetAssetType());
}
```

## Technical Details
- UniAsset is a lightweight reference to an external resource
- The actual asset loading and management is handled by the framework
- Assets are typically assigned in the editor or through resource loading systems
- The `GetAssetName()` and `GetAssetType()` methods use `Utility.GetAssetName()` and `Utility.GetAssetType()` internally

## Use Cases
- Referencing audio clips for sound effects and music
- Specifying animations for characters
- Assigning textures to materials
- Referencing prefabs for instantiation
- Specifying UI assets like icons and fonts
- Loading configuration data from asset files
- Referencing special effect assets

## Notes
- UniAsset references do not guarantee that the asset is loaded in memory
- The framework handles loading and unloading assets as needed
- For dynamic asset loading at runtime, consider using a resource management system
- Asset paths and naming conventions may be important depending on the project structure
- Assets are typically assigned through the editor interface rather than created at runtime

## Related Components
- Used by many components that need asset references:
  - `AudioPlayer.cs` for audio clips
  - `Character.cs` for animations
  - `MotionOverride.cs` for custom animations
  - `SetTexture.cs` for textures
  - `NpcController.cs` for settings
  - And many others

## Dependencies
- Uses `Utility.GetAssetName()` and `Utility.GetAssetType()` for asset information
