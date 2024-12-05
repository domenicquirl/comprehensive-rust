---
minutes: 5
---

# Other Types of Tests

## Integration Tests

If you want to test your library as a client, use an integration test.

Create a `.rs` file under `tests/`:

```rust,ignore
// tests/my_library.rs
use my_library::init;

#[test]
fn test_init() {
    assert!(init().is_ok());
}
```

These tests only have access to the public API of your crate.

## Documentation Tests

Rust has built-in support for documentation tests: code blocks in `///` comments 
are automatically interpreted as Rust code and the contained code will be 
compiled and executed as part of `cargo test`.

````rust
/// Shortens a string to the given length.
///
/// ```
/// # use playground::shorten_string;
/// assert_eq!(shorten_string("Hello World", 5), "Hello");
/// assert_eq!(shorten_string("Hello World", 20), "Hello World");
/// ```
pub fn shorten_string(s: &str, length: usize) -> &str {
    &s[..std::cmp::min(length, s.len())]
}
````

- Adding `#` in the code will hide it from the docs, but will still compile/run
  it.
- Test the above code on the
  [Rust Playground](https://play.rust-lang.org/?version=stable&mode=debug&edition=2021&gist=3ce2ad13ea1302f6572cb15cd96becf0).
- You can apply additional attributes to the code block to make it test that 
  the code inside the block doesn't compile, or to skip running the test entirely.
