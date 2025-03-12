---
layout: default
title: UIPanel
nav_order: 48
parent: Scripting API
---
# UIPanel

## Description
The `UIPanel` class provides a comprehensive interface for managing UI panels in the game. It handles panel opening/closing, visibility, positioning, and element manipulation, allowing for dynamic UI control.

## Namespace
`Universe.Core`

## Enums

### UIPositionType
Defines how position coordinates are interpreted for UI elements.

| Value | Description |
|-------|-------------|
| World | Position in 3D world space coordinates |
| Screen | Position in 2D screen space coordinates (pixels) |
| Anchored | Position relative to the panel's anchor points |

## Properties

| Property   | Type   | Description                                              |
|------------|--------|----------------------------------------------------------|
| name       | string | Identifier for the UI panel                              |
| openOnLoad | bool   | Whether to automatically open the panel when initialized |
| panelId    | int    | Internal ID for the panel (default: -1)                  |
| open       | bool   | Whether the panel is currently open                      |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Opens the panel if `openOnLoad` is true.

### OnDestroy
```csharp
void OnDestroy()
```
Called when the script is destroyed. Closes the panel if it's open.

### CheckIfOpen
```csharp
void CheckIfOpen()
```
Ensures the panel is open, opening it if necessary.

### IsThisPanel
```csharp
bool IsThisPanel(string panelName)
```
Checks if this panel matches a specified name.

#### Parameters
- `panelName`: The name to check against

#### Returns
- `true` if the names match, `false` otherwise

### Open
```csharp
void Open(bool closeOthers)
```
Opens the UI panel.

#### Parameters
- `closeOthers`: Whether to close all other panels

### Close
```csharp
void Close()
```
Closes the UI panel.

### Show
```csharp
void Show()
```
Makes the panel visible without changing its open state.

### Hide
```csharp
void Hide()
```
Makes the panel invisible without changing its open state.

### SetVisibility
```csharp
void SetVisibility(bool state)
```
Sets the visibility of the panel.

#### Parameters
- `state`: Whether the panel should be visible

### PlayAnimation
```csharp
void PlayAnimation(string animation)
```
Plays an animation on the panel.

#### Parameters
- `animation`: Name of the animation to play

### ShowItem
```csharp
void ShowItem(string itemName)
```
Makes a specific UI element visible.

#### Parameters
- `itemName`: Name of the element to show

### HideItem
```csharp
void HideItem(string itemName)
```
Makes a specific UI element invisible.

#### Parameters
- `itemName`: Name of the element to hide

### SetItemVisibility
```csharp
void SetItemVisibility(string itemName, bool state)
```
Sets the visibility of a specific UI element.

#### Parameters
- `itemName`: Name of the element
- `state`: Whether the element should be visible

### SetItemActivition
```csharp
void SetItemActivition(string itemName, bool state)
```
Sets whether a UI element is interactive.

#### Parameters
- `itemName`: Name of the element
- `state`: Whether the element should be interactive

### SetItemValue
```csharp
void SetItemValue(string itemName, object value)
```
Sets the value of a UI element (text, number, etc.).

#### Parameters
- `itemName`: Name of the element
- `value`: Value to set

### GetItemValue
```csharp
object GetItemValue(string itemName)
```
Gets the value of a UI element.

#### Parameters
- `itemName`: Name of the element

#### Returns
- The element's current value

### PlayItemAnimation
```csharp
void PlayItemAnimation(string itemName, string animation)
```
Plays an animation on a specific UI element.

#### Parameters
- `itemName`: Name of the element
- `animation`: Name of the animation to play

### SetItemIcon
```csharp
void SetItemIcon(string itemName, int iconId)
```
Sets the icon for a UI element.

#### Parameters
- `itemName`: Name of the element
- `iconId`: ID of the icon to display

### SetItemColor
```csharp
void SetItemColor(string itemName, float r, float g, float b, float a)
```
Sets the color of a UI element.

#### Parameters
- `itemName`: Name of the element
- `r`, `g`, `b`, `a`: Color components (red, green, blue, alpha)

### SetItemPosition
```csharp
void SetItemPosition(string itemName, vector3 position, UIPositionType positionType)
```
Sets the position of a UI element.

#### Parameters
- `itemName`: Name of the element
- `position`: New position
- `positionType`: How to interpret the position coordinates

### SetPanelPosition
```csharp
void SetPanelPosition(vector3 position, UIPositionType positionType)
```
Sets the position of the entire panel.

#### Parameters
- `position`: New position
- `positionType`: How to interpret the position coordinates

### GetItemPosition
```csharp
vector3 GetItemPosition(string itemName, UIPositionType positionType)
```
Gets the position of a UI element.

#### Parameters
- `itemName`: Name of the element
- `positionType`: How to interpret the position coordinates

#### Returns
- The element's position

### GetPanelPosition
```csharp
vector3 GetPanelPosition(UIPositionType positionType)
```
Gets the position of the panel.

#### Parameters
- `positionType`: How to interpret the position coordinates

#### Returns
- The panel's position

### SetPanelScale
```csharp
void SetPanelScale(float scale)
```
Sets the scale of the entire panel.

#### Parameters
- `scale`: Scale factor

### AddScoreboardItem
```csharp
void AddScoreboardItem(string itemName, string value)
```
Adds an item to a scoreboard element.

#### Parameters
- `itemName`: Name of the scoreboard element
- `value`: Value to add

### InitScoreboard
```csharp
void InitScoreboard(string itemName)
```
Initializes a scoreboard element.

#### Parameters
- `itemName`: Name of the scoreboard element

### ClearScoreboard
```csharp
void ClearScoreboard(string itemName)
```
Clears all items from a scoreboard element.

#### Parameters
- `itemName`: Name of the scoreboard element

### CLoseAllPanels
```csharp
void CLoseAllPanels()
```
Closes all UI panels in the scene (static method).

## Example Usage
```csharp
// Create a main menu panel
UIPanel mainMenu = new UIPanel();
mainMenu.name = "MainMenu";
mainMenu.openOnLoad = true;

// Open/close panel methods
void ShowInventory() {
    inventoryPanel.Open(false); // Open without closing other panels
}

void CloseInventory() {
    inventoryPanel.Close();
}

// Manipulate UI elements
void UpdateHealthDisplay(int currentHealth, int maxHealth) {
    healthPanel.SetItemValue("HealthText", currentHealth + "/" + maxHealth);
    healthPanel.SetItemValue("HealthBar", (float)currentHealth / maxHealth);
}

// Show/hide UI elements based on game state
void ShowGameOverScreen(bool victory) {
    gameOverPanel.Open(true); // Close other panels
    
    if (victory) {
        gameOverPanel.ShowItem("VictoryMessage");
        gameOverPanel.HideItem("DefeatMessage");
        gameOverPanel.PlayAnimation("VictoryAnimation");
    } else {
        gameOverPanel.HideItem("VictoryMessage");
        gameOverPanel.ShowItem("DefeatMessage");
        gameOverPanel.PlayAnimation("DefeatAnimation");
    }
}

// Position UI elements
void PositionHealthBar(UniObject player) {
    vector3 screenPos = CameraUtil.WorldToScreen(player.GetWorldPosition() + [0, 2, 0]);
    healthPanel.SetPanelPosition(screenPos, UIPositionType.Screen);
}

// Update scoreboard
void AddHighScore(string playerName, int score) {
    highScorePanel.AddScoreboardItem("HighScoreList", playerName + ": " + score);
}
```

## Technical Details
- UI panels are identified by name and tracked with an internal ID
- The UI system is initialized when the first panel is opened
- Panel operations use the `UIUtil` utilities for actual implementation
- Elements within panels are referenced by name
- Multiple positioning modes allow for different UI layout approaches
- Scoreboard functionality provides simple list-based displays

## Use Cases
- Game menus (main menu, options, etc.)
- HUD elements (health bars, ammo counters, etc.)
- Inventory and character screens
- Dialog windows and quest information
- Shop interfaces
- Scoreboards and leaderboards
- Notification and alert displays
- Interactive tutorials

## Notes
- Panels should have unique names to avoid conflicts
- For complex UI layouts, consider using a design tool to create the panels
- Performance can be affected by having many panels open simultaneously
- For world-space UI, the World position type allows attaching UI to 3D objects
- Elements must exist in the UI definition before they can be manipulated
- The static method `CLoseAllPanels()` is useful for scene transitions

## Related Components
- Works with `Interactable.cs` for displaying interaction UI
- Can be used with `InputController.cs` for handling UI input

## Dependencies
- Uses `UIUtil` for all UI operations
