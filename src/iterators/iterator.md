---
minutes: 5
---

# `Iterator`

The [`Iterator`][1] trait supports iterating over values in a collection. It
requires you to implement a `next` method that yields the next iterator value
and in exchange provides lots of useful methods to customize using the iterator. 
Many standard library types implement `Iterator`, and you can implement it 
yourself, too:

```rust,editable
struct Fibonacci {
    curr: u32,
    next: u32,
}

impl Iterator for Fibonacci {
    type Item = u32;

    fn next(&mut self) -> Option<Self::Item> {
        let new_next = self.curr + self.next;
        self.curr = self.next;
        self.next = new_next;
        Some(self.curr)
    }
}

fn main() {
    let fib = Fibonacci { curr: 0, next: 1 };
    for (i, n) in fib.enumerate().take(5) {
        println!("fib({i}): {n}");
    }
}
```

<details>

- Note how the implementation of the `Iterator` trait starts with `type Item = u32`,
  which determines the data type of what's inside the iterator by specifying a
  value for the `Iterator` trait's _associated type_ parameter.

- The `Iterator` trait implements many common functional programming operations
  over collections (e.g. `map`, `filter`, `reduce`, etc). This is the trait
  where you can find all the documentation about them. In Rust these functions
  should produce the code as efficient as equivalent imperative implementations.

</details>

[1]: https://doc.rust-lang.org/std/iter/trait.Iterator.html
