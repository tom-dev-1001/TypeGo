TypeGo

***

TypeGo is an experimental extension to Go that explores alternative approaches
to type declarations, enums, and struct methods while remaining fully
interoperable with the Go toolchain.

TypeGo code lives in .tgo files and is compiled into standard .go files,
allowing incremental adoption in existing Go projects.

Example:

Type input:
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

Generated Go output:
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
