---
minutes: 10
---

# Borrow Checking

Rust's _borrow checker_ puts constraints on the ways you can borrow values. For
a given value, at any time:

- You can have one or more shared references to the value, _or_
- You can have exactly one exclusive reference to the value.

<!-- mdbook-xgettext: skip -->

```rust,editable,compile_fail
fn main() {
    let mut a: i32 = 10;
    let b: &i32 = &a;

    {
        let c: &mut i32 = &mut a;
        *c = 20;
    }

    println!("a: {a}");
    println!("b: {b}");
}
```

The following visualization (from [Rufflewind](https://rufflewind.com/2017-02-15/rust-move-copy-borrow)) 
shows how one might think about the different ways to move, copy, or borrow a value.

<div style="background-color: white">

![Visualization](rust-move-copy-borrow.svg)

</div>

<details>

- Note that the requirement is that conflicting references not _exist_ at the
  same point. It does not matter where the reference is dereferenced.
- The above code does not compile because `a` is borrowed as mutable (through
  `c`) and as immutable (through `b`) at the same time.
- Move the `println!` statement for `b` before the scope that introduces `c` to
  make the code compile.
- After that change, the compiler realizes that `b` is only ever used before the
  new mutable borrow of `a` through `c`, even though the variable is in scope
  until the end of `main`. This is a feature of the borrow checker called 
  "non-lexical lifetimes".
- The exclusive reference constraint is quite strong. Rust uses it to ensure
  that data races do not occur. Rust also _relies_ on this constraint to
  optimize code. For example, a value behind a shared reference can be safely
  cached in a register for the lifetime of that reference.
- Check out the [Flowistry](https://github.com/willcrichton/flowistry/) VS Code
  plugin, which uses the information obtained during borrow checking to highlight
  which parts of a function are influenced by a particular argument.
- The borrow checker is designed to accommodate many common patterns, such as
  taking exclusive references to different fields in a struct at the same time.
  But, there are some situations where it doesn't quite "get it" and this often
  results in "fighting with the borrow checker."

</details>
