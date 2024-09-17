# Course Structure

> This page is for the course instructor.

## Rust Fundamentals

The first four days make up [Rust Fundamentals](../welcome-day-1.md). The days
are fast paced and we cover a lot of ground!

{{%course outline Fundamentals}}

## Deep Dives

In addition to the 4-day class on Rust Fundamentals, we cover some more
specialized topics:

### Bare-Metal Rust

The [Bare-Metal Rust](../bare-metal.md) deep dive is a full day class on using
Rust for bare-metal (embedded) development. Both microcontrollers and
application processors are covered.

For the microcontroller part, you will need to buy the
[BBC micro:bit](https://microbit.org/) v2 development board ahead of time.
Everybody will need to install a number of packages as described on the
[welcome page](../bare-metal.md).

### Concurrency in Rust

The [Concurrency in Rust](../concurrency/welcome.md) deep dive is a full day
class on classical as well as `async`/`await` concurrency.

You will need a fresh crate set up and the dependencies downloaded and ready to
go. You can then copy/paste the examples into `src/main.rs` to experiment with
them:

```shell
cargo init concurrency
cd concurrency
cargo add tokio --features full
cargo run
```

{{%course outline Concurrency}}

## Format

The course is meant to be very interactive and we recommend letting the
questions drive the exploration of Rust!
