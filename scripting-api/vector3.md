---
layout: default
title: Vector3
nav_order: 6
parent: Scripting API
---
# Vector3

## Overview

The Vector3 class represents a three-dimensional vector commonly used for position, rotation, and direction calculations.

## Properties

| float x | The X component of the vector. |
| float y | The Y component of the vector. |
| float z | The Z component of the vector. |

## Methods

| Vector3(float xV, float yV, float zV) | Initializes a new vector with the specified coordinates. |
| Vector3 New(float xV, float yV, float zV) | Sets the vector's components to new values. |
| Vector3 Zero() | Resets the vector to (0,0,0). |
| Vector3 One() | Sets the vector to (1,1,1). |
| Vector3 Right() | Sets the vector to (1,0,0). |
| Vector3 Left() | Sets the vector to (-1,0,0). |
| Vector3 Up() | Sets the vector to (0,1,0). |
| Vector3 Down() | Sets the vector to (0,-1,0). |
| Vector3 Forward() | Sets the vector to (0,0,1). |
| Vector3 Backward() | Sets the vector to (0,0,-1). |
| Vector3 Add(Vector3 vector) | Adds another vector to this one. |
| Vector3 Normalize() | Normalizes the vector to unit length. |
| Vector3 Normalized() | Returns a normalized version of this vector. |
| float Magnitude() | Returns the magnitude (length) of the vector. |
| Vector3 Cross(Vector3 vector) | Returns the cross product with another vector. |
| float Dot(Vector3 vector) | Returns the dot product with another vector. |
| Vector3 Lerp(Vector3 to, float phase) | Linearly interpolates between two vectors. |
| Vector3 SmoothLerp(Vector3 to, float phase) | Smoothly interpolates between two vectors. |
| Vector3 Project(Vector3 normal) | Projects this vector onto another vector. |
| Vector3 FromVector(vector3 vector) | Converts a vector3 to a Vector3. |
| vector3 ToVector() | Converts this Vector3 to a vector3 object. |