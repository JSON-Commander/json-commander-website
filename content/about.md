+++
title = "About JSON Commander"
toc = true
+++

## What is JSON Commander?

JSON Commander is a header-only C++20 library that lets you define command-line
interfaces declaratively using JSON schemas. Inspired by OCaml's
[cmdliner](https://erratique.ch/software/cmdliner), it takes a schema-driven
approach: describe your CLI's structure — commands, options, types, defaults —
in a JSON document, and JSON Commander handles argument parsing, validation,
type conversion, help generation, man page output, and JSON configuration
output.

## Design Philosophy

**Declarative over imperative.** CLI structure belongs in data, not code. A JSON
schema is easier to read, validate, and generate tooling for than scattered
`add_option()` calls.

**Type safety.** Parsed arguments are returned with their declared types.
Invalid input is caught at parse time with clear error messages, not at use
time with undefined behavior.

**Zero boilerplate.** A single `json_commander::run()` call handles parsing,
`--help`, `--version`, and `--man` dispatch. A schema file replaces hundreds
of lines of argument parsing setup.

**Composable.** Subcommands nest naturally in JSON. Complex CLI tools like
`git` can be described as a tree of schemas — see the `fake-git` example in
the repository.

## Features

- JSON schema-driven CLI definition
- Type-safe argument parsing (string, int, float, bool, enum, file, dir, path)
- Compound types (list, pair, triple)
- Flag groups (mutually exclusive boolean flags)
- Nested subcommands with independent option sets
- Automatic help text generation (`--help`)
- Man page generation in groff format (`--man`)
- Default values and required/optional arguments
- Positional arguments
- Environment variable fallbacks
- Config schema generation (JSON Schema draft 2020-12)
- Schema validation against the json-commander metaschema
- C API shared library (`jcmd_run()`) for embedding and FFI
- Self-hosting CLI tool (`json-commander validate`, `man`, `parse`, ...)
- Header-only C++20 library — no separate compilation step
- CMake integration with FetchContent

## License

JSON Commander is released under the [MIT License](https://opensource.org/licenses/MIT).

## Source Code

The source is hosted on GitHub: [github.com/JSON-Commander/json-commander](https://github.com/JSON-Commander/json-commander)
