---
layout: default
title: NpcController
nav_order: 33
parent: Scripting API
---
# NpcController

## Description
The `NpcController` class manages AI-controlled non-player characters (NPCs) in the game world. It handles movement, behavior, targeting, accessory management, and integration with navigation systems. This serves as the foundation for creating enemies, companions, and neutral characters with various AI behaviors.

## Namespace
`Universe.Character`

## Enums

### NPCType
Defines the basic disposition of the NPC.

| Value | Description |
|-------|-------------|
| Enemy | Hostile character that opposes the player |
| Companion | Friendly character that assists the player |
| UnBiased | Neutral character with no inherent alignment |

### Factor
Defines external factors that can influence NPC behavior.

| Value | Description |
|-------|-------------|
| Health | NPC's health status |
| Stamina | NPC's stamina/energy level |
| Strength | NPC's strength attribute |
| Power | NPC's power/magic attribute |
| Ammo | NPC's ammunition status |
| Hit | NPC has been hit/damaged |

## Properties
| Property | Type | Description |
|----------|------|-------------|
| character | Character | Reference to the Character component for movement and animation |
| npcType | NPCType | The disposition of the NPC (Enemy, Companion, or UnBiased) |
| leftHandAccessories | uniscript | Script controlling left-hand accessories/weapons |
| rightHandAccessories | uniscript | Script controlling right-hand accessories/weapons |
| colliderAttachment | UniObject | Collider used for interaction when the NPC is defeated |
| targetsTag | string | Tag used to automatically identify potential targets |
| active | bool | Whether the NPC's AI is currently active (default: true) |
| automaticTargeting | bool | Whether to automatically find targets with the specified tag |
| useNavigation | bool | Whether to use navigation system for pathfinding |
| overrideDimensions | bool | Whether to override the default character dimensions |
| radius | float | Collision radius if dimensions are overridden (default: 0.5) |
| height | float | Height if dimensions are overridden (default: 2) |
| stepHeight | float | Maximum step height if dimensions are overridden (default: 0.5) |
| slope | float | Maximum slope angle if dimensions are overridden (default: 45) |
| settingsAsset | UniAsset | Asset containing NPC behavior settings |
| customMotions | uniscript | Script containing custom motion/animation functions |

## Fields
| Field | Type | Description |
|-------|------|-------------|
| isAlive | bool | Whether the NPC is currently alive |
| isReady | bool | Whether the NPC is fully initialized and ready |
| settings | NpcSettings | Reference to the NPC's behavior settings |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the NPC controller and registers it with the AI system.

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Sets up navigation, targeting, and NPC settings.

### SetNpcSettings
```csharp
void SetNpcSettings()
```
Loads and applies behavior settings from the settings asset.

### SettingsRead
```csharp
void SettingsRead(UniObject settingsObject)
```
Callback for when settings are loaded. Initializes the NPC with the loaded settings.

#### Parameters
- `settingsObject`: The instantiated settings object

### SetTarget
```csharp
bool SetTarget(vector3 target)
```
Sets a position as the navigation target for the NPC.

#### Parameters
- `target`: World position to navigate to

#### Returns
- `true` if target was set successfully, `false` otherwise

### AddTargetObject
```csharp
void AddTargetObject(UniObject target)
```
Adds an object to the NPC's target list.

#### Parameters
- `target`: Object to target

### RemoveTargetObject
```csharp
void RemoveTargetObject(UniObject target)
```
Removes an object from the NPC's target list.

#### Parameters
- `target`: Object to remove from targets

### AssignTargetsAutomatically
```csharp
void AssignTargetsAutomatically(string targetTag)
```
Automatically finds and assigns objects with the specified tag as targets.

#### Parameters
- `targetTag`: Tag to search for when finding targets

### ExternalEvent
```csharp
void ExternalEvent(Factor factor, object value)
```
Triggers an external event that affects the NPC's behavior.

#### Parameters
- `factor`: The type of factor affecting the NPC
- `value`: Value associated with the factor

### Activate
```csharp
void Activate()
```
Activates the NPC's AI.

### DeActivate
```csharp
void DeActivate()
```
Deactivates the NPC's AI.

### Die
```csharp
void Die()
```
Handles NPC death, stopping movement and AI.

### DieLate
```csharp
void DieLate()
```
Delayed death handling, enabling collider for interaction.

### PlayCustomMotion
```csharp
void PlayCustomMotion(string motion)
```
Plays a custom animation/motion on the NPC.

#### Parameters
- `motion`: Name of the custom motion to play

### SelectRandomAccessory
```csharp
void SelectRandomAccessory()
```
Randomly selects accessories for the NPC's hands.

## Example Usage
```csharp
// Create a basic enemy NPC
NpcController enemyNpc = new NpcController();
enemyNpc.character = enemyCharacter;
enemyNpc.npcType = NPCType.Enemy;
enemyNpc.targetsTag = "player";
enemyNpc.automaticTargeting = true;
enemyNpc.useNavigation = true;
enemyNpc.settingsAsset = aggressiveNpcSettings;

// Create a companion NPC with custom dimensions
NpcController companionNpc = new NpcController();
companionNpc.character = companionCharacter;
companionNpc.npcType = NPCType.Companion;
companionNpc.overrideDimensions = true;
companionNpc.radius = 0.4;
companionNpc.height = 1.8;
companionNpc.useNavigation = true;
companionNpc.settingsAsset = friendlyNpcSettings;

// Later, give the companion a specific target
PlayerCharacter player = GetPlayerCharacter();
companionNpc.AddTargetObject(player);

// Trigger an external event on the NPC
enemyNpc.ExternalEvent(Factor.Hit, 25); // NPC took 25 damage
```

## Technical Details
- The NPC controller integrates with the navigation system for pathfinding
- Character movement and animation are handled through the Character component
- The AI decision-making is determined by the NpcSettings and optional CustomAiModel
- NPCs can automatically target objects with a specific tag
- External events can influence behavior based on the AI implementation
- Accessory scripts handle weapons or items held by the NPC
- Custom motion scripts provide additional animation capabilities

## Use Cases
- Enemies with different behavior patterns
- Friendly NPCs that follow and assist the player
- Neutral characters that react to player actions
- Quest givers and interactive characters
- Guard NPCs that patrol and respond to intruders
- Creatures with custom behaviors
- Companions with different personalities and abilities

## Notes
- For best results, combine with a custom AI model
- Navigation requires properly set up navigation data in the scene
- NPCs can be customized extensively through settings assets
- When an NPC "dies," it's not destroyed but deactivated for potential interaction
- Accessory management allows NPCs to use different weapons or items
- The `settingsAsset` should be a prefab containing an NpcSettings component

## Related Components
- Works with `Character.cs` for movement and animation
- Uses `NpcSettings.cs` for behavior configuration
- Can work with `CustomAiModelTemplate.cs` for advanced AI
- Integrates with navigation systems for pathfinding

## Dependencies
- Uses `Universe.Core` namespace
- Uses `AIUtil` for AI and navigation functions
- Uses `UniObjectUtil` for object instantiation and manipulation
- Uses `Utility.CallMethodDelayed()` for timing functions
