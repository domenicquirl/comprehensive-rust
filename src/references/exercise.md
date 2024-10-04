---
minutes: 15
---

# Exercise: Geometry

We will create a few utility functions for 3-dimensional geometry, representing
a point as `[f64;3]`. It is up to you to determine the function signatures.

```rust,compile_fail
// Calculate the magnitude of a vector by summing the squares of 
// its coordinates and taking the square root. Use the `sqrt()` 
// method on floats to calculate their square root, like `v.sqrt()`.

fn magnitude(...) -> f64 {
    todo!()
}

// Normalize a vector by calculating its magnitude and dividing 
// all of its coordinates by that magnitude.

fn normalize(...) {
    todo!()
}

// Use the following `main` to test your work.

{{#include exercise.rs:main}}
```
