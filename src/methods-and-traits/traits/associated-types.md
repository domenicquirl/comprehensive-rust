# Associated Types

Associated types are placeholder types which are supplied by the trait
implementation.

```rust,editable
#[derive(Debug)]
struct Meters(i32);
#[derive(Debug)]
struct MetersSquared(i32);

trait Multiply {
    type Output;
    fn multiply(&self, other: &Self) -> Self::Output;
}

impl Multiply for Meters {
    type Output = MetersSquared;
    fn multiply(&self, other: &Self) -> Self::Output {
        MetersSquared(self.0 * other.0)
    }
}

fn main() {
    println!("{:?}", Meters(10).multiply(&Meters(20)));
}
```

<details>

- Associated types are sometimes also called "output types". The key observation
  is that the implementer, not the caller, chooses this type, but it can only
  pick one.

- Many standard library traits have associated types, including arithmetic
  operators and `Iterator`.

</details>
