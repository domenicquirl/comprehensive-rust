---
minutes: 3
---

# Modules

We have seen how `impl` blocks let us namespace functions to a type.

Similarly, `mod` lets us namespace types and functions:

```rust,editable
mod foo {
    pub fn do_something() {
        println!("In the foo module");
    }
}

/// Important stuff for bar-ing.
mod bar {
    pub fn do_something() {
        println!("In the bar module");
    }
}

fn main() {
    foo::do_something();
    bar::do_something();
}
```

<details>

There are 3 hierarchical levels on which code can be organized in Rust.

- _Packages_ provide functionality and include a `Cargo.toml` file that describes
  how to build a bundle of 1 or more _crates_.
- _Crates_ are a tree of _modules_, where a binary crate creates an executable and a
  library crate compiles to a library.
- _Modules_ define organization, scope, and are the focus of this section.

</details>
