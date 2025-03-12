---
layout: default
title: Scoreboard
nav_order: 38
parent: Scripting API
---
# Scoreboard

## Description
The `Scoreboard` class provides functionality for managing and storing high scores, leaderboards, and player statistics. It interfaces with a persistent storage system to save scores across game sessions and potentially share them between players.

## Namespace
`Universe.Tools`

## Properties

| Property      | Type   | Description                                                                        |
|---------------|--------|------------------------------------------------------------------------------------|
| boardId       | string | Unique identifier for the scoreboard (default: "HighScores")                       |
| maxItems      | int    | Maximum number of entries to keep in the scoreboard (default: 100)                 |
| allowMultiple | bool   | Whether a player can have multiple entries on the same scoreboard (default: false) |
| scores        | List   | List of current scoreboard entries                                                 |

## Events

| Event                | Parameters                            | Description                                           |
|----------------------|---------------------------------------|-------------------------------------------------------|
| OnAddScoreComplete   | (bool isOk, int index, string userId) | Triggered when a score addition operation completes   |
| OnGetScoreComplete   | (bool isOk, List data)                | Triggered when a score retrieval operation completes  |
| OnClearScoreComplete | (bool isOk)                           | Triggered when a scoreboard clear operation completes |

## Methods

### OnInit
```csharp
void OnInit()
```
Initializes the scoreboard with an empty list.

### AddScore
```csharp
void AddScore(string userId, string userName, float score, dictionary customData)
```
Adds a score entry to the scoreboard.

#### Parameters
- `userId`: Unique identifier for the player
- `userName`: Display name for the player
- `score`: Numerical score value
- `customData`: Additional custom data to store with the score entry

### AddHandler
```csharp
void AddHandler(bool isOk, int index, string userId)
```
Callback handler for when a score addition operation completes.

#### Parameters
- `isOk`: Whether the operation succeeded
- `index`: Index of the added entry in the scoreboard
- `userId`: ID of the user whose score was added

### GetScores
```csharp
void GetScores(string userId)
```
Retrieves scoreboard entries, optionally filtered by user ID.

#### Parameters
- `userId`: User ID to filter by, or null for all entries

### GetHandler
```csharp
void GetHandler(bool isOk, list data)
```
Callback handler for when a score retrieval operation completes.

#### Parameters
- `isOk`: Whether the operation succeeded
- `data`: The retrieved scoreboard data

### ClearScores
```csharp
void ClearScores()
```
Clears all entries from the scoreboard.

### ClearHandler
```csharp
void ClearHandler(bool isOk)
```
Callback handler for when a scoreboard clear operation completes.

#### Parameters
- `isOk`: Whether the operation succeeded

## Example Usage
```csharp
// Create a level completion time scoreboard
Scoreboard levelTimeScoreboard = new Scoreboard();
levelTimeScoreboard.boardId = "Level1Times";
levelTimeScoreboard.maxItems = 10; // Only keep top 10 times
levelTimeScoreboard.allowMultiple = false; // Each player's best time only

// Listen for events
levelTimeScoreboard.OnAddScoreComplete += (isOk, index, userId) => {
    if (isOk) {
        if (index <= 3) {
            UI.ShowMessage("New top 3 time!");
        } else {
            UI.ShowMessage("Score added!");
        }
    }
};

levelTimeScoreboard.OnGetScoreComplete += (isOk, data) => {
    if (isOk) {
        DisplayScoreboardUI(data);
    }
};

// Add a player's level completion time
void SubmitLevelTime(float completionTime) {
    string userId = GetCurrentUserId();
    string userName = GetCurrentUserName();
    dictionary additionalData = DictionaryUtil.New();
    DictionaryUtil.Add(additionalData, "deaths", playerDeathCount);
    DictionaryUtil.Add(additionalData, "secrets", secretsFound);
    
    levelTimeScoreboard.AddScore(userId, userName, completionTime, additionalData);
}

// Display the leaderboard
void ShowLeaderboard() {
    levelTimeScoreboard.GetScores(null); // Get all scores
    // The OnGetScoreComplete event will be triggered when data is ready
}

// Create a global high score board
Scoreboard globalHighScores = new Scoreboard();
globalHighScores.boardId = "GlobalHighScores";
globalHighScores.maxItems = 100;
globalHighScores.allowMultiple = false;

// Add a score to the global leaderboard
globalHighScores.AddScore(userId, userName, playerScore, null);
```

## Technical Details
- The scoreboard system uses `StorageUtil` to persist data across sessions
- Score entries are stored with the player's ID, name, score value, and optional custom data
- Entries can be ordered by score (typically highest first)
- When `allowMultiple` is false, only the best score for each player is kept
- The `maxItems` property limits the total number of entries to prevent unbounded growth
- Operations are asynchronous with completion callbacks through events

## Use Cases
- High score leaderboards for levels or game modes
- Time trial rankings
- Player statistics tracking
- Competitive gameplay features
- Achievement progress tracking
- Speedrun leaderboards
- Player progression metrics

## Notes
- Scoreboards are identified by their `boardId`, so use unique identifiers for different purposes
- Consider appropriate values for `maxItems` based on the expected number of players
- Custom data can store additional metrics like accuracy, time played, or level-specific stats
- The actual persistence mechanism is abstracted by `StorageUtil`, which may use local storage or online services
- If network connectivity is required for scoreboard functions, handle possible failures gracefully

## Related Components
- Works with UI components to display leaderboards
- Integrates with user authentication systems for player identification

## Dependencies
- Uses `Universe.Core` namespace
- Uses `List` class for storing score entries
- Uses `StorageUtil` for data persistence operations
