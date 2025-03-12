---
layout: default
title: String
nav_order: 2
parent: Scripting API
---
# String

## Overview

The String class provides utility methods for string manipulation, including searching, modifying, and formatting text.

## Methods

| bool Contains(string value) | Checks if the string contains the specified substring. |
| bool EndsWith(string value) | Checks if the string ends with the specified substring. |
| int IndexOf(string value) | Finds the first occurrence of a substring. |
| int IndexOfAny(string chars) | Finds the first occurrence of any character from the given list of characters. |
| string Insert(int index, string value) | Inserts a substring at the specified position. |
| int LastIndexOf(string value) | Finds the last occurrence of a substring. |
| int LastIndexOfAny(string chars) | Finds the last occurrence of any character from the given list of characters. |
| int Length() | Returns the length of the string. |
| string Merge(string value) | Merges the current string with another string. |
| string PadLeft(string character, int length) | Creates a new string of `length` in which the beginning is padded with the given `character` |
| string PadRight(string character, int length) | Creates a new string of `length` in which the end is padded with the given `character` |
| string RemoveTillEnd(int start) | Removes the rest of the string starting from `start` |
| string Remove(int start, int length) | Removes the specified number of characters from the string starting from `start` | 
| string Replace(string search, string replace) | Replaces occurrences of a substring with another. |
| List Split(string divider) | Splits the string by the given divider and returns the list of substrings. |
| List SplitAny(string dividerChars) |
| bool StartsWith(string value) | Checks if the string starts with the specified value. |
| string SubstringTillEnd(int start) | Returns the substring that starts at `start` |
| string Substring(int start, int length) | Returns the substring that starts at `start` and is of `length` |
| string ToLower() | Converts the string to lowercase. |
| string ToUpper() | Converts the string to uppercase. |
| string Trim() | Removes leading and trailing whitespace. |
| string TrimEnd() | Removes trailing whitespace. |
| string TrimStart() | Removes leading whitespace. |