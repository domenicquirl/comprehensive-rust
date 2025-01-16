---
minutes: 3
---

# Extern Functions

It is possible to call functions written in other languages from your Rust code.
To do so, the signature of these external functions has to written out in an
`extern` block, similar to a trait definition. They may then be called through 
FFI (the Foreign Function Interface).

```rust,editable
// SAFETY: We verified that all functions have the correct signature (the same
// as in C).
unsafe extern "C" {
    // SAFETY: `abs` doesn't deal with pointers and doesn't have any safety
    // requirements.
    safe fn abs(input: i32) -> i32;
    
    /// # Safety
    /// `p` must be valid and point to a null-terminated character sequence.
    unsafe fn strlen(p: *const u8) -> usize;
}

fn main() {
    // SAFETY: `foobar` is null-terminated and valid during the call to `strlen`.
    let foobar = "foobar\0";
    println!(
        "Length of 'foobar' according to C: {}", 
        unsafe { strlen(&raw const foobar as *const u8) }
    );
    
    // No `unsafe` required here because we marked the function as `safe` above.
    println!("Absolute value of -3 according to C: {}", abs(-3));

    // UNSAFE:
    // let not_null_terminated  = "evil";
    // println!(
    //     "Length of 'evil' according to C: {}", 
    //     unsafe { strlen(&raw const not_null_terminated as *const u8) }
    // );
}
```

<details>

By default, `extern` functions are unsafe to call, because they may have 
additional preconditions that need to be upheld, but which are outside the 
purview of the Rust compiler (because they are defined in a different language).

Calling external functions is usually only a problem when those functions do 
things with pointers which might violate Rust's memory model (such as `strlen`), 
but in general any C function might have undefined behaviour under any arbitrary 
circumstances.

Note how the `extern` block itself is already `unsafe`, because you as the author
of the extern declarations are responsible for making sure the signatures are 
correct and match what is defined on the C side (see also the corresponding 
[Release announcement] from the Rust team). Note also how, because `abs` does 
not have any additional safety requirements (other than calling the correct 
C function), we marked it as `safe`, which allows it to be called from `main`
without an `unsafe` block. This is not possible for `strlen` because of the 
requirements on the string pointer.

The `"C"` in this example is the ABI;
[other ABIs are available too](https://doc.rust-lang.org/reference/items/external-blocks.html).

[Release announcement]: https://blog.rust-lang.org/2024/10/17/Rust-1.82.0.html#safe-items-with-unsafe-extern

</details>

