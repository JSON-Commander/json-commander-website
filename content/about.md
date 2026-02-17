+++
title = "About JSON Commander"
toc = true
+++

## What is JSON Commander?

JSON Commander is a C++20 library that lets you define command-line interfaces
declaratively using JSON schemas. Instead of writing imperative argument parsing
code, you describe your CLI's structure — commands, options, types, defaults —
in a JSON document, and JSON Commander handles parsing, validation, type
conversion, and help generation.

## Design Philosophy

**Declarative over imperative.** CLI structure belongs in data, not code. A JSON
schema is easier to read, validate, and generate tooling for than scattered
`add_option()` calls.

**Type safety.** Parsed arguments are returned with their declared types.
Invalid input is caught at parse time with clear error messages, not at use
time with undefined behavior.

**Zero boilerplate.** A single schema file replaces hundreds of lines of
argument parsing setup. Help text, usage messages, and error formatting come
for free.

**Composable.** Subcommands nest naturally in JSON. Complex CLI tools like
`git` or `docker` can be described as a tree of schemas.

## Features

- JSON schema-driven CLI definition
- Type-safe argument parsing (string, integer, float, boolean, arrays)
- Nested subcommands with independent option sets
- Automatic help and usage generation
- Default values and required/optional options
- Positional arguments
- Environment variable fallbacks
- Modern C++20 (concepts, ranges, structured bindings)
- Header-only or compiled library options
- CMake and pkg-config integration

## License

JSON Commander is released under the [MIT License](https://opensource.org/licenses/MIT).

## Source Code

The source is hosted on GitHub: [github.com/json-commander/json-commander](https://github.com/json-commander/json-commander)
