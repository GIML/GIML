# GIML

Gazay's incomplete Minimalistic Language.

By Alexey Gaziev.

## Objectives

Smallest and incomplete language for big but simple config files.
It should be so simple that you can write fast parser for it in few LOC and without heavy dependencies.

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

# Vertical list is the same as list.
# Values should be written each on separate line with '- ' in beginning
:vlist: vertical_list_variable_name
- ###, really handy when value starts with #
- value
- another value
- values in list should be all of one type

:num: numeric_variable_name
123

:num: float_number_variable_name
123.321
```

## Spec

Variable names should be written in one line (any symbols acceptabe) splitted from type by space.

There are only 4 types of variables:

1. `num`    - numeric value. Can be an `integer` or `float`.
2. `text`   - text value. All what goes under name of variable will be parsed as one line of text, splitted if needed with `\n` symbol.
3. `list`   - single level list of values. Values will parsed as `text`. Values should be splitted by `, `.
4. `vlist`  - same as `list`, but values splitted with `- ` and each value on separate line.

### :num:

Numeric value. Contains only one number. Can be integer or float with format: `/\d+\.?\d*/`

```giml
:num: some_num
# This line will be ignored and one below too

1234

# This will be parsed as { "some_num" => 1234 }

:num: only_last_number_matters

1
2

# This will be parsed as { "only_last_number_matters" => 2 }

:num: some_float

123.123

# This will be parsed as { "some_float" => 123.123 }
```

### :text:

Multiline text value. Empty lines in beginning and end of text will be truncated.

```giml
:text: some_text

# Both lines above and below will be ignored

This is some
multiline text

value.

# This will be parsed as { "some_text" => "This is some\nmultiline text\n\nvalue." }
```

### :list:

Single level list of text values. Lines without any text will be ignored.
Values should be splitted with ", ".
Comma in the end of line not required and will be removed during parsing.

```giml
:list: some_list

# Both lines above and below will be ignored

1, 2, 3, 4,
# Comma in the end of line above will be ignored
5, 6, 7, 8

# This will be parsed as { "some_list" => ["1", "2", "3", "4", "5", "6", "7", "8"] }
```

If you need to save ", " as part of one of values – you can escape it like that:
```giml
:list: some_list

first value, second value\, with escaped comma, third value

# This will be parsed as { "some_list" => ["first_value", "second value, with escaped comma", "third value"] }
```

### :vlist:

Single level list of text values. Lines without any text will be ignored.
Values should be on separate lines with "- " in beginning

```giml
:vlist: some_list

- 1

- 2
- 3

# This will be parsed as { "some_list" => ["1", "2", "3"] }
```

## Why not [TOML](https://github.com/toml-lang/toml)?

TOML is super language for obvious config files.
But it is a little more complicated than needed
if you want to write not really a config file
for example for database but some file with a lot of data,
like arrays of fake names in faker libraries in any language.

Also this language was written for my Haskell education project
and I don't really want to dig into parsing
YAML there (it's super complicated for me for now) or
install and study other heavy parsers with lots of dependencies for simple data file.
I want to have parser which was written in pure language,
like a script or just a module, without any heavy dependencies and with simple output.

## Parsers

- [gimlr](https://github.com/GIML/gimlr) - Ruby
- [gimlh](https://github.com/GIML/gimlh) - Haskell
- [gimlex](https://github.com/GIML/gimlex) - Elixir
