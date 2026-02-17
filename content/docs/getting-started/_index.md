+++
title = "Getting Started"
weight = 1
+++

This guide walks you through installing JSON Commander and building your first
CLI application.

## Prerequisites

JSON Commander requires:

- A **C++20** compatible compiler (GCC 12+, Clang 15+, MSVC 2022+)
- **CMake** 3.20 or later
- A JSON library (nlohmann/json is used by default)

## Installation

### Using CMake FetchContent

The simplest way to add JSON Commander to your project:

```cmake
include(FetchContent)
FetchContent_Declare(
  json_commander
  GIT_REPOSITORY https://github.com/json-commander/json-commander.git
  GIT_TAG main
)
FetchContent_MakeAvailable(json_commander)

target_link_libraries(your_target PRIVATE json_commander::json_commander)
```

### Building from Source

```sh
git clone https://github.com/json-commander/json-commander.git
cd json-commander
cmake -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build
cmake --install build
```

## Your First CLI

Create a schema file `hello.json`:

```json
{
  "name": "hello",
  "description": "Say hello",
  "options": [
    {
      "name": "name",
      "type": "string",
      "description": "Who to greet",
      "default": "World"
    }
  ]
}
```

Write the C++ code:

```cpp
#include <json_commander/json_commander.hpp>
#include <iostream>

int main(int argc, char* argv[]) {
  auto cli = json_commander::from_schema("hello.json");
  auto args = cli.parse(argc, argv);

  std::cout << "Hello, " << args.get<std::string>("name") << "!\n";
}
```

Build and run:

```sh
cmake -B build && cmake --build build
./build/hello --name "JSON Commander"
```

```
Hello, JSON Commander!
```

## Next Steps

Explore the [Documentation]({{< relref "/docs" >}}) for in-depth coverage of
schema syntax, subcommands, type validation, and advanced features.
