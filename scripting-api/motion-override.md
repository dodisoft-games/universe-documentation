---
layout: default
title: MotionOverride
nav_order: 28
parent: Scripting API
---
# MotionOverride

## Description
The `MotionOverride` class allows customization of a character's animation set by overriding the default animation assets with custom ones. This enables unique movement styles and actions for different characters while maintaining the same core character controller functionality.

## Namespace
`Universe.Character`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| idle | UniAsset | Animation played when the character is standing still |
| run | UniAsset | Animation played when the character is running forward |
| runBack | UniAsset | Animation played when the character is running backward |
| jump | UniAsset | Animation played when the character is jumping |
| walk | UniAsset | Animation played when the character is walking forward |
| walkBack | UniAsset | Animation played when the character is walking backward |
| walkLeft | UniAsset | Animation played when the character is walking to the left |
| walkRight | UniAsset | Animation played when the character is walking to the right |
| turnLeft | UniAsset | Animation played when the character is turning left |
| turnRight | UniAsset | Animation played when the character is turning right |
| climbIdle | UniAsset | Animation played when the character is idle on a climbing surface |
| climbUp | UniAsset | Animation played when the character is climbing upward |
| climbDown | UniAsset | Animation played when the character is climbing downward |
| climbLeft | UniAsset | Animation played when the character is climbing to the left |
| climbRight | UniAsset | Animation played when the character is climbing to the right |
| swim | UniAsset | Animation played when the character is swimming |
| dive | UniAsset | Animation played when the character is diving underwater |
| fall | UniAsset | Animation played when the character is falling |
| crouch | UniAsset | Animation played when the character is crouching |
| drop | UniAsset | Animation played when the character is dropping from a height |
| punch | UniAsset | Animation played when the character is punching |
| kick | UniAsset | Animation played when the character is kicking |
| pistol | UniAsset | Animation played when the character is using a pistol |
| riffle | UniAsset | Animation played when the character is using a rifle |
| sit | UniAsset | Animation played when the character is sitting |
| lay | UniAsset | Animation played when the character is lying down |

## Example Usage
```csharp
// Create a zombie character with unique animations
Character zombieCharacter = new Character();
MotionOverride zombieMotions = new MotionOverride();

// Set basic locomotion animations
zombieMotions.idle = zombieIdleAnimation;
zombieMotions.walk = zombieWalkAnimation;
zombieMotions.run = zombieRunAnimation;
zombieMotions.jump = zombieJumpAnimation;
zombieMotions.fall = zombieFallAnimation;

// Set combat animations
zombieMotions.punch = zombiePunchAnimation;
zombieMotions.kick = zombieKickAnimation;

// Assign the custom animations to the character
zombieCharacter.overrideMotions = zombieMotions;

// Create a robot character with mechanical movements
Character robotCharacter = new Character();
MotionOverride robotMotions = new MotionOverride();

// Set robot-specific animations
robotMotions.idle = robotIdleAnimation;
robotMotions.walk = robotWalkAnimation;
robotMotions.run = robotRunAnimation;
// ... and so on for other animations

// Assign the custom animations to the character
robotCharacter.overrideMotions = robotMotions;
```

## Technical Details
- Each property corresponds to a specific animation state in the character controller
- When a property is set, the corresponding animation will be used instead of the default one
- Properties that are left as null will fall back to the default animations
- The animations are applied through the Character class's animation system
- For blending between animations, the Character class handles the transitions

## Use Cases
- Creating unique character types with distinct movement styles
- Implementing character customization options
- Supporting different animation sets for various character models
- Creating specialized NPCs with unique behaviors
- Implementing different animation styles for various weapons or tools

## Notes
- Animation assets should be compatible with the character's skeleton rig
- Some animation states may require specific transitions or blending parameters
- Not all characters may support all animation states (e.g., swimming might not be used in a desert game)
- For completely custom animation systems, you might need to implement a custom Character class
- Properties are applied individually, so you can override just a subset of animations

## Related Components
- Used by `Character.cs` to customize animation behavior
- Works with animation assets loaded through the `UniAsset` system

## Dependencies
- No direct method calls or initialization required
- Relies on the Character class to apply the animation overrides
