---
layout: default
title: Enums
nav_order: 15
parent: Scripting API
---
# Enums

## Description
The `Enums.cs` file contains several important enumeration types used throughout the Character system in the Universe framework. These enumerations define character bones, movement types, facial expressions, and basic actions.

## Namespace
`Universe.Character`

## Enums

### CharacterBone
Defines the bones that can be targeted for attachments, IK control, or animation.

| Value | Description |
|-------|-------------|
| Head | The character's head |
| Chest | The character's chest |
| Belly | The character's stomach area |
| Hips | The character's pelvis/hip area |
| LeftShoulder | The character's left shoulder |
| LeftUpperArm | The character's left upper arm |
| LeftLowerArm | The character's left forearm |
| LeftHand | The character's left hand |
| RightShoulder | The character's right shoulder |
| RightUpperArm | The character's right upper arm |
| RightLowerArm | The character's right forearm |
| RightHand | The character's right hand |
| LeftUpperLeg | The character's left thigh |
| LeftLowerLeg | The character's left calf |
| LeftFoot | The character's left foot |
| RightUpperLeg | The character's right thigh |
| RightLowerLeg | The character's right calf |
| RightFoot | The character's right foot |

### Movements
Defines the character's current movement state or locomotion type.

| Value | Description |
|-------|-------------|
| Walking | Character is walking or running on ground |
| Climbing | Character is climbing a ladder or wall |
| Swimming | Character is swimming in water |
| Flying | Character is flying or gliding through air |
| Falling | Character is falling due to gravity |

### FacialExpression
Defines facial expressions that can be applied to the character.

| Value | Description |
|-------|-------------|
| Natural | Default neutral expression |
| Happy | Pleased, content expression |
| Smiling | Smiling expression |
| Sad | Unhappy, downcast expression |
| Tearful | Crying or about to cry |
| Furious | Extremely angry expression |
| Screaming | Shouting, yelling expression |
| Shocked | Surprised, startled expression |
| Pensive | Thoughtful, contemplative expression |
| Confused | Puzzled, perplexed expression |
| Wink | Winking one eye |
| Blink | Blinking both eyes |

### Actions
Defines basic actions a character can perform.

| Value | Description |
|-------|-------------|
| Jump | Character performs a jump |

## Example Usage
```csharp
// Attach item to character's hand
AccessoryAttachment weaponAttachment = new AccessoryAttachment();
weaponAttachment.character = playerCharacter;
weaponAttachment.bone = CharacterBone.RightHand;
weaponAttachment.autoAttach = true;

// Set character's facial expression
playerCharacter.SetFacialExpression(FacialExpression.Happy);

// Check if character is swimming
if (playerCharacter.status == Movements.Swimming) {
    // Apply swimming effects
    PlaySwimmingSound();
    ApplyWaterPhysics();
}

// Make character jump
playerCharacter.Jump(true);
```

## Notes
- The `CharacterBone` enum corresponds to the standard humanoid skeleton rig
- `Movements` is used to track and respond to the character's current locomotion state
- `FacialExpression` requires character models with facial animation support
- The `Actions` enum currently only includes Jump but may be expanded in future versions

## Related Components
- Used by `Character.cs` for movement states and actions
- Used by `AccessoryAttachment.cs` for attaching items to bones
- Used by `IKHandler.cs` for inverse kinematics control
- Used by animation systems for transitioning between movement types
