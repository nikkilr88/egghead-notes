# Rust

### Why use Rust?

- Fast
- Secure
- compiler doesn't allow you to write code that isn't memory safe

### Package management

Rust uses cargo as its' package manager.

- Cargo is similar to npm

- Packages are called 'crates'

### Basics

Every Rust program needs a `main` function

```rust
fn main() {
  // Your code goes here
}
```

#### Variables

In Rust, variables are immutable by default. If you want to be able to change them later on, use the `mut` keyword.'

```rust
let mut name = "John Dope";

name = "Another Name"
```

#### Printing to the console

`println!()` is the easiest way to print text to the console.

```rust
fn main() {
  println!("Hello world!");
}
```

_`print!()` can also be used. The difference is that with `print!()`, newline is not printed at the end of the message._

If you want to print a variable, use `{}` inside of the string, and pass the variable as the second parameter.

```rust
let name = "John Dope";

println!("Hello, {}", name);
```

**Additional reading:**

- [println](https://doc.rust-lang.org/std/macro.println.html)
- [print](https://doc.rust-lang.org/1.6.0/std/macro.println!.html)

### Getting user input

To be able to read user input, we first need to import the `std::io` module into our project.

```rust
use std::io
```

```rust
println!("Please enter your name:")

// Creates a new mutable string
let mut input = String::new();

// We pass a reference of input to read_line, and read_line will updated the variable with the user input
io::stdin().read_line(&input).unwrap()
```

**Additional reading:**

- [Pointers](https://doc.rust-lang.org/std/primitive.pointer.html)
- [Stdin](https://doc.rust-lang.org/std/io/struct.Stdin.html)

### Functions

Functions are declared with the `fn` keyword. Arguments are type annotated, and if the function returns a value, the return type must be specified after an arrow `->`.

```rust
fn sum(a: u32, b: u32) -> u32 {
  // Your code goes here
}
```

**Additional reading:**

- [Functions](https://doc.rust-lang.org/rust-by-example/fn.html)
- [Data types](https://doc.rust-lang.org/book/ch03-02-data-types.html)

### Pattern matching

Pattern matching allows us to evaluate an expression, and excute code based on its' value.

```rust
// If the user input is a number, we will assign its' value to `a`

// If the user input is not a number, we will print an error message

match input.trim().parse() {
  Ok(value) => {
    a = value;
  },
  Err(_err) => {
    eprintln!("Error: Not a valid number!");
  }
}
```

**Additional reading:**

- [Pattern syntax](https://doc.rust-lang.org/book/ch18-03-pattern-syntax.html)
- [Match expressions](https://doc.rust-lang.org/reference/expressions/match-expr.html)

---

### Resources

#### Official

- [Learn Rust](https://www.rust-lang.org/learn)
- [The Rust Programming Language (online book)](https://doc.rust-lang.org/book/)

#### YouTube Videos

- [Rust Crash Course | Traversy Media
  ](https://www.youtube.com/watch?v=zF34dRivLOw)
- [Rust Programming Tutorials
  | dcode](https://www.youtube.com/playlist?list=PLVvjrrRCBy2JSHf9tGxGKJ-bYAN_uDCUL)
- [All About Rust | Microsoft Developer
  ](https://www.youtube.com/watch?v=FYGS2q1bljE)
