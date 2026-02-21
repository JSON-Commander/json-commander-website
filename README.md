# JSON Commander Website

Documentation website for [JSON Commander](https://github.com/JSON-Commander/json-commander), built with [Hugo](https://gohugo.io/) and the [Hextra](https://github.com/imfing/hextra) theme.

Live at: https://json-commander.github.io/

## Prerequisites

- [Hugo](https://gohugo.io/) (extended edition) v0.155+
- [Go](https://go.dev/) 1.23+

If you use [Nix](https://nixos.org/), both are provided automatically:

```sh
nix develop       # or let direnv handle it via .envrc
```

## Local Development

Start the Hugo dev server:

```sh
hugo server
```

This serves the site at http://localhost:1313 with live reload — edits to
content and templates are reflected immediately.

## Project Structure

```
content/                 Markdown pages (Hugo content)
  _index.md              Homepage
  about.md               About page
  docs/                  Documentation section
    _index.md            Docs hub
    getting-started/     Getting started guide
layouts/                 Custom Hugo template overrides
static/                  Static assets (favicon, etc.)
hugo.toml                Hugo configuration
flake.nix                Nix dev shell (Hugo + Go)
.github/workflows/       CI/CD (deploy to GitHub Pages)
```

## Content Editing

Pages are written in Markdown with TOML front matter (`+++`). The site uses
Hextra shortcodes for UI components — see the
[Hextra docs](https://imfing.github.io/hextra/) for available shortcodes
(`tabs`, `cards`, `feature-grid`, etc.).

Content in this site documents the JSON Commander C++ library. When the
library's public API changes, the website content should be updated to match.

## Production Build

```sh
hugo --minify
```

Output goes to `public/`.

## Deployment

Deployment is triggered manually via the `workflow_dispatch` GitHub Action. It
builds the site and pushes the output to the
[json-commander.github.io](https://github.com/JSON-Commander/json-commander.github.io)
repository.
