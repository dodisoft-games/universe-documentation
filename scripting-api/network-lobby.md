---
layout: default
title: NetworkLobby
nav_order: 31
parent: Scripting API
---
# NetworkLobby

## Description
The `NetworkLobby` class manages pre-game lobbies in multiplayer games, handling player joining/leaving, countdown timers, and game starting. It provides a framework for creating waiting areas where players gather before matches begin.

## Namespace
`Universe.Network`

## Properties

| Property   | Type   | Description                                                             |
|------------|--------|-------------------------------------------------------------------------|
| id         | int    | Unique identifier for this lobby (default: 1)                           |
| mode       | string | Game mode identifier (default: "Default")                               |
| minPlayers | int    | Minimum number of players required to start a game (default: 2)         |
| maxPlayers | int    | Maximum number of players allowed in the lobby (default: 4)             |
| waitDelay  | int    | Seconds to wait after minimum player count is reached (default: 10)     |
| autoStart  | bool   | Whether to automatically start the game after countdown (default: true) |
| playerTag  | string | Tag used to identify player objects (default: "player")                 |
| players    | list   | List of players currently in the lobby                                  |
| countDown  | int    | Current countdown timer value                                           |
| starting   | bool   | Whether the game is currently starting                                  |

## Events

| Event              | Parameters                                        | Description                                 |
|--------------------|---------------------------------------------------|---------------------------------------------|
| OnPlayerEvent      | (NetworkLobby lobby, string name, bool connected) | Triggered when a player joins or leaves     |
| OnCounterTickEvent | (NetworkLobby lobby, int counter)                 | Triggered every second during the countdown |
| OnStartingEvent    | (NetworkLobby lobby, string roomId)               | Triggered when the game is about to start   |
| OnPlayerListEvent  | (NetworkLobby lobby)                              | Triggered when the player list is updated   |

## Methods

### OnTriggerEnter
```csharp
void OnTriggerEnter(UniObject other)
```
Called when an object enters the lobby trigger area. If it's a player, adds them to the lobby.

#### Parameters
- `other`: The object entering the trigger

### OnTriggerExit
```csharp
void OnTriggerExit(UniObject other)
```
Called when an object exits the lobby trigger area. If it's a player, removes them from the lobby.

#### Parameters
- `other`: The object exiting the trigger

### OnInit
```csharp
void OnInit()
```
Initializes the lobby and registers it with the network system.

### Tick
```csharp
void Tick()
```
Updates the countdown timer and starts the game when ready. Called every second.

### GetNetworkObject
```csharp
NetworkObject GetNetworkObject(UniObject source)
```
Gets the NetworkObject component from an object.

#### Parameters
- `source`: The object to get the NetworkObject from

#### Returns
- The NetworkObject component, or null if none exists

### IsMaster
```csharp
bool IsMaster()
```
Checks if the local player is the master client (lobby owner).

#### Returns
- `true` if the local player is the master client, `false` otherwise

### Join
```csharp
bool Join()
```
Joins the lobby.

#### Returns
- `true` if successful, `false` otherwise

### Leave
```csharp
bool Leave()
```
Leaves the lobby.

#### Returns
- `true` if successful, `false` otherwise

### StartGame
```csharp
void StartGame()
```
Starts the game with the current players.

### UpdateCallback
```csharp
void UpdateCallback(list playerList, string playerName, int state, int counter)
```
Called by the network system when lobby state changes. Updates the player list and triggers events.

#### Parameters
- `playerList`: Updated list of players
- `playerName`: Name of the player that changed (if applicable)
- `state`: Change state (-1: player left, 0: list update, 1: player joined)
- `counter`: Current countdown value

### StartCallback
```csharp
void StartCallback(string roomId)
```
Called by the network system when the game is starting. Triggers the start event.

#### Parameters
- `roomId`: ID of the game room being created

### StartLate
```csharp
void StartLate(string roomId)
```
Triggers the starting event after a short delay.

#### Parameters
- `roomId`: ID of the game room being created

### Reset
```csharp
void Reset()
```
Resets the lobby state, clearing players and countdown.

### DestroyPlayerObjects
```csharp
void DestroyPlayerObjects()
```
Destroys all network player objects associated with this lobby.

### AskInfo
```csharp
void AskInfo()
```
Requests updated lobby information from the server.

## Example Usage
```csharp
// Create a team deathmatch lobby
NetworkLobby teamDeathmatchLobby = new NetworkLobby();
teamDeathmatchLobby.id = 1;
teamDeathmatchLobby.mode = "TeamDeathmatch";
teamDeathmatchLobby.minPlayers = 4; // 2v2 minimum
teamDeathmatchLobby.maxPlayers = 10; // 5v5 maximum
teamDeathmatchLobby.waitDelay = 15; // 15 second countdown
teamDeathmatchLobby.autoStart = true;

// Add event listeners
teamDeathmatchLobby.OnPlayerEvent += (lobby, name, connected) => {
    if (connected) {
        UI.ShowMessage(name + " joined the lobby");
    } else {
        UI.ShowMessage(name + " left the lobby");
    }
    UpdatePlayerList(lobby.players);
};

teamDeathmatchLobby.OnCounterTickEvent += (lobby, counter) => {
    UI.UpdateCountdown(counter);
    if (counter <= 5 && counter > 0) {
        // Play countdown sound
        AudioSystem.PlaySound("countdown_beep");
    }
};

teamDeathmatchLobby.OnStartingEvent += (lobby, roomId) => {
    UI.ShowMessage("Game starting!");
    // Transition to game scene
    SceneManager.LoadGameScene(lobby.mode, roomId);
};

// Create a racing game lobby with manual start
NetworkLobby racingLobby = new NetworkLobby();
racingLobby.id = 2;
racingLobby.mode = "Racing";
racingLobby.minPlayers = 2;
racingLobby.maxPlayers = 8;
racingLobby.autoStart = false; // Manual start by host

// Add a UI button for the host to start the game
startRaceButton.onClick = () => {
    if (racingLobby.IsMaster()) {
        racingLobby.StartGame();
    }
};
```

## Technical Details
- The lobby functions as both a network coordinator and a physical area in the game world
- Player detection uses trigger colliders with the specified `playerTag`
- The countdown begins automatically when player count reaches `minPlayers`
- The lobby uses a tick system that updates every second to manage countdown and events
- Network communication is handled through the `NetworkUtil` system
- Only the master client (first player to join) can start the game manually

## Use Cases
- Waiting rooms before matches start
- Game mode selection and team assignment
- Character selection and customization areas
- Pre-game strategy and loadout selection
- Tutorial or rules explanation areas
- Voting systems for maps or game options

## Notes
- The lobby should be placed in a designated waiting area in the game world
- For UI-only lobbies, the trigger functionality can be ignored
- Consider implementing custom player list UI to show all players in the lobby
- The countdown can be used to display a timer in the UI
- Special care should be taken to handle network disconnects gracefully
- For more advanced lobbies, extend this class with additional functionality

## Related Components
- Works with `NetworkGame.cs` for overall network management
- Works with `NetworkObject.cs` for player object synchronization

## Dependencies
- Uses `NetworkUtil` for network operations
- Uses `Utility.CallMethodDelayed()` for timing functions
