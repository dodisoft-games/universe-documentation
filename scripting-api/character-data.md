---
layout: default
title: CharacterData
nav_order: 9
parent: Scripting API
---
# CharacterData

## Description
The `CharacterData` class manages a character's attributes and stats such as health, stamina, strength, power, and inventory. It provides a foundation for implementing RPG-like character systems.

## Namespace
`Universe.Character`

## Properties
| Property          | Type  | Description                                                  |
|-------------------|-------|--------------------------------------------------------------|
| maxHealth         | float | Maximum health points the character can have (default: 100)  |
| maxStamina        | float | Maximum stamina points the character can have (default: 100) |
| maxStrength       | float | Maximum strength attribute (default: 100)                    |
| maxPower          | float | Maximum power attribute (default: 100)                       |
| maxAmmo           | float | Maximum ammunition the character can carry (default: 100)    |
| healthRegenPerSec | float | Rate of health regeneration per second (default: 0.1)        |

## Protected Fields
| Field     | Type  | Description                 |
|-----------|-------|-----------------------------|
| health    | float | Current health points       |
| stamina   | float | Current stamina points      |
| strength  | float | Current strength value      |
| power     | float | Current power value         |
| inventory | List  | Character's inventory items |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the character's attributes to their maximum values.

## Example Usage
```csharp
// Create a character with custom stats
Character warrior = new Character();
CharacterData warriorData = new CharacterData();
warriorData.maxHealth = 150;
warriorData.maxStamina = 120;
warriorData.maxStrength = 80;
warriorData.maxPower = 60;
warriorData.healthRegenPerSec = 0.2;
warrior.data = warriorData;

// Create a mage character
Character mage = new Character();
CharacterData mageData = new CharacterData();
mageData.maxHealth = 80;
mageData.maxStamina = 150;
mageData.maxStrength = 30;
mageData.maxPower = 150;
mageData.healthRegenPerSec = 0.15;
mage.data = mageData;
```

## Notes
- The `health` field is marked with `#` which likely indicates it's protected or has special access
- This class only provides the data structure for character stats; actual game mechanics (like taking damage or using abilities) would need to be implemented elsewhere
- The `inventory` field is initialized but not populated by default
- Health regeneration happens at a rate of `healthRegenPerSec` points per second, but the implementation of this regeneration is not shown in this class

## Related Components
- Used by `Character.cs` to manage character attributes
- May be referenced by `NpcController.cs` for AI decision making
- Could be accessed by combat or inventory systems

## Dependencies
- Uses `Universe.Core` namespace
- Uses `List` class for inventory management
