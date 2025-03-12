---
layout: default
title: InventoryManager
nav_order: 23
parent: Scripting API
---
# InventoryManager

## Description
The `InventoryManager` class provides a simple inventory system for tracking and managing collected items. It maintains a dictionary of items with their quantities and provides methods for adding and removing items.

## Namespace
`Universe.Tools`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| inventory | Dictionary | Dictionary storing item IDs and their quantities |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the inventory system with an empty dictionary.

### Pick
```csharp
void Pick(string key, int amount)
```
Adds a specified amount of an item to the inventory.

#### Parameters
- `key`: The identifier of the item to add
- `amount`: The quantity to add (default: 1)

### Drop
```csharp
void Drop(string key, int amount, bool allowNegative)
```
Removes a specified amount of an item from the inventory.

#### Parameters
- `key`: The identifier of the item to remove
- `amount`: The quantity to remove
- `allowNegative`: Whether the quantity can go below zero

## Example Usage
```csharp
// Create a player inventory
InventoryManager playerInventory = new InventoryManager();

// Add items to inventory
playerInventory.Pick("gold_coin", 50);
playerInventory.Pick("health_potion", 3);
playerInventory.Pick("iron_sword", 1);

// Use a potion (remove from inventory)
playerInventory.Drop("health_potion", 1, false);

// Check if player has enough coins and spend them
Dictionary inventoryDict = playerInventory.inventory.dict;
int goldCoins = DictionaryUtil.Get(inventoryDict, "gold_coin");
if (goldCoins >= 20) {
    playerInventory.Drop("gold_coin", 20, false);
    // Give player purchased item
    playerInventory.Pick("magic_scroll", 1);
}
```

## Implementation Details
- The inventory is implemented as a Dictionary with item IDs as keys and quantities as values
- If an item doesn't exist in the inventory when picked up, it's added with the specified amount
- When dropping items, the quantity is reduced, but won't go below zero unless `allowNegative` is true
- Item quantities of zero are still kept in the dictionary

## Use Cases
- Player inventory management
- Resource tracking and spending
- Quest item collection
- Crafting systems (tracking materials)
- Shop and trading systems

## Notes
- This is a basic inventory system focused on item quantities
- For more complex inventory needs, consider extending with:
  - Item metadata (descriptions, stats, etc.)
  - Item stacking rules
  - Weight or slot limitations
  - Categories or organization
  - Equipped item tracking
- For UI representation of the inventory, a separate component would be needed

## Related Components
- Works with `InteractableManager.cs` for item collection
- Can be used with `Interactable.cs` items

## Dependencies
- Uses `Universe.Core` namespace
- Uses `Dictionary` class for item storage
