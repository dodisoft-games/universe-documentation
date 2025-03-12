---
layout: default
title: Type
nav_order: 47
parent: Scripting API
---
# Type

## Description
The `Type` class provides type information and conversion utilities for working with different data types in the Universe framework. It allows checking the type of a value and converting values between different types safely.

## Namespace
`Universe.Core`

## Enums

### DataType
Defines the different data types supported by the type system.

| Value | Description |
|-------|-------------|
| Integer | Whole number values |
| Float | Floating-point number values |
| Boolean | True/false values |
| String | Text string values |
| Object | Generic object references |
| Vector3 | 3D vector values (x, y, z) |
| Quaternion | Rotation values |
| RGBA | Color values with alpha (red, green, blue, alpha) |
| Assembly | Code assembly references |
| List | Collection of items |
| Dictionary | Key-value pair collections |
| Asset | Game asset references |

## Fields
| Field | Type | Description |
|-------|------|-------------|
| intType | int | Internal type code for Integer (0) |
| floatType | int | Internal type code for Float (1) |
| boolType | int | Internal type code for Boolean (2) |
| stringType | int | Internal type code for String (3) |
| objectType | int | Internal type code for Object (4) |
| vectorType | int | Internal type code for Vector3 (5) |
| quaternionType | int | Internal type code for Quaternion (6) |
| rgbaType | int | Internal type code for RGBA (7) |
| assemblyType | int | Internal type code for Assembly (8) |
| listType | int | Internal type code for List (9) |
| dictionaryType | int | Internal type code for Dictionary (10) |
| assetType | int | Internal type code for Asset (11) |

## Methods

### GetTypeName
```csharp
string GetTypeName(object obj)
```
Gets the type name of an object as a string.

#### Parameters
- `obj`: The object to check

#### Returns
- The type name as a string

### GetType
```csharp
DataType GetType(object obj)
```
Gets the DataType enum value for an object.

#### Parameters
- `obj`: The object to check

#### Returns
- The DataType enum value corresponding to the object's type

### Convert
```csharp
object Convert(object obj, DataType type)
```
Converts an object to the specified data type.

#### Parameters
- `obj`: The object to convert
- `type`: The target data type

#### Returns
- The converted object

### ConvertToInteger
```csharp
int ConvertToInteger(object obj)
```
Converts an object to an integer.

#### Parameters
- `obj`: The object to convert

#### Returns
- The integer value

### ConvertToFloat
```csharp
float ConvertToFloat(object obj)
```
Converts an object to a float.

#### Parameters
- `obj`: The object to convert

#### Returns
- The float value

### ConvertToBoolean
```csharp
bool ConvertToBoolean(object obj)
```
Converts an object to a boolean.

#### Parameters
- `obj`: The object to convert

#### Returns
- The boolean value

### ConvertToString
```csharp
string ConvertToString(object obj)
```
Converts an object to a string.

#### Parameters
- `obj`: The object to convert

#### Returns
- The string value

### ConvertToVector3
```csharp
vector3 ConvertToVector3(object obj)
```
Converts an object to a vector3.

#### Parameters
- `obj`: The object to convert

#### Returns
- The vector3 value

### ConvertToQuaternion
```csharp
quaternion ConvertToQuaternion(object obj)
```
Converts an object to a quaternion.

#### Parameters
- `obj`: The object to convert

#### Returns
- The quaternion value

### ConvertToRGBA
```csharp
rgba ConvertToRGBA(object obj)
```
Converts an object to an RGBA color.

#### Parameters
- `obj`: The object to convert

#### Returns
- The RGBA color value

### ConvertToList
```csharp
list ConvertToList(object obj)
```
Converts an object to a list.

#### Parameters
- `obj`: The object to convert

#### Returns
- The list value

## Example Usage
```csharp
// Create a Type utility instance
Type typeUtil = new Type();

// Get the type of an object
object someValue = 42;
DataType valueType = typeUtil.GetType(someValue); // Returns DataType.Integer

// Get the type name
string typeName = typeUtil.GetTypeName(someValue); // Returns "Integer"

// Convert between types
string stringValue = "123";
int intValue = typeUtil.ConvertToInteger(stringValue); // Returns 123

float floatValue = 3.14;
string floatString = typeUtil.ConvertToString(floatValue); // Returns "3.14"

// Convert using the generic Convert method
object value = "true";
bool boolValue = typeUtil.Convert(value, DataType.Boolean); // Returns true

// Convert enum values to integers
BehaviourType behaviour = BehaviourType.Follow;
int behaviourCode = typeUtil.ConvertToInteger(behaviour); // Returns the enum integer value

// Convert values for serialization
vector3 position = [1, 2, 3];
string positionString = typeUtil.ConvertToString(position); // Converts to string representation
```

## Technical Details
- Type conversions use `TypeUtil` for the actual implementation
- Conversions attempt to be intelligent about handling different formats
- Numeric conversions support parsing from strings
- Vector and quaternion conversions support various input formats
- Enum values can be converted to and from their integer representations
- For unsupported conversions, a default value or null is typically returned

## Use Cases
- Safe type conversion in scripts
- Dynamic property handling
- Data serialization and deserialization
- Command parsing and validation
- Working with configuration data
- Converting user input to appropriate types
- Handling values from external systems

## Notes
- Always check for conversion failures when converting between incompatible types
- String conversion is generally the most flexible and works with almost any type
- For complex type conversions, consider implementing custom conversion logic
- The enum integer values (intType, floatType, etc.) are implementation details and should not be relied upon directly
- Conversion performance may be important in performance-critical code paths

## Related Components
- Used throughout the framework for type operations
- Particularly useful when working with `Dictionary` and `List` classes

## Dependencies
- Uses `TypeUtil` for the actual type operations
