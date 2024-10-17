---
minutes: 3
---

# `if let` expressions

The
[`if let` expression](https://doc.rust-lang.org/reference/expressions/if-expr.html#if-let-expressions)
lets you execute different code depending on whether a value matches a pattern:

```rust,editable
use std::time::Duration;

fn sleep_for(secs: f32) {
    if let Ok(dur) = Duration::try_from_secs_f32(secs) {
        std::thread::sleep(dur);
        println!("slept for {:?}", dur);
    } else {
        println!("can't sleep");
    }
}

fn main() {
    sleep_for(-10.0);
    sleep_for(0.8);
}
```

This is equivalent to a `match` with one arm that is the same as the `if let` and 
which does nothing for any other pattern:

```rust
// Long version of the above:
fn sleep_for(secs: f32) {
    match Duration::try_from_secs_f32(secs) {
        Ok(dur) => {
            std::thread::sleep(dur);
            println!("slept for {:?}", dur);
        }
        _ => {
            println!("can't sleep");
        }
    }
}
```

<details>

- Unlike `match`, `if let` does not have to cover all branches. This can make it
  more concise than `match`.
- A common usage is handling `Some` values when working with `Option`.
- Unlike `match`, `if let` does not support guard clauses for pattern matching.

</details>

