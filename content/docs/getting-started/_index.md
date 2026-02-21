+++
title = "Getting Started"
weight = 1
+++

This guide walks you through installing JSON Commander and building your first
CLI application.

## Prerequisites

JSON Commander requires:

- A **C++20** compatible compiler (GCC 12+, Clang 16+, or Apple Clang via Xcode 15+)
- **CMake** 3.12 or later (3.21+ if using presets)

Dependencies (nlohmann/json, json-schema-validator, Catch2) are fetched
automatically via CMake FetchContent — no manual installation needed.

## Installation

### Using CMake FetchContent

The simplest way to add JSON Commander to your project:

```cmake
include(FetchContent)
FetchContent_Declare(
  json_commander
  GIT_REPOSITORY https://github.com/JSON-Commander/json-commander.git
  GIT_TAG v0.2.0
)
FetchContent_MakeAvailable(json_commander)

target_link_libraries(your_target PRIVATE
  json_commander::header
  json_commander::library
  nlohmann_json::nlohmann_json
  nlohmann_json_schema_validator)
```

### Building from Source

```sh
git clone --recurse-submodules https://github.com/JSON-Commander/json-commander.git
cd json-commander
cmake --preset <preset-name>
cmake --build build --config Release
ctest --test-dir build -C Release --output-on-failure
```

Presets are defined per-compiler in `CMakeUserPresets.json` (auto-generated
from `compilers.json`). See the repository README for details.

## Your First CLI

Create a schema file `greet.json`:

```json
{
  "name": "greet",
  "doc": ["A friendly greeting tool."],
  "version": "1.0.0",
  "args": [
    {
      "kind": "flag",
      "names": ["loud", "l"],
      "doc": ["Print the greeting in uppercase."]
    },
    {
      "kind": "positional",
      "name": "name",
      "doc": ["The name to greet."],
      "type": "string",
      "required": true
    }
  ]
}
```

Write the C++ code (`greet.cpp`):

```cpp
#include <json_commander/run.hpp>

#include <iostream>
#include <string>

int main(int argc, char *argv[]) {
  return json_commander::run_file(GREET_SCHEMA, argc, argv,
    [](const nlohmann::json &config) {
      auto name = config["name"].get<std::string>();
      auto loud = config["loud"].get<bool>();

      std::string greeting = "Hello, " + name + "!";
      if (loud) {
        std::transform(greeting.begin(), greeting.end(),
          greeting.begin(), ::toupper);
      }
      std::cout << greeting << "\n";
      return 0;
    });
}
```

The `GREET_SCHEMA` macro is set via CMake to point at the JSON file:

```cmake
add_executable(greet greet.cpp)
target_link_libraries(greet PRIVATE
  json_commander::header
  json_commander::library
  nlohmann_json::nlohmann_json
  nlohmann_json_schema_validator)
target_compile_definitions(greet PRIVATE
  GREET_SCHEMA="${CMAKE_CURRENT_SOURCE_DIR}/greet.json")
```

Build and run:

```sh
cmake --preset <preset-name>
cmake --build build --config Release
./build/examples/greet/Release/greet Alice
```

```
Hello, Alice!
```

```sh
./build/examples/greet/Release/greet --loud Alice
```

```
HELLO, ALICE!
```

```sh
./build/examples/greet/Release/greet --help
```

```
NAME
       greet - A friendly greeting tool.

SYNOPSIS
       greet [OPTIONS] NAME

ARGUMENTS
       NAME
           The name to greet.

OPTIONS
       --loud, -l
           Print the greeting in uppercase.
```

## Next Steps

Explore the [Documentation]({{< relref "/docs" >}}) for more on schema syntax,
subcommands, type validation, and advanced features.
