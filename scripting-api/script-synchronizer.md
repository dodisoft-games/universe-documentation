---
layout: default
title: ScriptSynchronizer
nav_order: 39
parent: Scripting API
---
# ScriptSynchronizer

## Description
The `ScriptSynchronizer` class provides a simple way to synchronize script properties over the network in multiplayer games. It acts as a bridge between a script that needs network synchronization and the network object that handles the actual networking.

## Namespace
`Universe.Network`

## Properties
| Property      | Type          | Description                                                      |
|---------------|---------------|------------------------------------------------------------------|
| networkObject | NetworkObject | Reference to the NetworkObject component that handles networking |
| script        | uniscript     | Reference to the script that needs to be synchronized            |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the specified script with the network object for synchronization.

## Example Usage
```csharp
// Create a script synchronizer for a health component
ScriptSynchronizer healthSync = new ScriptSynchronizer();
healthSync.networkObject = playerNetworkObject;
healthSync.script = playerHealth;

// Create a script synchronizer for an interactive object
ScriptSynchronizer doorSync = new ScriptSynchronizer();
doorSync.networkObject = doorNetworkObject;
doorSync.script = doorController;

// Create a script synchronizer for an inventory component
ScriptSynchronizer inventorySync = new ScriptSynchronizer();
inventorySync.networkObject = characterNetworkObject;
inventorySync.script = playerInventory;
```

## Technical Details
- The synchronizer simply serves as a connection between a script and a network object
- It calls `networkObject.AddSyncScript(script)` during initialization
- The actual synchronization process is handled by the NetworkObject component
- Only properties and state changes in the script will be synchronized, not method calls
- The synchronization direction is typically from the owner of the network object to other clients

## Use Cases
- Synchronizing player health, ammo, or stats in multiplayer games
- Keeping interactive object states consistent across clients
- Sharing inventory or collectible states between players
- Synchronizing NPC behavior state
- Replicating environmental changes or destructible object states
- Ensuring UI elements show consistent information for all players

## Notes
- This component simplifies the process of adding scripts to network synchronization
- For scripts that need frequent updates, consider bandwidth implications
- Not all script properties need to be synchronized; custom serialization can be implemented
- Use this for scripts that wouldn't otherwise have direct access to the NetworkObject
- For fine-grained control over synchronization, use the NetworkObject directly
- Multiple scripts can be synchronized on a single NetworkObject

## Related Components
- Works with `NetworkObject.cs` for network synchronization
- Can be used with any script that needs network synchronization

## Dependencies
- Requires a valid `NetworkObject` component
- The script must be properly designed to support synchronization
