# KiwiStudio
[![Feature Requests](https://img.shields.io/github/issues/microsoft/vscode/feature-request.svg)](https://github.com/microsoft/vscode/issues?q=is%3Aopen+is%3Aissue+label%3Afeature-request+sort%3Areactions-%2B1-desc)
[![Bugs](https://img.shields.io/github/issues/microsoft/vscode/bug.svg)](https://github.com/microsoft/vscode/issues?utf8=✓&q=is%3Aissue+is%3Aopen+label%3Abug)

## About KiwiStudio

KiwiStudio is a powerful, customizable open-source code editor built on top of the VS Code codebase foundation.

KiwiStudio combines the simplicity of a code editor with what developers need for their core edit-build-debug cycle. It provides comprehensive code editing, navigation, and understanding support along with lightweight debugging, a rich extensibility model, and lightweight integration with existing tools.

## Building KiwiStudio

For detailed, step-by-step instructions on how to build KiwiStudio into runnable executables (`.exe`), macOS applications (`.app`, `.dmg`), and Linux packages (`.tar.gz`, `.deb`, `.rpm`, `.snap`), please see [BUILD.md](BUILD.md).

## Contributing

There are many ways in which you can participate in this project, for example:

* Submit bugs and feature requests, and help us verify them as they are checked in
* Review source code changes
* Review the documentation and make pull requests for anything from typos to new content.

## Bundled Extensions

KiwiStudio includes a set of built-in extensions located in the [extensions](extensions) folder, including grammars and snippets for many languages. Extensions that provide rich language support (inline suggestions, Go to Definition) for a language have the suffix `language-features`.

## Development Container

This repository includes a Dev Containers / GitHub Codespaces development container.

Docker / the Codespace should have at least **4 cores and 6 GB of RAM (8 GB recommended)** to run a full build. See the [development container README](.devcontainer/README.md) for more information.

## License

Licensed under the [MIT](LICENSE.txt) license.
