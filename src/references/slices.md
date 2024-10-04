---
minutes: 10
---

# Slices

A slice gives you a view into a larger collection:

```rust,editable
fn main() {
    let mut a: [i32; 6] = [10, 20, 30, 40, 50, 60];
    println!("a: {a:?}");

    let s: &[i32] = &a[2..4];

    println!("s: {s:?}");
}
```

- Slices borrow data from the sliced type.
- Question: What happens if you modify `a[3]` right before printing `s`? What about `a[5]`?

<details>

- We create a slice by borrowing `a` and specifying the starting and ending
  indices in brackets. This "range syntax" should already be familiar from 
  learning about `for` loops.

- If the slice starts at index 0, Rust’s range syntax allows us to drop the
  starting index, meaning that `&a[0..a.len()]` and `&a[..a.len()]` are
  identical.

- The same is true for the last index, so `&a[2..a.len()]` and `&a[2..]` are
  identical.

- To easily create a slice of the full array, we can therefore use `&a[..]`.

- `s` is a reference to a slice of `i32`s. Notice that the type of `s`
  (`&[i32]`) no longer mentions the array length. This allows us to perform
  computation on slices of different sizes. Slices always know their length, 
  however, and we can retrieve the number of elements in a slice by asking 
  for its `len()`.

- Slices always borrow from another object. In this example, `a` has to remain
  'alive' (in scope) for at least as long as our slice.

- The question about modifying `a[3]` can spark an interesting discussion, but
  the answer is that for memory safety reasons you cannot do it through `a` at
  this point in the execution, but you can read the data from both `a` and `s`
  safely because `s` is a _shared_ reference. Modification works before you 
  created the slice, and again after the `println`, when the slice is no longer 
  used.

  Note how the entire array `a` is borrowed by `s`, so even an attempt to modify
  an array element outside the range of the slice is rejected by the compiler,
  even though in this case it would be safe to do.

</details>
