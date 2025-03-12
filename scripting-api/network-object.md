---
layout: default
title: NetworkObject
nav_order: 32
parent: Scripting API
---
# NetworkObject

## Description
The `NetworkObject` class enables network synchronization for game objects in multiplayer games. It handles the replication of object position, rotation, scale, animation, and script properties across all clients, ensuring that all players see a consistent game state.

## Namespace
`Universe.Network`

## Properties

| Property      | Type      | Description                                                                                      |
|---------------|-----------|--------------------------------------------------------------------------------------------------|
| targetObject  | UniObject | The object to synchronize (defaults to the object this script is attached to)                    |
| isSceneObject | bool      | Whether this is a persistent scene object rather than a dynamically spawned one (default: false) |
| syncPosition  | bool      | Whether to synchronize position (default: true)                                                  |
| syncRotation  | bool      | Whether to synchronize rotation (default: true)                                                  |
| syncScale     | bool      | Whether to synchronize scale (default: true)                                                     |
| syncAnimation | bool      | Whether to synchronize animation state (default: true)                                           |
| syncPhysics   | bool      | Whether to synchronize physics properties like velocity (default: false)                         |
| syncScripts   | bool      | Whether to synchronize script properties (default: true)                                         |
| viewID        | int       | Unique identifier for this network object (0 for auto-assignment) (default: 0)                   |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the network object and registers it with the network system.

### IsMaster
```csharp
bool IsMaster()
```
Checks if the local player is the master client (room owner).

#### Returns
- `true` if the local player is the master client, `false` otherwise

### IsMine
```csharp
bool IsMine()
```
Checks if the local player owns this network object.

#### Returns
- `true` if the object is owned by the local player, `false` otherwise

### Destroy
```csharp
void Destroy()
```
Destroys the network object across all clients if it's owned by the local player and not a scene object.

### AddSyncScript
```csharp
void AddSyncScript(uniscript script)
```
Adds a script to be synchronized across the network.

#### Parameters
- `script`: The script to synchronize

### RemoveSyncScript
```csharp
void RemoveSyncScript(uniscript script)
```
Removes a script from network synchronization.

#### Parameters
- `script`: The script to stop synchronizing

## Example Usage
```csharp
// Create a player character with network synchronization
NetworkObject playerNetworkObject = new NetworkObject();
playerNetworkObject.targetObject = playerCharacter;
playerNetworkObject.syncPosition = true;
playerNetworkObject.syncRotation = true;
playerNetworkObject.syncAnimation = true;
playerNetworkObject.syncPhysics = false; // Use character controller instead
playerNetworkObject.syncScripts = true;

// Create a simple synchronized pickup item
NetworkObject pickupNetworkObject = new NetworkObject();
pickupNetworkObject.syncPosition = true;
pickupNetworkObject.syncRotation = true;
pickupNetworkObject.syncScale = false; // Scale doesn't change
pickupNetworkObject.syncAnimation = false; // No animations
pickupNetworkObject.syncPhysics = false; // No physics needed
pickupNetworkObject.syncScripts = true; // For pickup state

// Add a script to be synchronized
Interactable pickupInteractable = new Interactable();
pickupNetworkObject.AddSyncScript(pickupInteractable);

// Create a persistent scene object
NetworkObject doorNetworkObject = new NetworkObject();
doorNetworkObject.isSceneObject = true; // Part of the scene, not spawned
doorNetworkObject.syncPosition = false; // Only rotates, doesn't move
doorNetworkObject.syncRotation = true; // Door opening/closing
doorNetworkObject.syncAnimation = false;
doorNetworkObject.syncPhysics = false;
doorNetworkObject.syncScripts = true; // For door state
```

## Technical Details
- The network object system uses view IDs to identify objects across the network
- Objects can be owned by a specific player or shared (like scene objects)
- Only the owner of an object can directly modify its synchronized properties
- Scene objects persist throughout the game session and are not destroyed on owner disconnect
- Dynamic objects are created at runtime and typically belong to a specific player
- Synchronization is selective to minimize network traffic; only enable what's needed
- Script synchronization allows custom properties to be replicated across the network

## Use Cases
- Player characters and vehicles
- Projectiles and weapons
- Interactive objects like doors, buttons, levers
- Collectible items and powerups
- Movable objects and physics props
- NPCs and enemies in cooperative games
- Shared world objects that can change state

## Notes
- For optimal network performance, only synchronize what's necessary
- Physics synchronization can be bandwidth-intensive; use carefully
- Animation synchronization works best with simple animation states
- For complex custom synchronization, implement custom serialization in scripts
- Scene objects should typically be marked with `isSceneObject = true`
- Use different synchronization strategies based on game type (e.g., action games need more frequent position updates)
- Ownership determines which client can directly modify an object

## Related Components
- Works with `NetworkGame.cs` for overall network management
- Works with `ScriptSynchronizer.cs` for easier script synchronization
- Can be used with `Interactable.cs` for networked interactive objects

## Dependencies
- Uses `NetworkUtil` for network operations
- Uses `UniObjectUtil` to access the target object if not specified
