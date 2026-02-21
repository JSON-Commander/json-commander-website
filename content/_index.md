+++
title = "JSON Commander"
toc = false
+++

{{< hextra/hero-subtitle >}}
  Define CLIs declaratively with JSON schemas.&nbsp;<br class="sm:block hidden" />
  Type-safe argument parsing, nested subcommands, and automatic help and man page generation for C++20.
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
  {{< /tab >}}

  {{< tab >}}
  ```cpp
  #include <json_commander/run.hpp>

  #include <algorithm>
  #include <cctype>
  #include <iostream>
  #include <string>

  using namespace json_commander;

  model::Root make_cli() {
    model::Flag loud;
    loud.names = {"loud", "l"};
    loud.doc = {"Print the greeting in uppercase."};

    model::Positional name;
    name.name = "name";
    name.doc = {"The name to greet."};
    name.type = model::ScalarType::String;
    name.required = true;

    model::Root root;
    root.name = "greet";
    root.doc = {"A friendly greeting tool."};
    root.version = "1.0.0";
    root.args = std::vector<model::Argument>{loud, name};
    return root;
  }

  int main(int argc, char *argv[]) {
    return json_commander::run(make_cli(), argc, argv,
      [](const nlohmann::json &config) {
        std::string greeting =
          "Hello, " + config["name"].get<std::string>() + "!";
        if (config["loud"].get<bool>()) {
          std::transform(greeting.begin(), greeting.end(),
            greeting.begin(),
            [](unsigned char c) {
              return static_cast<char>(std::toupper(c));
            });
        }
        std::cout << greeting << "\n";
        return 0;
      });
  }
  ```
  {{< /tab >}}

  {{< tab >}}
  ```sh
  $ ./greet Alice
  Hello, Alice!

  $ ./greet --loud Alice
  HELLO, ALICE!

  $ ./greet --help
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
    subtitle="Scalar types (string, int, float, bool, enum, file, dir, path) and compound types (list, pair, triple) are validated and converted at parse time."
    icon="check-circle"
  >}}

  {{< hextra/feature-card
    title="Nested Subcommands"
    subtitle="Build complex CLI tools with arbitrarily nested subcommands, each with their own options and arguments."
    icon="collection"
  >}}

  {{< hextra/feature-card
    title="Automatic Help and Man Pages"
    subtitle="Help text and groff man pages are generated directly from your schema — always accurate, always up to date."
    icon="question-mark-circle"
  >}}

  {{< hextra/feature-card
    title="Modern C++20"
    subtitle="Built with structured bindings, std::variant, and std::optional. Clean, modern API that feels native to C++20."
    icon="lightning-bolt"
  >}}

  {{< hextra/feature-card
    title="Environment and Config Support"
    subtitle="Options can fall back to environment variables when not provided on the command line. Generate JSON Schema for runtime configuration output."
    icon="puzzle"
  >}}

{{< /hextra/feature-grid >}}
