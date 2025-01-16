---
minutes: 2
---

# Unsafe Functions

A function or method can be marked `unsafe` if it has extra preconditions you
must uphold to avoid undefined behaviour. There are many `unsafe` functions in
the standard library that require you to have checked these conditions yourself
if you want to use them.

```rust,editable
fn main() {
    let emojis = "🗻∈🌏";

    // SAFETY: The indices are in the correct order, within the bounds of the
    // string slice, and lie on UTF-8 sequence boundaries.
    unsafe {
        println!("emoji: {}", emojis.get_unchecked(0..4));
        println!("emoji: {}", emojis.get_unchecked(4..7));
        println!("emoji: {}", emojis.get_unchecked(7..11));
    }

    println!("chars: {}", count_chars(unsafe { emojis.get_unchecked(0..7) }));

    // Not upholding the UTF-8 encoding requirement breaks memory safety!
    // println!("emoji: {}", unsafe { emojis.get_unchecked(0..3) });
    // println!("chars: {}", count_chars(unsafe { emojis.get_unchecked(0..3) }));
}

fn count_chars(s: &str) -> usize {
    s.chars().count()
}
```

<details>

[`get_unchecked`], like most `_unchecked` functions, is unsafe because it can
create UB if the given range is incorrect. 

[`get_unchecked`]: https://doc.rust-lang.org/std/primitive.str.html#method.get_unchecked

</details>
