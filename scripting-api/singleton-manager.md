---
layout: default
title: SingletonManager
nav_order: 42
parent: Scripting API
---
# SingletonManager

## Description
The `SingletonManager` class implements a singleton pattern for game objects, ensuring that only one instance of a particular object type exists. It destroys any previous instances when a new one is created, making it useful for manager objects, controllers, and other components that should be unique in the game world.

## Namespace
`Universe.Helper`

## Properties
| Property    | Type   | Description                               |
|-------------|--------|-------------------------------------------|
| singletonId | string | Unique identifier for this singleton type |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Checks if an instance with the same singletonId already exists, destroys it if found, and registers this object as the new instance.

## Example Usage
```csharp
// Create a singleton game manager
SingletonManager gameManagerSingleton = new SingletonManager();
gameManagerSingleton.singletonId = "GameManager";

// Create a singleton audio controller
SingletonManager audioControllerSingleton = new SingletonManager();
audioControllerSingleton.singletonId = "AudioController";

// Create a singleton player data controller that persists between scenes
SingletonManager playerDataSingleton = new SingletonManager();
playerDataSingleton.singletonId = "PlayerData";

// Get a reference to a singleton from another script
UniObject GetAudioController() {
    return StorageUtil.GetTempData("AudioController", null);
}
```

## Technical Details
- The singleton pattern is implemented using `StorageUtil.GetTempData()` and `StorageUtil.SetTempData()`
- When initialized, the manager checks if an object with the same `singletonId` already exists
- If a previous instance exists, it is destroyed to maintain the singleton pattern
- The current object is then registered as the singleton instance for that ID
- Other scripts can access the singleton through `StorageUtil.GetTempData(singletonId, null)`

## Use Cases
- Game managers that coordinate game state
- Audio controllers that manage sound playback
- Input managers that process player input
- UI controllers that manage user interface elements
- Resource managers that handle asset loading
- Network managers for multiplayer games
- Persistent data controllers that maintain state between scenes

## Notes
- Each singleton type should have a unique `singletonId`
- Consider using descriptive IDs like "GameManager", "AudioController", etc.
- Singletons can create tight coupling between systems, so use judiciously
- This implementation does not prevent creation of multiple singletons, but ensures only one exists at a time
- For true enforcement of the singleton pattern, additional code would be needed
- Singletons stored with this method will not persist between game sessions

## Related Components
- Often used with manager and controller scripts that need to be globally accessible

## Dependencies
- Uses `StorageUtil` for temporary data storage
- Uses `UniObjectUtil.GetUniObject()` to get a reference to the object
- Uses `UniObjectUtil.Destroy()` to remove old instances
