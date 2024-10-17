---
minutes: 3
---

# `let else` expressions

A common case in which one might use `if let` is to check if a value matches some 
pattern and immediately return from the function if it doesn't: 

```rust,editable
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    if let Some(s) = maybe_string {
        if let Some(first_byte_char) = s.chars().next() {
            if let Some(digit) = first_byte_char.to_digit(16) {
                Ok(digit)
            } else {
                return Err(String::from("not a hex digit"));
            }
        } else {
            return Err(String::from("got empty string"));
        }
    } else {
        return Err(String::from("got None"));
    }
}

fn main() {
    println!("result: {:?}", hex_or_die_trying(Some(String::from("foo"))));
}
```

There is a variant of `if let` statements called 
[`let else`](https://doc.rust-lang.org/rust-by-example/flow_control/let_else.html)
which lets you flatten the function and write it without the deep nesting. If the pattern 
of a `let else` matches, the values _inside_ the pattern will be available in 
the surrounding scope (the function body). In a `let else` statement, the "else" 
case must diverge (`return`, `break`, or panic - anything that doesn't force the 
function to continue without the matched value). 

<details>

`if-let`s can pile up, as shown. The `let-else` construct supports flattening
this nested code. Rewrite the awkward version for students, so they can see the
transformation.

The rewritten version is:

```rust
fn hex_or_die_trying(maybe_string: Option<String>) -> Result<u32, String> {
    let Some(s) = maybe_string else {
        return Err(String::from("got None"));
    };
    let Some(first_byte_char) = s.chars().next() else {
        return Err(String::from("got empty string"));
    };
    let Some(digit) = first_byte_char.to_digit(16) else {
        return Err(String::from("not a hex digit"));
    };

    return Ok(digit);
}
```

Point out that `let else` requires a semicolon after the closing brace, same as
a regular `let` statement.

</details>

