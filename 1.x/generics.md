---
layout: project
version: 1.x
title: Generic validation keywords
description: php opis json schema generic validation keywords
keywords: opis, php, json, schema, generic, validation, type, enum, const
---

The `type`, `const`, and `enum` generic keywords, allow you to validate JSON data, 
by checking if its value, or its type, matches a given value or type. 
The keywords can be used with all JSON types and are evaluated in the order on which they are presented below. 
All these keywords are optional.


## type

The `type` keyword specifies the type of data that the schema is expecting to validate.
This keyword is not mandatory and the value of the keyword must be a string,
representing a valid [data type][data_types], or an array of strings, representing a
valid list of [data types][data_types].

{% capture schema %}
```json
{
  "type": "string"
}
```
{% endcapture %}
{% capture data %}
|Input|Status|
|-----|------|
| `"some text"`{:.language-json} | *valid*{:.text-success.text-normal} |
| `""`{:.language-json} | *valid*{:.text-success.text-normal} - empty string |
| `12`{:.language-json} | *invalid*{:.text-danger.text-normal} - is integer/number |
| `null`{:.language-json} | *invalid*{:.text-danger.text-normal} - is null |
{:.table}
{% endcapture %}
{% include tabs.html 1="Schema" 2="Data" _1=schema _2=data %}

When specifying multiple types, their order is irrelevant to the validation process, but
you should make sure that a data type is specified only once. 

```json
{
  "type": ["object", "null"]
}
```

`{"a": 1}` - valid (is object)
{:.alert.alert-success}

`null` - valid (is null)
{:.alert.alert-success}

`"1, 2, 3"` - invalid (is string)
{:.alert.alert-danger}

`[{"a": 1}, {"b": 2}]` - invalid (is array)
{:.alert.alert-danger}

```json
{
  "type": ["number", "string", "null"]
}
```

`-10.5` - valid (is number)
{:.alert.alert-success}

`"some string"` - valid (is string)
{:.alert.alert-success}

`null` - valid (is null)
{:.alert.alert-success}

`false` - invalid (is boolean)
{:.alert.alert-danger}

`{"a": 1}` - invalid (is object)
{:.alert.alert-danger}

`[1, 2, 3]` - invalid (is array)
{:.alert.alert-danger}

## const

An instance validates against this keyword if its value equals to the
value of this keyword. The value of this keyword can be anything.

```json
{
  "const": "test"
}
```
Validates if equals to `"test"`.
{:.blockquote-footer}

`"test"` - valid
{:.alert.alert-success}

`"Test"` - invalid
{:.alert.alert-danger}

`"tesT"` - invalid
{:.alert.alert-danger}

`3.4` - invalid
{:.alert.alert-danger}

```json
{
  "const": {
    "a": 1,
    "b": "2"
  }
}
```
Validates if the object have the same properties and values (order of properties does not matter).
{:.blockquote-footer}

`{"a": 1, "b": "2"}` - valid
{:.alert.alert-success}

`{"b": "2", "a": 1}` - valid
{:.alert.alert-success}

`{"a": 1, "b": "2", "c": null}` - invalid
{:.alert.alert-danger}

`5.10` - invalid
{:.alert.alert-danger}

## enum

An instance validates against this keyword if its value equals can be
found in the items defined by the value of this keyword. 
The value of this keyword must be an array containing anything.
An empty array is not allowed.

```json
{
  "enum": ["a", "b", 1, null]
}
```

`"a"` - valid
{:.alert.alert-success}

`"b"` - valid
{:.alert.alert-success}

`1` - valid
{:.alert.alert-success}

`null` - valid
{:.alert.alert-success}

`"A"` - invalid
{:.alert.alert-danger}

`-1` - invalid
{:.alert.alert-danger}

`false` - invalid
{:.alert.alert-danger}

`["a", "b", 1, null]` - invalid
{:.alert.alert-danger}


[data_types]: ./structure.html#data-types "Data types"
