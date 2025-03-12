---
layout: default
title: NpcSettings
nav_order: 34
parent: Scripting API
---
# NpcSettings

## Description
The `NpcSettings` class defines the behavior parameters for non-player characters (NPCs). It controls personality traits, decision-making tendencies, and capabilities through numerical values and boolean flags.

## Namespace
`Universe.Character`

## Enums

### Mood
Defines the general personality type of the NPC.

| Value | Description |
|-------|-------------|
| Natural | Balanced, neutral disposition |
| Friendly | Positive attitude, helpful |
| Happy | Cheerful, optimistic |
| Coward | Easily frightened, avoids conflict |
| Angry | Irritable, prone to aggression |
| Aggressive | Highly combative, initiates conflict |
| Custom | Custom-defined mood through other parameters |

## Properties
| Property | Type | Description |
|----------|------|-------------|
| mood | Mood | The general personality type (affects behavior) |
| aggresiveness | float | Tendency to engage in combat (0-100, default: 30) |
| intelligence | float | Decision-making sophistication (0-100, default: 40) |
| randomness | float | Unpredictability in behaviors (0-100, default: 50) |
| learningSkills | float | Ability to adapt to player strategies (0-100, default: 30) |
| follow | bool | Whether the NPC will follow targets (default: true) |
| attack | bool | Whether the NPC can attack (default: true) |
| protect | bool | Whether the NPC will protect allies (default: true) |
| useWeapon | bool | Whether the NPC can use weapons (default: true) |
| selfDefend | bool | Whether the NPC will defend itself when attacked (default: true) |
| targetInSight | bool | Whether the NPC requires line of sight to targets (default: true) |
| customAiModel | uniscript | Reference to a custom AI model script for advanced behavior |

## Methods

### Init
```csharp
void Init(NpcController controller)
```
Initializes the settings with a reference to the NPC controller.

#### Parameters
- `controller`: The NPC controller that will use these settings

## Example Usage
```csharp
// Create aggressive enemy NPC settings
NpcSettings enemySettings = new NpcSettings();
enemySettings.mood = Mood.Aggressive;
enemySettings.aggresiveness = 80;
enemySettings.intelligence = 60;
enemySettings.randomness = 30;
enemySettings.follow = true;
enemySettings.attack = true;
enemySettings.protect = false; // Doesn't care about allies
enemySettings.selfDefend = true;
enemySettings.targetInSight = true;

// Create cowardly NPC settings
NpcSettings cowardSettings = new NpcSettings();
cowardSettings.mood = Mood.Coward;
cowardSettings.aggresiveness = 10;
cowardSettings.intelligence = 70;
cowardSettings.randomness = 20;
cowardSettings.follow = false; // Won't follow player
cowardSettings.attack = false; // Won't initiate attacks
cowardSettings.protect = false;
cowardSettings.selfDefend = true; // Will try to defend itself if cornered
cowardSettings.targetInSight = true;

// Create a friendly companion NPC settings
NpcSettings companionSettings = new NpcSettings();
companionSettings.mood = Mood.Friendly;
companionSettings.aggresiveness = 50; // Moderately aggressive toward enemies
companionSettings.intelligence = 80;
companionSettings.randomness = 30;
companionSettings.follow = true; // Will follow player
companionSettings.attack = true; // Will attack enemies
companionSettings.protect = true; // Will protect player
companionSettings.selfDefend = true;
companionSettings.targetInSight = false; // Can sense enemies even without sight
```

## Technical Details
- The `mood` property serves as a preset that can influence the default behavior
- Numerical values (aggresiveness, intelligence, etc.) range from 0 to 100
- Higher aggresiveness means the NPC is more likely to engage in combat
- Higher intelligence allows for more sophisticated decision-making and tactics
- Higher randomness introduces more variation in behavior
- Higher learningSkills means the NPC adapts more quickly to player strategies
- Boolean properties enable or disable specific capabilities
- The `customAiModel` allows implementing completely custom behavior logic

## Use Cases
- Configuring enemy difficulty and behavior
- Creating different personality types for NPCs
- Defining companion behavior preferences
- Setting up neutral characters with varying dispositions
- Creating progressive difficulty with increasingly sophisticated enemies
- Implementing faction-based AI behaviors

## Notes
- For best results, balance the numerical values based on game difficulty
- The `mood` enum provides basic presets, but fine-tuning requires adjusting individual properties
- Consider creating a variety of settings presets for different NPC types
- The `customAiModel` is optional but allows for more complex behavior beyond the basic parameters
- These settings are typically created in the editor and assigned via `settingsAsset` in the NpcController

## Related Components
- Used by `NpcController.cs` to determine NPC behavior
- Can reference `CustomAiModelTemplate.cs` implementations for advanced AI

## Dependencies
- When using a custom AI model, calls the model's `SetController` method during initialization
