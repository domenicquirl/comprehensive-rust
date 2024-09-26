---
minutes: 5
---

# Variables

Rust provides type safety via static typing. Variable bindings are made with
`let`:

```rust,editable
fn main() {
    let x: i32 = 10;
    println!("x: {x}");
    // x = 20;
    // println!("x: {x}");
}
```

<details>

- Uncomment the `x = 20` to demonstrate that variables are immutable by default.
  Before adding the `mut` keyword to allow changes, make sure to point out that 
  the error message already suggests this and that Rust's compiler messages are
  in general very good and almost always worth reading because they will help 
  you out.

- The `i32` here is the type of the variable. This must be known at compile
  time, but type inference (covered later) allows the programmer to omit it in
  many cases.

</details>
