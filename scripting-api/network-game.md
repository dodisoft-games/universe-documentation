---
layout: default
title: NetworkGame
nav_order: 30
parent: Scripting API
---
# NetworkGame

## Description
The `NetworkGame` class is the core component for implementing multiplayer functionality in games built with the Universe framework. It manages network connections, room joining, player synchronization, and event handling for networked games.

## Namespace
`Universe.Network`

## Enums

### NetworkState
Defines the current state of the network connection.

| Value | Description |
|-------|-------------|
| Disconnected | Not connected to any network service |
| Connecting | Attempting to connect to the network service |
| Connected | Connected to the network service but not in a lobby |
| JoiningLobby | Attempting to join a lobby |
| JoinedLobby | Connected to a lobby but not in a room |
| JoiningRoom | Attempting to join a room |
| JoinedRoom | Connected to a room but not ready to play |
| ReadyToPlay | Connected and ready for gameplay |

## Properties

| Property          | Type         | Description                                                |
|-------------------|--------------|------------------------------------------------------------|
| autoConnect       | bool         | Whether to automatically connect on start (default: true)  |
| maxPlayerPerLobby | int          | Maximum number of players allowed in a lobby (default: 20) |
| state             | NetworkState | Current state of the network connection                    |
| playerId          | int          | The local player's unique identifier                       |
| playerName        | string       | The local player's name                                    |

## Events

| Event                 | Parameters           | Description                                   |
|-----------------------|----------------------|-----------------------------------------------|
| OnStateChangedEvent   | (NetworkState state) | Triggered when the network state changes      |
| ConnectedToLobbyEvent | ()                   | Triggered when connected to a lobby           |
| DisconnectedEvent     | ()                   | Triggered when disconnected from the network  |
| ConnectedToRoomEvent  | (string name)        | Triggered when connected to a room            |
| LeftRoomEvent         | ()                   | Triggered when leaving a room                 |
| PlayerEnterEvent      | (int playerId)       | Triggered when another player enters the room |
| PlayerExitEvent       | (int playerId)       | Triggered when another player leaves the room |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the network component and registers it with the network system.

### OnDestroy
```csharp
void OnDestroy()
```
Called when the script is destroyed. Disconnects from the network.

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Automatically connects if `autoConnect` is true.

### ChangeState
```csharp
void ChangeState(NetworkState newState)
```
Changes the current network state and triggers the state change event.

#### Parameters
- `newState`: The new network state

### Connect
```csharp
void Connect()
```
Initiates a connection to the network service.

### Disconnect
```csharp
void Disconnect()
```
Disconnects from the network service.

### JoinRoom
```csharp
void JoinRoom(string name)
```
Joins a specific room by name.

#### Parameters
- `name`: Name of the room to join

### CreateOrJoinRoom
```csharp
void CreateOrJoinRoom(string name)
```
Creates a new room or joins an existing one with the specified name.

#### Parameters
- `name`: Name of the room to create or join

### JoinRandomRoom
```csharp
void JoinRandomRoom(string gameMode, string map)
```
Joins a random room matching the specified game mode and map.

#### Parameters
- `gameMode`: The game mode to match
- `map`: The map to match

### LeaveRoom
```csharp
void LeaveRoom()
```
Leaves the current room.

### LeaveLobby
```csharp
void LeaveLobby()
```
Leaves the current lobby.

### SetName
```csharp
void SetName(string name)
```
Sets the player's name.

#### Parameters
- `name`: The player's name

### UpdateIdAndName
```csharp
void UpdateIdAndName()
```
Updates the local player's ID and name from the network system.

### AmIMaster
```csharp
bool AmIMaster()
```
Checks if the local player is the master client (room owner).

#### Returns
- `true` if the local player is the master client, `false` otherwise

### GetRoomPlayers
```csharp
list GetRoomPlayers()
```
Gets a list of players in the current room.

#### Returns
- A list containing player information

### SetPlayerInfo
```csharp
void SetPlayerInfo(int id, string key, string value)
```
Sets a custom property for a specific player.

#### Parameters
- `id`: The player's ID
- `key`: The property key
- `value`: The property value

### GetPlayerInfo
```csharp
dictionary GetPlayerInfo(int id)
```
Gets all custom properties for a specific player.

#### Parameters
- `id`: The player's ID

#### Returns
- A dictionary containing the player's properties

## Network Event Handling Methods
The class also includes methods for handling network events:

- `OnConnected()` - Called when successfully connected to the network
- `OnDisconnected()` - Called when disconnected from the network
- `OnJoinedLobby()` - Called when joined a lobby
- `OnJoinedRoom()` - Called when joined a room
- `OnPlayerEnter()` - Called when another player enters the room
- `OnPlayerExit()` - Called when another player leaves the room
- `OnLeftLobby()` - Called when the local player leaves a lobby
- `OnLeftRoom()` - Called when the local player leaves a room
- `OnRoomClosed()` - Called when a room is closed
- `OnGameStarted()` - Called when the game starts

## Example Usage
```csharp
// Create and configure a network manager
NetworkGame networkManager = new NetworkGame();
networkManager.maxPlayerPerLobby = 10;
networkManager.autoConnect = true;

// Listen for network events
networkManager.OnStateChangedEvent += (state) => {
    UpdateUIForNetworkState(state);
};

networkManager.ConnectedToRoomEvent += (roomName) => {
    Debug.Log("Joined room: " + roomName);
    LoadMultiplayerLevel();
};

networkManager.PlayerEnterEvent += (playerId) => {
    Debug.Log("Player joined: " + playerId);
    SpawnPlayerCharacter(playerId);
};

networkManager.PlayerExitEvent += (playerId) => {
    Debug.Log("Player left: " + playerId);
    RemovePlayerCharacter(playerId);
};

// Manually connect to a specific room
void JoinGameRoom(string roomName) {
    if (networkManager.state == NetworkState.JoinedLobby) {
        networkManager.JoinRoom(roomName);
    } else if (networkManager.state == NetworkState.Connected) {
        // Need to join lobby first
        // Lobby joining is automatic in this implementation
    } else {
        Debug.Log("Not connected to network");
    }
}
```

## Technical Details
- The `NetworkGame` class serves as a high-level wrapper around the network implementation
- It manages the state machine for network connection states
- Only one `NetworkGame` instance should exist at a time; the class handles this by removing duplicate instances
- Players in a room can have custom properties set using `SetPlayerInfo`
- The master client (first player to join or next in line if the original leaves) has special privileges

## Use Cases
- Multiplayer games of all types
- Cooperative gameplay
- Competitive matches
- Shared virtual spaces
- Multiplayer game lobbies
- Turn-based online games

## Notes
- For proper multiplayer functionality, objects that need to be synchronized should use `NetworkObject`
- The actual network implementation is abstracted behind `NetworkUtil` calls
- Room properties, matchmaking, and custom game logic need to be implemented on top of this foundation
- Consider using `NetworkLobby` for more advanced lobby management
- Network performance depends on both the game design and the players' connection quality

## Related Components
- Works with `NetworkObject.cs` for object synchronization
- Works with `NetworkLobby.cs` for lobby management
- Works with `ScriptSynchronizer.cs` for script property synchronization

## Dependencies
- Uses `NetworkUtil` for network operations
- Uses `StorageUtil` for temporary data storage
- Uses `Debug.Log()` for logging
