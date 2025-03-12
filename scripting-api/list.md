---
layout: default
title: List
nav_order: 26
parent: Scripting API
---
# List

## Description
The `List` class provides a dynamic array implementation for the Universe framework. It allows storing and manipulating collections of objects with a variety of common operations like adding, inserting, removing, and accessing elements.

## Namespace
`Universe.Core`

## Properties

| Property | Type | Description                      |
|----------|------|----------------------------------|
| lst      | list | The internal list data structure |

## Methods

### List
```csharp
void List(list initList)
```
Constructor that initializes the list with an existing list.

#### Parameters
- `initList`: An existing list to initialize with

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Creates a new empty list.

### Add
```csharp
void Add(object item)
```
Adds an item to the end of the list.

#### Parameters
- `item`: The item to add

### Insert
```csharp
void Insert(int index, object item)
```
Inserts an item at the specified index.

#### Parameters
- `index`: The position to insert the item
- `item`: The item to insert

### Remove
```csharp
bool Remove(object item)
```
Removes the first occurrence of an item from the list.

#### Parameters
- `item`: The item to remove

#### Returns
- `true` if the item was found and removed, `false` otherwise

### RemoveAt
```csharp
void RemoveAt(int index)
```
Removes the item at the specified index.

#### Parameters
- `index`: The index of the item to remove

### Contains
```csharp
bool Contains(object item)
```
Checks if the list contains the specified item.

#### Parameters
- `item`: The item to check for

#### Returns
- `true` if the item exists in the list, `false` otherwise

### Clear
```csharp
void Clear()
```
Removes all items from the list.

### Get
```csharp
object Get(int index)
```
Gets the item at the specified index.

#### Parameters
- `index`: The index of the item to retrieve

#### Returns
- The item at the specified index, or null if the index is out of range

### Set
```csharp
object Set(int index, object item)
```
Sets the item at the specified index.

#### Parameters
- `index`: The index of the item to set
- `item`: The new value for the item

#### Returns
- The previous item at the specified index

### IndexOf
```csharp
int IndexOf(object item)
```
Gets the index of the first occurrence of an item.

#### Parameters
- `item`: The item to find

#### Returns
- The index of the item, or -1 if not found

### Count
```csharp
int Count()
```
Gets the number of items in the list.

#### Returns
- The number of items

### Init
```csharp
void Init(list newList)
```
Initializes the list with a new list.

#### Parameters
- `newList`: The new list to initialize with

### First
```csharp
object First()
```
Gets the first item in the list.

#### Returns
- The first item, or null if the list is empty

### Last
```csharp
object Last()
```
Gets the last item in the list.

#### Returns
- The last item, or null if the list is empty

## Example Usage
```csharp
// Create a list of inventory items
List inventory = new List();
inventory.Add("Health Potion");
inventory.Add("Magic Scroll");
inventory.Add("Sword");

// Check if an item exists
if (inventory.Contains("Health Potion")) {
    // Use the health potion
    inventory.Remove("Health Potion");
}

// Process all items
for (int i = 0; i < inventory.Count(); i++) {
    string item = inventory.Get(i);
    Debug.Log("Item " + i + ": " + item);
}

// Create a quest task list
List questTasks = new List();
questTasks.Add("Speak to the village elder");
questTasks.Add("Find the lost artifact");
questTasks.Add("Defeat the dragon");

// Track completion and update UI
void CompleteTask(int taskIndex) {
    string task = questTasks.Get(taskIndex);
    questTasks.RemoveAt(taskIndex);
    completedTasks.Add(task);
    UpdateQuestUI();
}
```

## Implementation Details
- The `List` class is a wrapper around the native `list` type
- The class provides standard list operations with an object-oriented interface
- Most operations delegate to the `ListUtil` utility class for the actual implementation
- The `First()` and `Last()` methods provide convenient access to the first and last elements

## Notes
- Lists can store any object type, including mixed types in the same list
- Index operations start at 0, as is standard
- For more complex collection needs, consider using `Dictionary` for key-value pairs
- Error handling for out-of-range indices is managed internally; most methods return null for invalid indices
- The list is not fixed-size and will grow dynamically as needed

## Related Components
- Often used with `Dictionary.cs` for more complex data structures
- Used throughout the framework for storing collections of objects

## Dependencies
- Uses `ListUtil` for the actual list operations
