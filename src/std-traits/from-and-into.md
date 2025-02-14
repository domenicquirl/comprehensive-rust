---
minutes: 5
---

# `From` and `Into`

Types implement [`From`][1] and [`Into`][2] to facilitate type conversions.
Unlike `as`, these traits correspond to lossless, infallible conversions.

```rust,editable
fn main() {
    let s = String::from("hello");
    let addr = std::net::Ipv4Addr::from([127, 0, 0, 1]);
    let one = i16::from(true);
    let bigger = i32::from(123_i16);
    println!("{s}, {addr}, {one}, {bigger}");
}
```

[`Into`][2] is automatically implemented when [`From`][1] is implemented:

```rust,editable
fn main() {
    let s: String = "hello".into();
    let addr: std::net::Ipv4Addr = [127, 0, 0, 1].into();
    let one: i16 = true.into();
    let bigger: i32 = 123_i16.into();
    println!("{s}, {addr}, {one}, {bigger}");
}
```

If it's only possible to convert some, but not all values of one type into 
another, the standard library also provides a version of these traits for
fallible conversions called [`TryFrom`][3] and [`TryInto`][4], which return
a `Result` instead.

<details>

- That's why it is common to only implement `From`, as your type will get `Into`
  implementation too.
- When declaring a function argument input type like "anything that can be
  converted into a `String`", the rule is opposite, you should use `Into`. Your
  function will accept types that implement `From` and those that _only_
  implement `Into`.

</details>

[1]: https://doc.rust-lang.org/std/convert/trait.From.html
[2]: https://doc.rust-lang.org/std/convert/trait.Into.html
[3]: https://doc.rust-lang.org/std/convert/trait.TryFrom.html
[4]: https://doc.rust-lang.org/std/convert/trait.TryInto.html
