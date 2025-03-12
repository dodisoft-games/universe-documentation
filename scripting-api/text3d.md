---
layout: default
title: Text3D
nav_order: 46
parent: Scripting API
---
# Text3D

## Description
The `Text3D` class enables the creation of three-dimensional text rendered directly in the 3D world space. This is useful for creating signs, labels, nameplates, markers, or any text that should exist as part of the 3D environment rather than on the 2D UI layer.

## Namespace
`Universe.Core`

## Properties
| Property | Type   | Description                                      |
|----------|--------|--------------------------------------------------|
| text     | string | The text content to display (default: "3D Text") |
| fontSize | float  | The size of the text (default: 1)                |
| color    | rgba   | The color of the text (default: white)           |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Creates the 3D text object with the specified settings.

## Example Usage
```csharp
// Create a sign with player instructions
Text3D instructionSign = new Text3D();
instructionSign.text = "Press 'E' to interact";
instructionSign.fontSize = 0.5; // Smaller text
instructionSign.color = [1, 0.8, 0, 1]; // Yellow text

// Create a character nameplate
Text3D nameplate = new Text3D();
nameplate.text = "Captain Smith";
nameplate.fontSize = 0.3;
nameplate.color = [0.2, 0.6, 1, 1]; // Blue text

// Create a large warning message
Text3D warningText = new Text3D();
warningText.text = "DANGER!";
warningText.fontSize = 2.0; // Large text
warningText.color = [1, 0, 0, 1]; // Red text
```

## Technical Details
- The text is rendered as a 3D object in the world space
- The actual text rendering is handled by `UniObjectUtil.Add3DText()`
- The text faces the direction of the object it's attached to
- For text that should always face the camera, combine with a `FaceToCamera` component
- The text is affected by lighting in the 3D environment
- The text inherits the position, rotation, and scale of its parent object

## Use Cases
- Signs and labels in the game environment
- Character nameplates or status indicators
- Waypoint markers with distance information
- Interactive object labels
- Floating damage numbers or status effects
- Environmental storytelling elements
- Debug information displayed in the 3D world

## Notes
- For UI text that should remain on screen regardless of camera position, use UI components instead
- Text3D objects are affected by occlusion, meaning they can be blocked by other objects
- For best readability, consider the background behind the text and choose contrasting colors
- The appearance may vary based on the font used by the engine
- For very small text, increase the font size and scale down the parent object for better quality
- For text that should be readable from any angle, consider using `FaceToCamera.cs`

## Related Components
- Can be combined with `FaceToCamera.cs` to make the text always face the player
- Works well with `Interactable.cs` for labeling interactive elements

## Dependencies
- Uses `UniObjectUtil.Add3DText()` for creation and rendering
