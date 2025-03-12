---
layout: default
title: String
nav_order: 45
parent: Scripting API
---
# String

## Description
The `String` class provides a comprehensive set of string manipulation operations for the Universe framework. It wraps the native string type with methods for searching, modifying, and analyzing text.

## Namespace
`Universe.Core`

## Properties
| Property | Type | Description |
|----------|------|-------------|
| text | string | The underlying string value being manipulated |

## Methods

### String
```csharp
void String(string value)
```
Constructor that initializes the String with a value.

#### Parameters
- `value`: The initial string value

### Contains
```csharp
bool Contains(string value)
```
Checks if the string contains a specified substring.

#### Parameters
- `value`: The substring to search for

#### Returns
- `true` if the substring is found, `false` otherwise

### EndsWith
```csharp
bool EndsWith(string value)
```
Checks if the string ends with a specified substring.

#### Parameters
- `value`: The substring to check for

#### Returns
- `true` if the string ends with the specified value, `false` otherwise

### IndexOf
```csharp
int IndexOf(string value)
```
Finds the index of the first occurrence of a substring.

#### Parameters
- `value`: The substring to find

#### Returns
- The index position of the value, or -1 if not found

### IndexOfAny
```csharp
int IndexOfAny(string chars)
```
Finds the index of the first occurrence of any character from a set.

#### Parameters
- `chars`: String containing characters to search for

#### Returns
- The index of the first matched character, or -1 if none found

### Insert
```csharp
string Insert(int index, string value)
```
Inserts a string at a specified position.

#### Parameters
- `index`: The position to insert at
- `value`: The string to insert

#### Returns
- The new string with the inserted value

### LastIndexOf
```csharp
int LastIndexOf(string value)
```
Finds the index of the last occurrence of a substring.

#### Parameters
- `value`: The substring to find

#### Returns
- The index position of the value, or -1 if not found

### LastIndexOfAny
```csharp
int LastIndexOfAny(string chars)
```
Finds the index of the last occurrence of any character from a set.

#### Parameters
- `chars`: String containing characters to search for

#### Returns
- The index of the last matched character, or -1 if none found

### Length
```csharp
int Length()
```
Gets the length of the string.

#### Returns
- The number of characters in the string

### Merge
```csharp
string Merge(string value)
```
Concatenates this string with another value.

#### Parameters
- `value`: The string to concatenate

#### Returns
- The concatenated string

### PadLeft
```csharp
string PadLeft(string character, int length)
```
Pads the string on the left with a specified character.

#### Parameters
- `character`: The padding character
- `length`: The desired total length

#### Returns
- The padded string

### PadRight
```csharp
string PadRight(string character, int length)
```
Pads the string on the right with a specified character.

#### Parameters
- `character`: The padding character
- `length`: The desired total length

#### Returns
- The padded string

### RemoveTillEnd
```csharp
string RemoveTillEnd(int start)
```
Removes all characters from a specified position to the end.

#### Parameters
- `start`: The starting position for removal

#### Returns
- The modified string

### Remove
```csharp
string Remove(int start, int length)
```
Removes a specified number of characters from a specified position.

#### Parameters
- `start`: The starting position for removal
- `length`: The number of characters to remove

#### Returns
- The modified string

### Replace
```csharp
string Replace(string search, string replace)
```
Replaces all occurrences of a substring with another string.

#### Parameters
- `search`: The string to find
- `replace`: The string to replace with

#### Returns
- The string with replacements

### Split
```csharp
List Split(string divider)
```
Splits the string into substrings using a specified divider.

#### Parameters
- `divider`: The string that delimits the substrings

#### Returns
- A List containing the substrings

### SplitAny
```csharp
List SplitAny(string dividerChars)
```
Splits the string into substrings at any of the specified characters.

#### Parameters
- `dividerChars`: String containing delimiter characters

#### Returns
- A List containing the substrings

### StartsWith
```csharp
bool StartsWith(string value)
```
Checks if the string starts with a specified substring.

#### Parameters
- `value`: The substring to check for

#### Returns
- `true` if the string starts with the specified value, `false` otherwise

### SubstringTillEnd
```csharp
string SubstringTillEnd(int start)
```
Extracts a substring from a specified position to the end.

#### Parameters
- `start`: The starting position

#### Returns
- The extracted substring

### Substring
```csharp
string Substring(int start, int length)
```
Extracts a substring with a specified length from a specified position.

#### Parameters
- `start`: The starting position
- `length`: The number of characters to extract

#### Returns
- The extracted substring

### ToLower
```csharp
string ToLower()
```
Converts the string to lowercase.

#### Returns
- The lowercase string

### ToUpper
```csharp
string ToUpper()
```
Converts the string to uppercase.

#### Returns
- The uppercase string

### Trim
```csharp
string Trim()
```
Removes whitespace from both ends of the string.

#### Returns
- The trimmed string

### TrimEnd
```csharp
string TrimEnd()
```
Removes whitespace from the end of the string.

#### Returns
- The trimmed string

### TrimStart
```csharp
string TrimStart()
```
Removes whitespace from the start of the string.

#### Returns
- The trimmed string

## Example Usage
```csharp
// Create a string and manipulate it
String message = new String("Hello, World!");

// Basic information
int length = message.Length(); // 13

// Searching
bool containsHello = message.Contains("Hello"); // true
int worldPosition = message.IndexOf("World"); // 7
bool endsWithExclamation = message.EndsWith("!"); // true

// Modifying
String greeting = new String("Hello");
String fullGreeting = new String(greeting.Merge(", User!")); // "Hello, User!"
String replaced = new String(message.Replace("World", "Universe")); // "Hello, Universe!"
String inserted = new String(message.Insert(7, "Beautiful ")); // "Hello, Beautiful World!"

// Extracting parts
String firstWord = new String(message.Substring(0, 5)); // "Hello"
String lastPart = new String(message.SubstringTillEnd(7)); // "World!"

// Splitting
List parts = message.Split(", ");
// parts.Get(0) is "Hello"
// parts.Get(1) is "World!"

// Case conversion
String lowercase = new String(message.ToLower()); // "hello, world!"
String uppercase = new String(message.ToUpper()); // "HELLO, WORLD!"

// Trimming
String paddedText = new String("  Padded  ");
String trimmed = new String(paddedText.Trim()); // "Padded"
```

## Notes
- This class provides an object-oriented wrapper around string functions
- Most methods return new strings rather than modifying the original
- The methods rely on `StringUtil` for the actual implementation
- For methods that return a string, you'll need to wrap the result in a new String object to continue method chaining
- For parsing more complex formats, consider implementing custom parser functions

## Related Components
- Used throughout the framework for text processing
- Useful for UI text, game dialogue, command parsing, and data processing

## Dependencies
- Uses `StringUtil` for the actual string operations
