# TypeGo

TypeGo is a statically typed transpiler that converts `.tgo` files into standard Go (`.go`) code.

It focuses on improving type clarity, readability, and developer ergonomics while remaining fully compatible with the Go toolchain.

---

## What this project demonstrates

TypeGo is a complete language and tooling project, built end-to-end:

- Custom language syntax and semantics
- Lexer, parser, and AST processing
- Code generation targeting Go
- Command-line interface
- VSCode Language Server
- **Self-hosting**: TypeGo is written in TypeGo and transpiles its own source code

This project was built as a practical exploration of language design, compiler construction, and developer tooling.

---

## Example

### TypeGo input

```go
package main

import "fmt"

enumstruct Role {
    Admin
    Guest
    Member
}

struct Person {
    string Name
    int Age
    IntRole Role

    fn string Greet() {
        return fmt.Sprintf(
            "Hi, I'm %s, I'm %d years old, and my role is %s.",
            self.Name,
            self.Age,
            self.Role.ToString()
        )
    }
}

fn main() {

    []Person people = make(0)

    people.append(Person{ Name: "Alice", Age: 30, Role: Role.Admin })
    people.append(Person{ Name: "Bob", Age: 25, Role: Role.Member })
    people.append(Person{ Name: "Charlie", Age: 40, Role: Role.Guest })

    for i := 0; i < len(people); i++ {
        fmt.Println(people[i].Greet())
    }
}

```

Generated Go output
```go
package main

import "fmt"

type IntRole int

var Role = struct {
    Admin  IntRole
    Guest  IntRole
    Member IntRole
}{
    Admin:  0,
    Guest:  1,
    Member: 2,
}

func (self IntRole) ToString() string {
    switch self {
    case Role.Admin:
        return "Admin"
    case Role.Guest:
        return "Guest"
    case Role.Member:
        return "Member"
    default:
        return "Unknown"
    }
}

type Person struct {
    Name string
    Age  int
    Role IntRole
}

func (self *Person) Greet() string {
    return fmt.Sprintf(
        "Hi, I'm %s, I'm %d years old, and my role is %s.",
        self.Name,
        self.Age,
        self.Role.ToString(),
    )
}

func main() {

    var people []Person = make([]Person, 0)

    people = append(people, Person{Name: "Alice", Age: 30, Role: Role.Admin})
    people = append(people, Person{Name: "Bob", Age: 25, Role: Role.Member})
    people = append(people, Person{Name: "Charlie", Age: 40, Role: Role.Guest})

    for i := 0; i < len(people); i++ {
        fmt.Println(people[i].Greet())
    }
}
```

Key features

Explicit type declarations by default

C-style declaration syntax (type name = value)

Improved enum abstractions:

enum

enumstruct (scoped, non-conflicting enums)

Struct methods defined inline

Automatic generation of helper methods (e.g. ToString)

Fully compatible with existing Go projects

Incremental adoption: .tgo files are ignored by the Go compiler

CLI usage

TypeGo installs as a command-line tool:

tgo help
tgo version
tgo convertfile file.tgo
tgo convertfileabs file.tgo
tgo convertdir


convertfile converts a single file

convertdir recursively converts all .tgo files in a directory

Generated .go files integrate directly with the Go compiler

Tooling
VSCode Language Server

A VSCode extension named TypeGo is included, providing:

Syntax highlighting

Automatic .tgo → .go conversion on save

Design notes

TypeGo explores alternative approaches to type declarations, enums, and struct methods while remaining interoperable with Go.

More detailed design rationale is available in DESIGN.md.

Status

TypeGo is a complete and functional project built as an exploration of language design and compiler tooling.
