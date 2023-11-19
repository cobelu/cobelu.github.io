---
layout: post
title: Rust Footguns - Return `Result`
tags: [rust, software]
featured: false
hidden: false
---

## New Series

As I struggle to unlearn almost everything I've ever known about programming in order to learn Rust, I realize that others likely experienced the same issues.
I decided it would be best if I sat down and pointed out some of the issues that ended up being giant blockers for me.
A lot of this advice will be "just do it", but I hope that I can offer some advice of *why* that's the case.

## A Comparison to... \*gulp\* Go

If you've ever worked in Go, you'll recognize this paradigm:

```go
func someFunction() (string, error) {
    result, err := doSomething()
    if err != nil {
        return nil, err
    }
    return result, nil
}
```

Don't you *hate* how there's no shorthand magic for this `if err ~= nil` pattern?
We all joke that any professional Go programmer should dedicate a keyboard shortcut to this pattern.

## Let's Get Rusty

Let's write the same thing in Rust:

```rust
// Result<String> is an alias for Result<String, Error>
fn some_function() -> Result<String> {
    match do_something() {
        Ok(value) => value
        Err(e) => e
    }
}
```

Let's rewrite it again, but this time, with the `?` operator:

```rust
fn some_function() -> Result<String> {
    do_something()?
}
```

## Footgun

Suppose we want to write the function such that we return the raw value instead of the value wrapped in a `Result`.
We can't use the `?` operator or we will be faced with the following compiler error:
this function should return `Result` or `Option` to accept `?`.

```rust
fn some_function() -> String {
    do_something().expect("Could not do something")
}
```

Oh no!
We introduced the use of `expect`, which *can* throw a `panic`,
but you probably want to use Rust in order to not worry about ever panicking!
If we had returned a `Result` instead, we wouldn't have that possiblity.

## Conclusion

You will *suffer* in Rust if you write functions that return values.
*Don't* waste time unwrapping `Option`s or `Result`s.
Instead, write your functions to return `Option`s or `Result`s in order to take advantage of the `?` operator.
