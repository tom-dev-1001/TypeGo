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
