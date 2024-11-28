---
minutes: 10
---

# Lifetime Annotations

Every Rust reference is associated with a _lifetime_, which is the part of the 
program where the reference is valid and can be safely used to access the 
underlying value.

A reference must not "outlive" the value it refers to (otherwise you could have
use-after-free errors when dereferencing the reference). This is verified by the 
borrow checker.

Often, the lifetime of a reference doesn't need to be named and can be 
implicit - this is what we have seen so far. But lifetimes can also be 
explicitly annotated: `&'a Point`, `&'document str`. Lifetime names start 
with `'` and `'a` is a typical default name. Read `&'a Point` as "a borrowed 
`Point` which is valid for at least the lifetime `a`".

The exact value of lifetimes is always inferred by the compiler: you cannot 
assign to a lifetime yourself. Explicit lifetime annotations create constraints 
where there is ambiguity; the compiler verifies that there is a valid solution.

Lifetimes become more complicated when considering passing values to and
returning values from functions.

<!-- The multi-line formatting by rustfmt in left_most is apparently
     intentional: https://github.com/rust-lang/rustfmt/issues/1908 -->

```rust,editable,compile_fail
#[derive(Debug)]
struct Point(i32, i32);

fn left_most(p1: &Point, p2: &Point) -> &Point {
    if p1.0 < p2.0 {
        p1
    } else {
        p2
    }
}

fn main() {
    let p1: Point = Point(10, 10);
    let p2: Point = Point(20, 20);
    let p3 = left_most(&p1, &p2); // What is the lifetime of p3?
    println!("p3: {p3:?}");
}
```

<details>

In this example, the compiler does not know what lifetime to infer for `p3`.
Looking inside the function body shows that it can only safely assume that
`p3`'s lifetime is the shorter of `p1` and `p2`. But just like types, Rust
requires explicit annotations of lifetimes on function arguments and return
values.

Add `'a` appropriately to `left_most` and note how it is introduced with the 
same syntax as generic parameters:

```rust,ignore
fn left_most<'a>(p1: &'a Point, p2: &'a Point) -> &'a Point {
```

This says, "given p1 and p2 which are both valid for at least `'a`, the return 
value is also valid for at least `'a`. Because the function is generic over `'a`,
the code will compile for any two references you pass in.

In common cases, lifetimes can be elided, as described on the next slide.

</details>
