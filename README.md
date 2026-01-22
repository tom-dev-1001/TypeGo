TypeGo

TypeGo is a statically typed transpiler and tooling ecosystem that converts .tgo files into standard Go (.go) code.

It is designed to improve type clarity, readability, and developer ergonomics while remaining fully compatible with the Go toolchain.

What this project demonstrates

TypeGo is a complete language and tooling project, built end-to-end:

A custom programming language and syntax

A full transpiler pipeline (.tgo → .go)

Lexer, parser, and AST processing

Code generation targeting Go

A command-line interface

A VSCode Language Server

Self-hosting: TypeGo is written in TypeGo itself and transpiles its own source code

This project was built to explore language design, compiler construction, and developer tooling in a practical, production-style setting.

Example
TypeGo input
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

Generated Go output
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

How it works

.tgo files coexist with .go files in the same project

TypeGo transpiles .tgo files into standard Go code

Generated Go code is readable and does not require runtime dependencies

Projects can adopt TypeGo partially or fully

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

TypeGo explores alternative approaches to type declarations, enums, and struct methods while remaining practical and interoperable with Go.

A more detailed discussion of the design decisions and trade-offs can be found here:

➡ DESIGN.md

(This includes deeper rationale behind explicit typing, enum design, and syntax choices.)

Status

TypeGo is a complete and functional project, built as an exploration of language design, compiler construction, and developer tooling.

License

[Add license here]
