---
layout: default
title: Wiki - JSON format
---

JSON stands for JavaScript Object Notation and is pronounced /ˈdʒeɪsən/.

JSON is a way to represent objects in a human-readable form.

There are a few important things to know about JSON:
- types
- structures
- formatting
- referencing

## Types
There are only three types in JSON: `string`, `number` and `boolean`.
There is also a `null`, but that's not really a type, it denotes absence of value.

### String
String is just a sequence of characters wrapped into a pair double quotes. Here are a few examples.

```json
"I am a string"

"I am a string too"
```

There are a number of special characters that have special meaning when used in a string.
For example, backslash is a special character that makes other special characters, 
like `\n` would be a new line, `\\` would be just one backspace, `\"` would be double quotes in a string.

For instance, the following string would represent two lines with a `"name"` on the first line and `"age"=11` on the second line:

```json
" \"name\" \n \"age\"=11 "
```

would actually be

```
"name"
"age"=11
```

### Number
Numbers in JSON could be integers or decimals. Have a look at few examples of numbers.

```json
23
0.45
49.06
```

### Boolean
Boolean type can have one of two values: `true` or `false`.

## Structures
There are only two structures in JSON: `array` and `object`.

### Array
Array is an _ordered_ sequence of values. It is just like a list - all values have position (index) and are indexed starting from `0`.

Array is represented in JSON using square brackets, for example:

```json
[34, 89, 40.6]
```

Values in array are separated by commas.

Array in JSON can only have values of one type, just like lists. That means there could only be an array of strings, an array of numbers or an array of booleans. Here is an example of an array of strings.

```json
["string1", "string2", "string3"]
```

### Object
Object is an _unordered_ sequence of keys and values. A value in an object can be found by its key.

For example, here is an object:

```json
{
  "key1": "value1",
  "key2": 45,
  "key3": "another value"
}
```

Keys are always put in double quotes. Values are written according to their type - strings in double quotes, numbers and booleans go without double quotes.

Keys are separated from values by colon.

Pairs of keys and values are separated by comma.

### Complex objects
In JSON any value could be another object or another array.

Here is an example of complex object.

```json
{
  "key1": {
    "inner-key1": "inner value 1",
    "inner-key2": [ "I", "am", "an", "array" ],
    "inner-key3": true,
    "inner-key4": null
  }
}
```

In that example we can see an object that has one key - `key1`.  
The value that corresponds to that key is another object.  
That other object has four keys - `inner-key1`, `inner-key2`, `inner-key3` and `inner-key4`.  
Key `inner-key1` has a string for its value - `inner value 1`.  
Key `inner-key2` has an array for its value.  
Key `inner-key3` has a boolean for its value.
Key `inner-key3` has a `null` for its value, which means there is no value.

A JSON document can be an object or an array. The JSON document above is an object, but it could as well have been an array:

```json
[ "I", "am", "a", "JSON", "document", "made", "from", "array" ]
```

## Formatting
The formatting rules are pretty loose for JSON. As long as the main rules above are respected, the rest can be formatted any way you like.

Have a look at this document:

```json
{ "key1": [     "a",         "string"  , "array"  ] 


}
```

That is a valid JSON object, although it looks really ugly.

## Path references
Any value in a JSON document can be referenced in a line like the following, which would find value `true` in the object above:

```yaml
$.key1["inner-key3"]
```

The rules for path referencing are:
- if a key starts with a letter and has only letters, numbers or underscores, then it can be used like `key1` was used in the reference
- in all other cases the key must be wrapped into double quotes and square brackets, like `inner-key3` because of the dash.
