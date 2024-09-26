---
minutes: 5
---

# Loops

There are three looping keywords in Rust: `while`, `loop`, and `for`:

## `while`

The
[`while` keyword](https://doc.rust-lang.org/reference/expressions/loop-expr.html#predicate-loops)
works much like in other languages, executing the loop body as long as the
condition is true.

```rust,editable
fn main() {
    let mut x = 200;
    while x >= 10 {
        x = x / 2;
    }
    println!("Final x: {x}");
}
```

<details>

Note that integer division [rounds towards 0](https://doc.rust-lang.org/stable/reference/expressions/operator-expr.html#arithmetic-and-logical-binary-operators).

</details>
