# GIML

Gazay's incomplete Minimalistic Language.

By Alexey Gaziev.

## Objectives

Smallest and incomplete language for big but simple config files. It should be so simple that you can write fast parser for it in few LOC and without heavy dependencies.

## Example

```giml
# This is comment and nobody cares what you'll write after '#'

:text: text_variable_name
Multiline text
value for
variable name

# List values should be splitted by ', '. They will be parsed as strings
:list: list_variable_name
Some, string, with, another

# This list will be parsed with three elements, because ',' was escaped with '\'
:list: escaped_list_variable_name
Some, string\, with, another

:list: numeric_list_variable_name
1, 2, 3, 4

# Vertical list is the same as list. Values should be written each on separate line with '- ' in beginning
:vlist: vertical_list_variable_name
- value
- another value
- values in list should be all of one type

:num: numeric_variable_name
123

:num: float_number_variable_name
123.321
```

## Spec

Variable names should be written in one word without special characters.

There are only 4 types of variables:

1. `num`    - numeric value. Can be an `integer` or `float`.
2. `text`   - text value. All what goes under name of variable will be parsed as one line of text, splitted if needed with `\n` symbol.
3. `list`   - single level list of values. Values will parsed as `text`. Values should be splitted by `, `.
4. `vlist`  - same as `list`, but values splitted with `- ` and each value on separate line.

## Parsers

- [gimlr](https://github.com/gazay/gimlr) - Ruby
- [gimlh](https://github.com/gazay/gimlh) - Haskell
