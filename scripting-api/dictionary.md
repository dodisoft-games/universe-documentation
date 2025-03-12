---
layout: default
title: Dictionary
nav_order: 13
parent: Scripting API
---
# Dictionary

## Description
The `Dictionary` class provides a key-value collection implementation for the Universe framework. It allows storing and retrieving objects by key with a range of common operations like adding, removing, and querying the collection.

## Namespace
`Universe.Core`

## Properties
| Property | Type       | Description                            |
|----------|------------|----------------------------------------|
| dict     | dictionary | The internal dictionary data structure |

## Methods

### Dictionary
```csharp
void Dictionary(dictionary initDictionary)
```
Constructor that initializes the dictionary with an existing dictionary.

#### Parameters
- `initDictionary`: An existing dictionary to initialize with

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Creates a new empty dictionary.

### Add
```csharp
void Add(object key, object value)
```
Adds a key-value pair to the dictionary.

#### Parameters
- `key`: The key for the value
- `value`: The value to store

### Remove
```csharp
bool Remove(object key)
```
Removes a key-value pair from the dictionary.

#### Parameters
- `key`: The key to remove

#### Returns
- `true` if the key was found and removed, `false` otherwise

### ContainsKey
```csharp
bool ContainsKey(object key)
```
Checks if the dictionary contains the specified key.

#### Parameters
- `key`: The key to check

#### Returns
- `true` if the key exists, `false` otherwise

### ContainsValue
```csharp
bool ContainsValue(object value)
```
Checks if the dictionary contains the specified value.

#### Parameters
- `value`: The value to check

#### Returns
- `true` if the value exists, `false` otherwise

### Clear
```csharp
void Clear()
```
Removes all key-value pairs from the dictionary.

### Get
```csharp
object Get(object key)
```
Gets the value associated with the specified key.

#### Parameters
- `key`: The key to look up

#### Returns
- The value associated with the key, or null if the key doesn't exist

### Set
```csharp
void Set(object key, object value)
```
Sets the value associated with the specified key.

#### Parameters
- `key`: The key to set
- `value`: The value to associate with the key

### Keys
```csharp
list Keys()
```
Gets a list of all keys in the dictionary.

#### Returns
- A list containing all the keys

### Count
```csharp
int Count()
```
Gets the number of key-value pairs in the dictionary.

#### Returns
- The number of key-value pairs

### GetByIndex
```csharp
object GetByIndex(int index)
```
Gets a value from the dictionary by its index.

#### Parameters
- `index`: The index of the key-value pair

#### Returns
- The value at the specified index, or null if the index is out of range

### Init
```csharp
void Init(dictionary newDictionary)
```
Initializes the dictionary with a new dictionary.

#### Parameters
- `newDictionary`: The new dictionary to initialize with

## Example Usage
```csharp
// Create a dictionary to store player stats
Dictionary playerStats = new Dictionary();
playerStats.Add("health", 100);
playerStats.Add("mana", 50);
playerStats.Add("strength", 15);
playerStats.Add("level", 1);

// Retrieve a value
int health = playerStats.Get("health");

// Check if a key exists
if (playerStats.ContainsKey("armor")) {
    // Use armor value
} else {
    // Set default armor
    playerStats.Set("armor", 10);
}

// Iterate through all keys
list keys = playerStats.Keys();
for (int i = 0; i < keys.Count(); i++) {
    string key = keys.Get(i);
    object value = playerStats.Get(key);
    Debug.Log(key + ": " + value);
}

// Create an inventory using dictionary
Dictionary inventory = new Dictionary();
inventory.Add("gold", 100);
inventory.Add("health_potion", 5);
inventory.Add("magic_scroll", 2);

// Update inventory count
int potionCount = inventory.Get("health_potion");
inventory.Set("health_potion", potionCount - 1);
```

## Notes
- The `Dictionary` class is a wrapper around the native `dictionary` type
- Keys should be unique; adding a key that already exists will overwrite the previous value
- The `GetByIndex` method allows treating the dictionary like a list, but the order is not guaranteed
- The class supports any object type for both keys and values

## Dependencies
- Uses `DictionaryUtil` for the actual dictionary operations
- Uses `ListUtil` for handling key lists and related operations
