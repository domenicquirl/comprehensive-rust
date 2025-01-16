---
minutes: 5
---

# Unsafe Rust

The Rust language has two parts:

- **Safe Rust:** memory safe, no undefined behavior possible.
- **Unsafe Rust:** can trigger undefined behavior if preconditions are violated.

We saw mostly safe Rust in this course, but it's important to know what Unsafe
Rust is.

Unsafe code is best used small and isolated, and its correctness should be
carefully documented. To make it easier for other people to work with your 
unsafe code, it is good practice to wrap it in a safe abstraction layer.

Unsafe Rust gives you access to five new capabilities:

- Dereference raw pointers.
- Access or modify mutable static variables.
- Access `union` fields.
- Call `unsafe` functions, including `extern` functions.
- Implement `unsafe` traits.

We will briefly cover unsafe capabilities next. For full details, please see
[Chapter 19.1 in the Rust Book](https://doc.rust-lang.org/book/ch19-01-unsafe-rust.html)
and the [Rustonomicon](https://doc.rust-lang.org/nomicon/).

<details>

Unsafe Rust does not mean the code is incorrect. It means that developers have
turned off some compiler safety features and have to write correct code by
themselves. It means the compiler no longer enforces Rust's memory-safety rules.

</details>
