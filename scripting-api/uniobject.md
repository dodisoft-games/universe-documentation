---
layout: default
title: UniObject
nav_order: 5
parent: Scripting API
---
# UniObject

## Overview

The UniObject class represents a fundamental object. It provides various methods for interacting with objects in the scene, such as manipulating transformations, attaching scripts, and handling materials.

## Properties

| string tag | The tag associated with the object. |
| UniAsset asset | The asset representing the object's appearance or data. |
| vector3 position | The object's position in the world. |
| vector3 rotation | The object's rotation in the world. |
| vector3 scale | The object's scale in the world. |
| bool persistent | Indicates if the object persists across scenes (default: false). |

## Methods

| string GetName() | Retrieves the name of the object. |
| void SetName(string name) | Sets the name of the object. |
| bool GetActivation() | Returns whether the object is active. |
| void SetActivation(bool enabled) | Sets the object's activation state. |
| uniscript GetScript(string name) | Retrieves a script attached to the object by name. |
| uniscript AddScript(string name) | Attaches a new script to the object. |
| void RemoveScript(string name) | Removes a script from the object by name. |
| void RemoveScriptComponent(uniscript script) | Removes a specific script component from the object. |
| void SetColor(float r, float g, float b, float a) | Sets the object's color. |
| void SetMaterial(Shaders shader, UniAsset texture) | Assigns a material with a specified shader and texture. |
| void SetShader(Shaders shader) | Sets the object's shader. |
| void LookAt(UniObject target) | Rotates the object to face another object. |
| void LookAtPoint(vector3 target) | Rotates the object to face a point in space. |
| void LookAtSmooth(UniObject target, float speed) | Smoothly rotates the object to face another object. |
| void LookAtSmoothWithOffset(UniObject target, vector3 offset, float speed) | Smoothly rotates the object to face another object with an offset. |
| void Rotate(float x, float y, float z) | Rotates the object by the given angles. |
| void Translate(float x, float y, float z) | Moves the object by the given values. |
| vector3 GetWorldPosition() | Returns the object's world position. |
| void SetWorldPosition(vector3 pos) | Sets the object's world position. |
| vector3 Forward() | Returns the forward direction vector. |
| vector3 Right() | Returns the right direction vector. |
| vector3 Up() | Returns the up direction vector. |
| void Destroy() | Destroys the object. |
| quaternion GetRotation() | Returns the object's rotation. |
| void SetRotation(quaternion rot) | Sets the object's rotation. |
| void ReParent(uniscript parent) | Changes the object's parent. |
| void Reset() | Resets the object's position, rotation, and scale. |
| UniObject GetParent() | Retrieves the parent of the object. |
| List GetChilds() | Retrieves the list of child objects. |
| void InstantiateAsync(UniAsset pack, string name, uniscript callbackscript, string callbackMethod, object ref) | Asynchronously instantiates an object and invokes a callback method. |
| void InstantiateOnTransform(UniAsset pack, string name, vector3 newPosition, vector3 newRotation, vector3 newScale) | Instantiates an object at a specified transformation. |
| void OnObjectInstantiated(UniObject createdObject, Dictionary pars) | Callback method handling object instantiation. |
| UniObject GetUniObject(uniscript script) | Retrieves the UniObject associated with a given script. |