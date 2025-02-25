---
layout: default
title: UIPanel
nav_order: 3
parent: Scripting API
---
# UIPanel

## Overview

The UIPanel class manages UI panels, handling their visibility, interaction, and animations.

## Properties

| string name | The name of the panel. |
| bool openOnLoad | Determines whether the panel opens when the game starts. |
| int panelId | Stores the panel ID (default: -1). |
| bool open | Tracks whether the panel is currently open. |

## Methods

| void OnStart() | Opens the panel if openOnLoad is true. |
| void OnDestroy() | Ensures the panel is closed upon destruction. |
| void Open(bool closeOthers) | Opens the panel, optionally closing others. |
| void Close() | Closes the panel. |
| void Show() | Makes the panel visible. |
| void Hide() | Hides the panel. |
| void SetVisibility(bool state) | Sets the panel's visibility. |
| void PlayAnimation(string animation) | Plays a specified animation on the panel. |
| void ShowItem(string itemName) | Shows a UI element. |
| void HideItem(string itemName) | Hides a UI element. |
| void SetItemVisibility(string itemName, bool state) | Sets the visibility of a UI element. |
| void SetItemActivition(string itemName, bool state) | Enables or disables interaction for a UI element. |
| void SetItemValue(string itemName, object value) | Sets a UI element's value. |
| object GetItemValue(string itemName) | Retrieves a UI element's value. |
| void PlayItemAnimation(string itemName, string animation) | Plays an animation on a UI element. |
| void SetItemIcon(string itemName, int iconId) | Sets the icon for a UI element. |
| void SetItemColor(string itemName, float r, float g, float b, float a) | Sets the color of a UI element. |
| void SetItemPosition(string itemName, vector3 position, UIPositionType positionType) | Sets the position of a UI element. |
| void SetPanelPosition(vector3 position, UIPositionType positionType) | Sets the position of the panel. |
| vector3 GetItemPosition(string itemName, UIPositionType positionType) | Retrieves an item's position. |
| vector3 GetPanelPosition(UIPositionType positionType) | Retrieves the panel's position. |
| void SetPanelScale(float scale) | Sets the scale of the panel. |
| void AddScoreboardItem(string itemName, string value) | Adds an item to the scoreboard. |
| void InitScoreboard(string itemName) | Initializes a scoreboard entry. |
| void ClearScoreboard(string itemName) | Clears a scoreboard entry. |
| void CLoseAllPanels() | Closes all panels in the UI system. |