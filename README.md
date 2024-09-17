**This repository is forked from [Comprehensive Rust by Google](https://github.com/google/comprehensive-rust) for my Rust course. Many thanks to the original authors 🥰**

# Comprehensive Rust 🦀

This repository has the source code for Comprehensive Rust 🦀, a multi-day Rust
course developed by the Android team. The course covers all aspects of Rust,
from basic syntax to generics and error handling. It also includes deep dives on
bare-metal and concurrency.

## Course Format and Target Audience

The course is used internally at Google when teaching Rust to experienced
software engineers. They typically have a background in C++ or Java.

The course is taught in a classroom setting and we hope it will be useful for
others who want to teach Rust to their team. The course will be less useful for
self-study since you miss out on the discussions happening in the classroom. You
don't see the questions and answers and you don't see the compiler errors we
trigger when going through the code samples. We hope to improve on this via
[speaker notes](https://github.com/google/comprehensive-rust/issues/53) and by
[publishing videos](https://github.com/google/comprehensive-rust/issues/52).

## Building

The course is built using a few tools:

- [mdbook](https://github.com/rust-lang/mdBook)
- [mdbook-svgbob](https://github.com/boozook/mdbook-svgbob)
- [mdbook-exerciser](mdbook-exerciser/)
- [mdbook-course](mdbook-course/)

In addition,
[mdbook-linkcheck](https://github.com/Michael-F-Bryan/mdbook-linkcheck) checks
the internal links.

First install Rust by following the instructions on https://rustup.rs/. Then
clone this repository:

```shell
git clone https://github.com/google/comprehensive-rust/
cd comprehensive-rust
```

Then install these tools with:

```shell
cargo install mdbook
cargo install --locked mdbook-svgbob
cargo install --locked mdbook-linkcheck
cargo install --locked --path mdbook-exerciser
cargo install --locked --path mdbook-course
```

Run

```shell
mdbook test
```

to test all included Rust snippets. Run

```shell
mdbook serve
```

to start a web server with the course. You'll find the content on
<http://localhost:3000>. You can use `mdbook build` to create a static version
of the course in the `book/` directory. Note that you have to separately build
and zip exercises and add them to `book/html`.

> **Note** On Windows, you need to enable symlinks
> (`git config --global core.symlinks true`) and Developer Mode.

