TypeGo

TypeGo is an experimental extension to Go that explores alternative approaches
to type declarations, enums, and struct methods while remaining fully
interoperable with the Go toolchain.

TypeGo code lives in .tgo files and is compiled into standard .go files,
allowing incremental adoption in existing Go projects.


KEY FEATURES

- Explicit type declarations by default
- C-style declaration syntax (type name = value)
- Improved enum abstractions:
  - enum
  - enumstruct (scoped, non-conflicting enums)
- Struct methods defined inline with the struct definition
- Automatic generation of helper methods (e.g. ToString)
- Fully compatible with existing Go projects
- Incremental adoption: .tgo files are ignored by the Go compiler


CLI USAGE

TypeGo installs as a command-line tool named "tgo".

Commands:

tgo help
tgo version
tgo convertfile file.tgo
tgo convertfileabs file.tgo
tgo convertdir

Command descriptions:

convertfile
Converts a single .tgo file into a .go file.

convertfileabs
Converts a single .tgo file using an absolute path.

convertdir
Recursively converts all .tgo files in a directory.

Generated .go files integrate directly with the standard Go compiler.


TOOLING

VS Code Extension

TypeGo includes a VS Code extension that provides:
- Syntax highlighting for .tgo files
- Automatic .tgo to .go conversion on save
- Language Server support


DESIGN NOTES

TypeGo is an exploration of language and tooling design rather than a proposal
to replace Go.

The project focuses on:
- Improving readability of type-heavy code
- Reducing enum-related boilerplate
- Experimenting with alternative struct and method syntax
- Maintaining strict compatibility with Go output

More detailed design rationale can be found in DESIGN.md.


STATUS

TypeGo is a complete and functional project built as an exploration of language
design, compiler construction, and developer tooling.
