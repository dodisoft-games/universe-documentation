---
layout: default
title: CustomAiModelTemplate
nav_order: 12
parent: Scripting API
---
# CustomAiModelTemplate

## Description
The `CustomAiModelTemplate` class provides a template for creating custom AI behavior models for NPCs. It allows developers to implement custom decision making, action selection, collision handling, and event responses.

## Namespace
`Universe.Character`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| overrideDecision | bool | When true, custom decision logic is used (default: true) |
| overrideAction | bool | When true, custom action logic is used (default: true) |
| overrideCollision | bool | When true, custom collision handling is used (default: true) |
| overrideEvents | bool | When true, custom event handling is used (default: true) |
| controller | NpcController | Reference to the NPC controller this model works with |

## Methods

### OnDecision
```csharp
string OnDecision()
```
Called when the NPC needs to make a decision about its behavior. Should return a behavior identifier.

### OnAction
```csharp
string OnAction()
```
Called when the NPC needs to perform an action. Should return an action identifier.

### OnEvent
```csharp
string OnEvent(BehaviourType type, object data)
```
Called when an external event affects the NPC. Should return a behavior response.

#### Parameters
- `type`: The type of behavior or event
- `data`: Additional data related to the event

### OnCollision
```csharp
string OnCollision(UniObject other, bool entered)
```
Called when the NPC collides with another object. Should return a behavior response.

#### Parameters
- `other`: The object collided with
- `entered`: True if entering collision, false if exiting

### OnTrigger
```csharp
string OnTrigger(UniObject other, bool entered)
```
Called when the NPC enters or exits a trigger area. Should return a behavior response.

#### Parameters
- `other`: The trigger object
- `entered`: True if entering trigger, false if exiting

### SetController
```csharp
void SetController(NpcController refController)
```
Sets the reference to the NPC controller this model works with.

#### Parameters
- `refController`: Reference to the NPC controller

## Example Usage
```csharp
// Create a custom guard AI model
class GuardAiModel : CustomAiModelTemplate
{
    bool hasSeenIntruder = false;
    UniObject intruder = null;
    
    string OnDecision()
    {
        if (hasSeenIntruder && intruder != null)
        {
            // Return "chase" behavior
            return "chase";
        }
        else
        {
            // Return "patrol" behavior
            return "patrol";
        }
    }
    
    string OnEvent(BehaviourType type, object data)
    {
        if (type == BehaviourType.LookAt)
        {
            // Spotted an intruder
            intruder = data as UniObject;
            hasSeenIntruder = true;
            return "spotted_intruder";
        }
        return null;
    }
    
    string OnCollision(UniObject other, bool entered)
    {
        if (entered && other.tag == "player")
        {
            // Return "attack" behavior
            return "attack";
        }
        return null;
    }
}

// Apply the custom AI model to an NPC
NpcController guardController = new NpcController();
GuardAiModel guardAi = new GuardAiModel();
guardController.customAiModel = guardAi;
```

## Notes
- This is a template class designed to be inherited by custom AI implementations
- The return strings from these methods determine the NPC's behavior
- The actual behavior implementation happens in the NpcController
- Override only the methods needed for your custom AI behavior
- Return `null` from methods when you don't want to change the NPC's behavior

## Related Components
- Works with `NpcController.cs` which manages the NPC character
- Uses `BehaviourType` from `AI.cs` for event types
- Integrates with the character movement and animation systems

## Dependencies
- The custom AI model is connected to the NPC controller via `SetController()`
