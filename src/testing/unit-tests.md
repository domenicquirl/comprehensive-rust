---
minutes: 5
---

# Unit Tests

Rust and Cargo come with a simple unit test framework. Tests are marked with
`#[test]`. Unit tests are often put in a nested `tests` module, using
`#[cfg(test)]` to conditionally compile them only when building tests.

```rust,editable,ignore
fn first_word(text: &str) -> &str {
    match text.find(' ') {
        Some(idx) => &text[..idx],
        None => &text,
    }
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_empty() {
        assert_eq!(first_word(""), "");
    }

    #[test]
    fn test_single_word() {
        assert_eq!(first_word("Hello"), "Hello");
    }

    #[test]
    fn test_multiple_words() {
        assert_eq!(first_word("Hello World"), "Hello");
    }
}
```

- Because the unit tests live in the same module as the code under test, this 
  lets you unit test private functions and access private fields of structs 
  from that module.
- The `#[cfg(test)]` attribute is only active when you run `cargo test`.

<details>

Run the tests in the playground in order to show their results.

- If you put the `tests` module in its own file (as seen in the last section),
  less code will need to be recompiled when editing a test.

</details>
