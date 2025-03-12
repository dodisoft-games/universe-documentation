---
layout: default
title: InputController
nav_order: 20
parent: Scripting API
---
# InputController

## Description
The `InputController` class provides an interface for handling user input from various sources (keyboard, mouse, touch, controllers). It registers with the input system and dispatches input events to subscribed listeners.

## Namespace
`Universe.Core`

## Properties

| Property | Type | Description                                                       |
|----------|------|-------------------------------------------------------------------|
| active   | bool | Whether this input controller is currently active (default: true) |

## Events

| Event         | Parameters                                                            | Description                                                        |
|---------------|-----------------------------------------------------------------------|--------------------------------------------------------------------|
| OnActionEvent | (string panel, string sender, string action, bool state, object data) | Triggered when an action input occurs (button press/release)       |
| OnAxisEvent   | (string panel, string sender, string action, vector3 direction)       | Triggered when an axis input occurs (analog stick, mouse movement) |

## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the controller with the input system.

### SetActivation
```csharp
void SetActivation(bool state)
```
Enables or disables the input controller.

#### Parameters
- `state`: Whether the controller should be active

### OnAction
```csharp
void OnAction(string panel, string sender, string action, bool state, object data)
```
Called by the input system when an action input occurs. Forwards the event to subscribers if the controller is active.

#### Parameters
- `panel`: The UI panel that triggered the action, if any
- `sender`: The input element that triggered the action
- `action`: The name of the action
- `state`: True for press/down, false for release/up
- `data`: Additional data related to the action

### OnAxis
```csharp
void OnAxis(string panel, string sender, string action, vector3 direction)
```
Called by the input system when an axis input occurs. Forwards the event to subscribers if the controller is active.

#### Parameters
- `panel`: The UI panel that triggered the axis input, if any
- `sender`: The input element that triggered the axis input
- `action`: The name of the axis
- `direction`: The direction and magnitude of the input

## Example Usage
```csharp
// Create a basic input controller
InputController input = new InputController();

// Subscribe to action events (like button presses)
input.OnActionEvent += (panel, sender, action, state, data) => {
    if (action == "Jump" && state) {
        // Player pressed jump button
        playerCharacter.Jump(true);
    }
    
    if (action == "Fire" && state) {
        // Player pressed fire button
        weapon.Fire();
    }
};

// Subscribe to axis events (like movement or looking)
input.OnAxisEvent += (panel, sender, action, direction) => {
    if (action == "Move") {
        // Player is moving
        playerCharacter.SetInput(direction.x, direction.z);
    }
    
    if (action == "Look") {
        // Player is looking/aiming
        cameraController.UpdateRotation(direction);
    }
};

// Temporarily disable input
input.SetActivation(false);

// Later, re-enable input
input.SetActivation(true);
```

## Implementation Details
- The input controller acts as a mediator between the input system and game logic
- Multiple input controllers can be active simultaneously, allowing for different input handling in different game states
- The controller filters events based on its activation state and the script's activation state
- Action events typically represent discrete inputs (button presses)
- Axis events typically represent continuous inputs (joystick, mouse movement)

## Use Cases
- Character control
- Camera control
- UI navigation
- Vehicle control
- Menu input handling
- Debug controls

## Notes
- The input system mapping (binding keys/buttons to actions) is configured elsewhere
- For game state management, consider using multiple input controllers with different subscribers
- To completely block input, set `active` to false
- The controller checks both its `active` property and the script's activation state

## Dependencies
- Uses `InputUtil.AddInputListener()` to register with the input system
- Uses `UniObjectUtil.GetScriptActivation()` to check script activation state
