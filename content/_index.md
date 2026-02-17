+++
title = "JSON Commander"
toc = false
+++

{{< hextra/hero-subtitle >}}
  Define CLIs declaratively with JSON schemas.&nbsp;<br class="sm:block hidden" />
  Type-safe argument parsing, nested subcommands, and automatic help generation for C++20.
{{< /hextra/hero-subtitle >}}

<div class="mt-6 mb-6 flex flex-wrap gap-4 justify-center">
{{< hextra/hero-button text="Get Started" link="docs/getting-started" >}}
<a href="docs/" class="inline-flex items-center px-6 py-2.5 text-sm font-medium rounded-full border border-current transition-colors hover:bg-gray-100 dark:hover:bg-neutral-800">Documentation →</a>
</div>

{{< hextra/hero-section >}}
  <h2 class="text-2xl sm:text-3xl font-bold tracking-tight mt-12 mb-6 text-center">See It in Action</h2>
{{< /hextra/hero-section >}}

{{< tabs items="Schema,C++ Code,Output" >}}

  {{< tab >}}
  ```json
  {
    "name": "greet",
    "description": "A friendly greeting CLI",
    "options": [
      {
        "name": "name",
        "type": "string",
        "description": "Name to greet",
        "required": true
      },
      {
        "name": "count",
        "type": "integer",
        "description": "Number of times to greet",
        "default": 1
      }
    ]
  }
  ```
  {{< /tab >}}

  {{< tab >}}
  ```cpp
  #include <json_commander/json_commander.hpp>
  #include <iostream>

  int main(int argc, char* argv[]) {
    auto cli = json_commander::from_schema("greet.json");
    auto args = cli.parse(argc, argv);

    auto name = args.get<std::string>("name");
    auto count = args.get<int>("count");

    for (int i = 0; i < count; ++i) {
      std::cout << "Hello, " << name << "!\n";
    }
  }
  ```
  {{< /tab >}}

  {{< tab >}}
  ```sh
  $ ./greet --name World --count 3
  Hello, World!
  Hello, World!
  Hello, World!

  $ ./greet --help
  greet - A friendly greeting CLI

  Usage: greet [OPTIONS]

  Options:
    --name <string>     Name to greet (required)
    --count <integer>   Number of times to greet (default: 1)
    --help              Show this help message
  ```
  {{< /tab >}}

{{< /tabs >}}

{{< hextra/feature-grid >}}

  {{< hextra/feature-card
    title="Declarative CLI Definition"
    subtitle="Define your entire command-line interface in a JSON schema. No hand-written argument parsing code needed."
    icon="document-text"
  >}}

  {{< hextra/feature-card
    title="Type-Safe Parsing"
    subtitle="Arguments are automatically validated and converted to their declared types at parse time."
    icon="check-circle"
  >}}

  {{< hextra/feature-card
    title="Nested Subcommands"
    subtitle="Build complex CLI tools with arbitrarily nested subcommands, each with their own options and arguments."
    icon="collection"
  >}}

  {{< hextra/feature-card
    title="Automatic Help Generation"
    subtitle="Help text and usage messages are generated directly from your schema — always accurate, always up to date."
    icon="question-mark-circle"
  >}}

  {{< hextra/feature-card
    title="Modern C++20"
    subtitle="Built with concepts, ranges, and structured bindings. Clean, modern API that feels native to C++20."
    icon="lightning-bolt"
  >}}

  {{< hextra/feature-card
    title="Header-Only Option"
    subtitle="Use as a header-only library for easy integration, or link as a static/shared library for faster builds."
    icon="puzzle"
  >}}

{{< /hextra/feature-grid >}}
