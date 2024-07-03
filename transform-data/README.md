# Transform Data

Table of Contents

* [Description](#description)
* [Requirements](#requirements)
* [How to use](#how-to-use)
* [Expected result](#expected-result)

## Description

The commands attempts to transform data from the source data type to the target data type.
Currently this commands transforming data from and to:
* JSON
* XML
* YAML
* CSV

## Requirements

There are no requirements to use this command.

## How to use

Enter the required input keys:
* data
* sourceFormat
* targetFormat

## Expected result

The expected result is to received the output data in the target format.

### Examples

* Transforming XML to JSON
Input:
```
<xml name="John" age="25">Hello</xml>
```
Output:
```
{
    "xml": {
        "@name": "John",
        "@age": 25,
        "$": "Hello"
    }
}
```

* Transforming JSON to CSV
Input:
```
[
    {
        "name": "John",
        "age": 25
    },
    {
        "name": "Monica",
        "age": 23
    }
]
```
Output:
```
name,age
John,25
Monica,23
```