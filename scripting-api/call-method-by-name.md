---
layout: default
title: CallMethodByName
nav_order: 5
parent: Scripting API
---
# CallMethodByName

## Description
The `CallMethodByName` class provides a flexible way to call methods on other scripts by name, either immediately or after a specified delay. This is useful for creating event chains, delayed reactions, or connections between different components.

## Namespace
`Universe.Helper`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| callScript | uniscript | Reference to the script containing the method to call |
| methodName | string | Name of the method to call |
| parameter | string | String parameter to pass to the method (can be null) |
| delay | float | Time in seconds to wait before calling the method (0 for immediate execution) |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. Initiates the method call, either immediately or after the specified delay.

### Call
```csharp
void Call()
```
Performs the actual method call on the target script with the specified parameter.

## Example Usage
```csharp
// Call a method immediately on start
CallMethodByName immediateCall = new CallMethodByName();
immediateCall.callScript = targetScript;
immediateCall.methodName = "Initialize";
immediateCall.parameter = "defaultConfig";
immediateCall.delay = 0;

// Create a delayed method call
CallMethodByName delayedCall = new CallMethodByName();
delayedCall.callScript = doorScript;
delayedCall.methodName = "Close";
delayedCall.delay = 5.0; // Close the door after 5 seconds
```

## Use Cases
- Creating sequences of events with specific timing
- Implementing delayed reactions to player actions
- Coordinating behavior between unrelated components
- Setting up simple state machines
- Implementing level scripting and game logic

## Notes
- Only supports a single string parameter; for more complex parameter passing, consider using events instead
- For recursive or repeating method calls, create the CallMethodByName instance within the called method

## Dependencies
- Uses `Utility.CallMethodDelayed()` for delayed execution
- Uses `Utility.CallMethod()` for immediate execution
