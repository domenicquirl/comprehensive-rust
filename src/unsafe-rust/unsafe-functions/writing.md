---
minutes: 3
---

# Writing Unsafe Functions

You can mark your own functions as `unsafe` if they require particular
conditions to avoid undefined behaviour.

```rust,editable
/// Swaps the values pointed to by the given pointers.
///
/// # Safety
///
/// The pointers must be valid and properly aligned.
unsafe fn swap(a: *mut u8, b: *mut u8) {
    let temp = *a;
    *a = *b;
    *b = temp;
}

fn main() {
    let mut a = 42;
    let mut b = 66;

    // SAFETY: ...
    unsafe {
        swap(&mut a, &mut b);
    }

    println!("a = {a}, b = {b}");
}
```

<details>

We wouldn't actually use pointers for a `swap` function - it can be done safely
with references.

Note that unsafe code is allowed within an unsafe function without an `unsafe`
block. We can prohibit this with `#[deny(unsafe_op_in_unsafe_fn)]`. Try adding
it and see what happens. This will likely change in a future Rust edition.

</details>
