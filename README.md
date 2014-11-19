# GIML

Gazay's incomplete Minimalistic Language.

By Alexey Gaziev.

## Objectives

Smallest and incomplete language with static typing for big but simple config files.

## Example

```giml
# This is comment and nobody cares what you'll write after '#'

:text: text_variable
Multiline
value for
variable name
untill next '"' in beginning of line

# Array should contain values of one type and they should be splitted by ', '
:array: array_variable
Some, string, with, another

# This array will be parsed with three elements, because ',' was escaped with '\'
:array: escaped_array_variable
Some, string\, with, another

:array: numeric_array_variable
1, 2, 3, 4

# Vertical array should contain values of one type and they should be written each on separate line with '- ' in beginning
:varray: vertical_array_variable
- value
- another value
- values in array should be all of one type

:num: numeric_variable
123

:num: float_number_variable
123.321
```

## Spec

Variable names should be written in one word without special characters.

There are only 4 types of variables:

1. `num`    - numeric value. Can be an `integer` or `float`.
2. `text`   - text value. All what goes under name of variable will be parsed as one line of text, splitted if needed with `\n` symbol.
3. `array`  - single level list of values of one type. Values can be `text` OR `integer` OR `float`. Values should be splitted by `, `.
4. `varray` - same as `array`, but values splitted with `- ` and each value on separate line.

