---
layout: default
title: AI
nav_order: 2
parent: Scripting API
---
# AI

## Description
The `AI.cs` file contains the `BehaviourType` enumeration which defines various AI behavior states used in NPC decision-making.

## Namespace
`Universe.Character`

## Enums

### BehaviourType
An enumeration defining the possible behavior states for AI-controlled characters.

| Value | Description |
|-------|-------------|
| Wait | AI stays idle and waits |
| HangAround | AI moves around in a relaxed manner without a specific destination |
| Go | AI moves to a destination at normal speed |
| GoFast | AI moves to a destination quickly |
| LookAt | AI turns to look at a point of interest |
| Attack | AI enters offensive behavior mode |
| Defend | AI enters defensive behavior mode |
| Follow | AI follows a target |
| Protect | AI protects a target or area |
| Escape | AI tries to retreat from danger |
| Jump | AI performs a jump |
| Animate | AI plays a specific animation |
| Action | AI performs a special action |
| Cancel | AI cancels its current behavior |

## Usage Context
This enumeration is typically used in NPC controllers and custom AI models to determine and set the behavior state of non-player characters. It provides the foundation for AI decision-making systems.

## Example Usage
```csharp
// In an NPC controller
if (enemyDetected) {
    // Set behavior to attack
    SetBehavior(BehaviourType.Attack);
} else if (playerNearby) {
    // Set behavior to follow
    SetBehavior(BehaviourType.Follow);
} else {
    // Default to hanging around
    SetBehavior(BehaviourType.HangAround);
}
```

## Related Components
- Works with `NpcController.cs`
- Used by `CustomAiModelTemplate.cs`
