# Solution

```rust,editable
{{#include exercise.rs:solution}}
```

<details>

Alternatively to using a `for` loop to iterate over the array or indexing the 
individual elements, we could also destructure the array because we know it 
contains exactly 3 elements.

```rs
fn magnitude(vector: &[f64; 3]) -> f64 {
    let [a, b, c] = vector;
    (a*a + b*b + c*c).sqrt()
}
```

</details>