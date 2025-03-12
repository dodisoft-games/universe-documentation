---
layout: default
title: InteractableManager
nav_order: 21
parent: Scripting API
---
# InteractableManager

## Description
The `InteractableManager` class handles the discovery and management of interactive objects in the game world. It detects when the player enters trigger areas around interactable objects, manages interaction state, and coordinates with the inventory system for item collection.

## Namespace
`Universe.Tools`

## Properties

| Property         | Type             | Description                                                        |
|------------------|------------------|--------------------------------------------------------------------|
| interactableTag  | string           | Tag used to identify interactable objects (default: "interact")    |
| inventoryManager | InventoryManager | Reference to the inventory system                                  |
| playerCamera     | UniObject        | Reference to the player's camera                                   |
| playerModel      | UniObject        | Reference to the player's character model                          |
| isActive         | bool             | Whether the interaction system is currently active (default: true) |

## Events

| Event           | Parameters                               | Description                              |
|-----------------|------------------------------------------|------------------------------------------|
| OnInteractEvent | (string code, Interactable interactable) | Triggered when interaction state changes |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the interaction manager, creating the active interactables list.

### OnTriggerEnter
```csharp
void OnTriggerEnter(UniObject other)
```
Called when the player enters an interactable's trigger area. Starts the interaction if valid.

#### Parameters
- `other`: The object whose trigger was entered

### Open
```csharp
void Open(Interactable interactable)
```
Opens interaction with an interactable object.

#### Parameters
- `interactable`: The object to interact with

### OnTriggerExit
```csharp
void OnTriggerExit(UniObject other)
```
Called when the player leaves an interactable's trigger area. Ends the interaction if active.

#### Parameters
- `other`: The object whose trigger was exited

### Close
```csharp
void Close(Interactable interactable)
```
Closes interaction with an interactable object.

#### Parameters
- `interactable`: The object to stop interacting with

### OnActionHandler
```csharp
void OnActionHandler(string panel, string sender, string action, bool state, object data)
```
Handles input actions directed at the currently active interactable.

#### Parameters
- `panel`: UI panel that triggered the action
- `sender`: The element that triggered the action
- `action`: The action to perform
- `state`: State of the action (pressed/released)
- `data`: Additional data related to the action

### Pick
```csharp
void Pick(Interactable interactable)
```
Collects an interactable item and adds it to the inventory.

#### Parameters
- `interactable`: The item to pick up

### Drop
```csharp
void Drop(Interactable interactable)
```
Removes an item from inventory and places it in the world.

#### Parameters
- `interactable`: The item to drop

## Example Usage
```csharp
// Create an interaction manager for the player
InteractableManager playerInteractionManager = new InteractableManager();
playerInteractionManager.playerCamera = mainCamera;
playerInteractionManager.playerModel = playerCharacter;
playerInteractionManager.inventoryManager = playerInventory;

// Listen for interaction events
playerInteractionManager.OnInteractEvent += (code, interactable) => {
    if (code == "open") {
        // Player has started interacting with an object
        UI.ShowInteractionPrompt(interactable.infoText);
    }
    else if (code == "close") {
        // Player has stopped interacting with an object
        UI.HideInteractionPrompt();
    }
    else if (code == "pick") {
        // Player has picked up an item
        UI.ShowPickupNotification(interactable.id, interactable.amount);
    }
};

// Connect input system to interaction manager
inputController.OnActionEvent += (panel, sender, action, state, data) => {
    playerInteractionManager.OnActionHandler(panel, sender, action, state, data);
};
```

## Implementation Details
- The manager detects interactable objects when the player enters their trigger areas
- Multiple interactions can be active simultaneously, but are processed in a stack-like manner
- Interaction events are fired with different codes: "open", "close", "pick", "drop", "lock", "unlock"
- The manager integrates with the inventory system to handle item pickup and management
- Input actions are forwarded to the appropriate interactable objects

## Use Cases
- Player interaction with the game world
- Item collection and inventory management
- Environmental puzzles and object interaction
- Examining and manipulating game objects
- Doors, containers, and other interactive elements

## Notes
- The interaction manager should be attached to the player's collision trigger
- For proper function, interactable objects should have the correct tag
- The manager maintains a list of currently active interactables
- The "Close" action is handled specially to close the current interaction
- For networked games, ensure proper synchronization of pickup/drop events

## Related Components
- Works closely with `Interactable.cs` for object interaction
- Integrates with `InventoryManager.cs` for item management
- Uses player camera for interaction view management

## Dependencies
- Uses `Universe.Core` namespace
- Uses `List` class for tracking active interactables
