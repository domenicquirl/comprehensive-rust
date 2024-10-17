---
minutes: 3
---

# `while let` expressions

Similar to `if let`, there is a
[`while let`](https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-pattern-loops)
variant which repeatedly tests a value against a pattern in a loop.
The loop will keep running as long as the pattern matches:

```rust,editable
fn main() {
    let mut name = String::from("Comprehensive Rust 🦀");
    while let Some(c) = name.pop() {
        println!("character: {c}");
    }
    // (There are more efficient ways to reverse a string!)
}
```

Here
[`String::pop`](https://doc.rust-lang.org/stable/std/string/struct.String.html#method.pop)
returns `Some(c)` until the string is empty, after which it will return `None`.
The `while let` lets us keep iterating through all items.

<details>

- You could rewrite the `while let` loop as an infinite loop with an if
  statement that breaks when there is no value to unwrap for `name.pop()`. The
  `while let` provides syntactic sugar for the above scenario.

```rust
fn main() {
    let mut name = String::from("Comprehensive Rust 🦀");
    loop {
        let Some(c) = name.pop() else {
            break;
        };
        println!("character: {c}");
    }
}
```

</details>
