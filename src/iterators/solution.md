# Solution

```rust,editable
{{#include exercise.rs:solution}}
```

<details>

A more literal translation of the comment can be achieved by creating an 
iterator over the index `n` instead of the values themselves:

```rust
fn offset_differences<N>(offset: usize, values: Vec<N>) -> Vec<N>
where
    N: Copy + std::ops::Sub<Output = N>,
{
    (0..values.len())
        .map(|n| values[(n + offset) % values.len()] - values[n])
        .collect()
}
```

</details>
