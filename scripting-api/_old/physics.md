---
layout: default
title: Physics
nav_order: 1
parent: Scripting API
---
# Physics

## Overview

The Physics class handles physics-based interactions such as forces, velocity, and collisions.

## Properties

| uniscript eventReceiver | | 
| bool gravity | Enables or disables gravity. |
| bool freeze | Freezes the object's movement. |
| float mass | The mass of the object. |
| float friction | The friction applied to the object. |
| bool lockXPosition, lockYPosition, lockZPosition | Locks movement along specific axes. |
| bool lockXRotation, lockYRotation, lockZRotation | Locks rotation along specific axes. |

## Methods

| void AddForce(float x, float y, float z, ForceMode mode) | Applies a force to the object. |
| void AddForceVector(vector3 force, ForceMode mode) | Applies a force to the object. |
| void AddTorque(float x, float y, float z, ForceMode mode) | Applies torque to the object. |
| void AddTorqueVector(vector3 force, ForceMode mode) | Applies torque to the object. |
| vector3 GetVelocity() | Retrieves the object's velocity. |
| void SetVelocity(vector3 velocity) | Sets the object's velocity. |
| vector3 GetAngularVelocity() | Retrieves the object's angular velocity. |
| void SetAngularVelocity(vector3 velocity) | Sets the object's angular velocity. |
| RaycastHit Raycast(vector3 position, vector3 direction, float maxDistance) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns the first hit. |
| RaycastHit RaycastWithTag(vector3 position, vector3 direction, float maxDistance, string tag) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns the first hit if the hit object is tagged with `tag` |
| RaycastHit RaycastWithTags(vector3 position, vector3 direction, float maxDistance, list tags) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns the first hit if the hit object is tagged with any of the `tags` |
| RaycastHit RaycastAll(vector3 position, vector3 direction, float maxDistance) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns all hits. |
| RaycastHit RaycastAllWithTag(vector3 position, vector3 direction, float maxDistance, string tag) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns all hits if the hit objects are tagged with `tag` |
| RaycastHit RaycastAllWithTags(vector3 position, vector3 direction, float maxDistance, list tags) | Casts a ray that starts from `position` in the direction of `direction` that is `maxDistance` long and returns all hits if the hit objects are tagged with any of the `tags` |