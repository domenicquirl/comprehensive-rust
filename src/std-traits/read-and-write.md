---
minutes: 5
---

# `Read` and `Write`

Using [`Read`][1] and [`BufRead`][2], you can abstract over `u8` sources:

```rust,editable
use std::io::{BufRead, BufReader, Read, Result};

fn count_lines<R: Read>(reader: R) -> usize {
    let buf_reader = BufReader::new(reader);
    buf_reader.lines().count()
}

fn main() -> Result<()> {
    let slice: &[u8] = b"foo\nbar\nbaz\n";
    println!("lines in slice: {}", count_lines(slice));

    let file = std::fs::File::open(std::env::current_exe()?)?;
    println!("lines in file: {}", count_lines(file));
    Ok(())
}
```

Similarly, [`Write`][3] lets you abstract over `u8` sinks:

```rust,editable
use std::io::{Result, Write};

fn log<W: Write>(writer: &mut W, msg: &str) -> Result<()> {
    writer.write_all(msg.as_bytes())?;
    writer.write_all("\n".as_bytes())
}

fn main() -> Result<()> {
    let mut buffer = Vec::new();
    log(&mut buffer, "Hello")?;
    log(&mut buffer, "World")?;
    println!("Logged: {buffer:?}");
    Ok(())
}
```

<details>

- Types that implement `Read` are `File`s, standard input (e.g., from a terminal), 
  TCP connectiions, etc.

- `Write` is implemented by `File`s, standard output, and other (e.g., TCP) streams
  as well, but also for `Vec` and (differently) for `String`s.

- The [`Cursor`][4] type can be used to wrap any array of bytes and implements 
  the `Read` and `Write` traits together with the trait `Seek`, which is often
  required for `File` operations.

</details>

[1]: https://doc.rust-lang.org/std/io/trait.Read.html
[2]: https://doc.rust-lang.org/std/io/trait.BufRead.html
[3]: https://doc.rust-lang.org/std/io/trait.Write.html
[4]: https://doc.rust-lang.org/std/io/struct.Cursor.html
