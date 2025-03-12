---
layout: default
title: AudioPlayer
nav_order: 3
parent: Scripting API
---
# AudioPlayer

## Description
The `AudioPlayer` class provides functionality for playing audio clips in the game world. It supports both 2D and 3D sound with configurable volume, range, and distribution modes.

## Namespace
`Universe.Core`

## Enums

### DistributionMode
Defines how sound attenuation is calculated over distance.

| Value | Description |
|-------|-------------|
| Logarithmic | Sound attenuates logarithmically with distance (more realistic) |
| Linear | Sound attenuates linearly with distance |

## Properties
| Property  | Type             | Description                                                                    |
|-----------|------------------|--------------------------------------------------------------------------------|
| clip      | UniAsset         | The audio clip to play                                                         |
| mode      | DistributionMode | Determines how sound volume decreases over distance                            |
| volume    | float            | The base volume of the audio clip (default: 1)                                 |
| range     | float            | The maximum distance the sound can be heard from (default: 200)                |
| autoStart | bool             | When true, the audio will play automatically on initialization (default: true) |
| is3D      | bool             | When true, the sound is positioned in 3D space (default: true)                 |
| loop      | bool             | When true, the audio will loop continuously (default: false)                   |


## Methods

### OnInit
```csharp
void OnInit()
```
Called when the script initializes. Registers the audio player with the audio system.

### Play
```csharp
void Play()
```
Starts playing the audio clip.

### Stop
```csharp
void Stop()
```
Stops playing the audio clip.

### Pause
```csharp
void Pause()
```
Pauses the currently playing audio clip.

## Example Usage
```csharp
// Create a background music player
AudioPlayer musicPlayer = new AudioPlayer();
musicPlayer.clip = backgroundMusicAsset;
musicPlayer.is3D = false; // 2D sound for background music
musicPlayer.loop = true;
musicPlayer.volume = 0.8f;
musicPlayer.Play();

// Create a 3D sound effect
AudioPlayer explosionSound = new AudioPlayer();
explosionSound.clip = explosionSoundAsset;
explosionSound.is3D = true;
explosionSound.range = 100;
explosionSound.volume = 1.0f;
explosionSound.mode = DistributionMode.Logarithmic;
explosionSound.autoStart = false; // Don't play until triggered
```

## Dependencies
- Uses `AudioUtil` for the actual audio functionality
