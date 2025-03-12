---
layout: default
title: AccessoryAttachment
nav_order: 1
parent: Scripting API
---
# AccessoryAttachment

## Description
The `AccessoryAttachment` class is used to attach accessories to character bones. It can automatically attach on start, with options for immediate or delayed attachment.

## Namespace
`Universe.Character`

## Properties

| Property     | Type          | Description                                                               |
|--------------|---------------|---------------------------------------------------------------------------|
| character    | Character     | Reference to the character the accessory will be attached to              |
| bone         | CharacterBone | The bone to attach the accessory to                                       |
| autoAttach   | bool          | When true, the accessory will automatically attach during start           |
| oneFrameLate | bool          | When true, the accessory will attach after a slight delay (0.001 seconds) |
| position     | vector3       | Local position offset for the attachment                                  |
| rotation     | vector3       | Local rotation offset for the attachment                                  |

## Methods

### OnStart
```csharp
void OnStart()
```
Called when the script starts. If `autoAttach` is true, this will trigger the attachment process.

### Attach
```csharp
void Attach()
```
Attaches the accessory to the specified character bone with the configured position and rotation offsets.

## Example Usage
```csharp
// Create a helmet accessory attached to the character's head
AccessoryAttachment helmet = new AccessoryAttachment();
helmet.character = playerCharacter;
helmet.bone = CharacterBone.Head;
helmet.position = [0, 0.1, 0]; // Slight upward offset
helmet.rotation = [0, 0, 0];
helmet.autoAttach = true;
```

## Dependencies
- Requires `Universe.Core`
- Uses `CharacterUtil.AttachAccessory()` for the actual attachment logic
