---
layout: default
title: Interactable
nav_order: 22
parent: Scripting API
---
# Interactable

## Description
The `Interactable` class provides a comprehensive system for creating interactive objects in the game world. It supports various types of interactions, from collectible items to doors, puzzles, and other interactive elements. This class manages the entire interaction lifecycle including visual representation, UI feedback, audio cues, and inventory integration.

## Namespace
`Universe.Tools`

## Enums

### InteractType
Defines the category of interactive object.

| Value | Description |
|-------|-------------|
| Treasure | Valuable items, rewards |
| Key | Keys used to unlock other interactables |
| Hint | Clues or information items |
| Weapon | Weapons that can be equipped |
| Potion | Consumable items with effects |
| Puzzle | Objects that require solving |
| Inventory | General inventory items |
| Door | Doors, gates, and other passage controls |
| Other | Miscellaneous interactive objects |

### CarryOn
Defines how an object is carried when collected.

| Value | Description |
|-------|-------------|
| Hidden | Object is not visibly carried |
| LeftHand | Object is carried in the left hand |
| RightHand | Object is carried in the right hand |

## Properties
| Property          | Type          | Description                                              |
|-------------------|---------------|----------------------------------------------------------|
| type              | InteractType  | The category of the interactive object                   |
| model             | UniObject     | Visual model of the interactable                         |
| uiPanel           | UIPanel       | UI panel to show when interacting                        |
| amount            | int           | Quantity of the item (default: 1)                        |
| id                | string        | Unique identifier for the item                           |
| infoText          | string        | Description text to display                              |
| lockPlayer        | bool          | Whether interaction locks player movement                |
| autoUse           | bool          | Whether item is used automatically upon interaction      |
| collectable       | bool          | Whether item can be picked up                            |
| collectAction     | string        | Action name that triggers collection (default: "Action") |
| caryOn            | CarryOn       | How the object is carried when collected                 |
| networkObject     | NetworkObject | Network synchronization reference                        |
| 3rdViewCamera     | UniObject     | Camera used for examining the object                     |
| characterPosition | UniObject     | Position for character during interaction                |
| extraData         | string        | Additional custom data                                   |
| infoSound         | UniAsset      | Sound played when examining                              |
| pickSound         | UniAsset      | Sound played when picking up                             |
| dropSound         | UniAsset      | Sound played when dropping                               |

## Events
| Event            | Parameters                                                                         | Description                                                      |
|------------------|------------------------------------------------------------------------------------|------------------------------------------------------------------|
| OnOpenCloseEvent | (Interactable interactable, bool isOpen)                                           | Triggered when interaction starts or ends                        |
| OnCommandEvent   | (Interactable interactable, string sender, string action, bool state, object data) | Triggered when the player performs an action on the interactable |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the interactable, setting up references and network synchronization.

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Records the initial position and rotation.

### OnSync
```csharp
void OnSync()
```
Called during network synchronization. Updates visibility state.

### Open
```csharp
void Open(InteractableManager manager)
```
Begins interaction with the object, showing UI and playing sounds.

#### Parameters
- `manager`: The interaction manager handling this interaction

### Command
```csharp
void Command(string panel, string sender, string action, bool state, object data)
```
Handles player commands directed at this interactable.

#### Parameters
- `panel`: UI panel that triggered the command
- `sender`: The element that triggered the command
- `action`: The action to perform
- `state`: State of the action (pressed/released)
- `data`: Additional data related to the action

### Close
```csharp
void Close()
```
Ends interaction with the object, hiding UI and restoring camera.

### Pick
```csharp
void Pick()
```
Collects the item, making it disappear from the world and playing pickup sound.

### Drop
```csharp
void Drop(vector3 position, vector3 rotation)
```
Places the item back into the world at the specified position and rotation.

#### Parameters
- `position`: World position to drop the item
- `rotation`: Rotation to apply to the dropped item

### Destroy
```csharp
void Destroy()
```
Permanently destroys the interactable object.

## Example Usage
```csharp
// Create a treasure chest
Interactable chest = new Interactable();
chest.type = InteractType.Treasure;
chest.model = chestModel;
chest.uiPanel = treasureUI;
chest.infoText = "An ancient treasure chest. It might contain valuable items.";
chest.collectable = false; // Can't pick up the chest itself
chest.lockPlayer = true; // Player can't move while interacting
chest.infoSound = chestOpenSound;

// Create a potion item
Interactable healthPotion = new Interactable();
healthPotion.type = InteractType.Potion;
healthPotion.model = potionModel;
healthPotion.uiPanel = itemUI;
healthPotion.id = "health_potion";
healthPotion.amount = 1;
healthPotion.infoText = "A healing potion that restores 50 health points.";
healthPotion.collectable = true;
healthPotion.pickSound = potionPickupSound;
healthPotion.dropSound = potionDropSound;

// Listen for interaction events
chest.OnOpenCloseEvent += (interactable, isOpen) => {
    if (isOpen) {
        // Chest has been opened
        PlayChestOpenAnimation();
    } else {
        // Interaction with chest has ended
        PlayChestCloseAnimation();
    }
};
```

## Implementation Details
- Interactables typically work in conjunction with an `InteractableManager` that detects when the player is near
- The visibility state is synchronized in networked games
- UI panels can be customized for each interactable type
- When collected, the actual object is hidden but not destroyed, allowing it to be dropped later
- Interaction can switch to a special camera view for examining objects in detail

## Use Cases
- Collectible items like potions, weapons, keys
- Interactive objects like doors, levers, buttons
- Information sources like books, notes, terminals
- Puzzles and mechanical contraptions
- Inventory and equipment management
- Loot and treasure systems

## Notes
- For proper interaction, the object should have an appropriate collision trigger
- The `#` before method names like `#Pick` likely indicates protected or special access methods
- Interaction UI should be designed to match the interaction type
- Consider implementing custom `OnCommandEvent` handlers for complex interactable behavior

## Related Components
- Works closely with `InteractableManager.cs` for player interaction
- Can integrate with `InventoryManager.cs` for item collection
- Uses `NetworkObject.cs` for multiplayer synchronization
- Uses `UIPanel.cs` for interaction interface

## Dependencies
- Uses `Universe.Core` and `Universe.Network` namespaces
- Uses `UniObjectUtil` for object manipulation
- Uses `AudioUtil` for sound effects
