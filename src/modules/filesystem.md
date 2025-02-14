---
minutes: 5
---

# Filesystem Hierarchy

Omitting the module content will tell Rust to look for it in another file:

```rust,editable,compile_fail
mod garden;
```

This tells Rust that the `garden` module content is found at `src/garden.rs`.
Similarly, a `garden::vegetables` module can be found at
`src/garden/vegetables.rs`. If the `garden` module contains multiple modules / 
files itself, the source file for the `garden` module can alternatively be
placed under `src/garden/mod.rs` next to the submodules of the `garden` module.

The `crate` root is in:

- `src/lib.rs` (for a library crate)
- `src/main.rs` (for a binary crate)

Modules defined in files can be documented, too, using "inner doc comments".
These document the item that contains them -- in this case, a module.

```rust,editable,compile_fail
//! This module implements the garden, including a highly performant germination
//! implementation.

// Re-export types from this module.
pub use garden::Garden;
pub use seeds::SeedPacket;

/// Sow the given seed packets.
pub fn sow(seeds: Vec<SeedPacket>) {
    todo!()
}

/// Harvest the produce in the garden that is ready.
pub fn harvest(garden: &mut Garden) {
    todo!()
}
```

<details>

- Before Rust 2018, the compiler only supported `module/mod.rs` instead of `module.rs`.

- The main reason to introduce `filename.rs` as alternative to `filename/mod.rs`
  was because many files named `mod.rs` can be hard to distinguish in IDEs. Some
  IDEs provide settings to customize how tabs for these files are shown, e.g.
  [VS Code](https://code.visualstudio.com/updates/v1_88#_custom-labels-for-open-editors).

- Deeper nesting can use folders, even if the main module is a file:

  ```ignore
  src/
  ├── main.rs
  ├── top_module.rs
  └── top_module/
      └── sub_module.rs
  ```

- The place rust will look for modules can be changed with a compiler directive:

  ```rust,ignore
  #[path = "some/path.rs"]
  mod some_module;
  ```

  This is useful, for example, if you would like to place tests for a module in
  a file named `some_module_test.rs`, similar to the convention in Go.

</details>
