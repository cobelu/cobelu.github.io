---
layout: post
title: Pitfalls in Go - That Darn Var
tags: [go, software, coding]
featured: false
hidden: false
---

Var leaves scars.

## New Series

I've previously written about my Adventures in Scala as I completely changed my worldview on what makes for a "good" language.
I've also lightly written about modifying that view more as I discussed Footguns in Rust.
These were mistakes that I made because I struggled to adapt to the paradigm that Rust provides, but I was all-the-more better for it in the end.
Now, as my professional work is moving from Scala to Go, I plan to write about some bugs in the wild I encounter, so we can learn from them.

As you may know, I am not fond of Golang.
Many of these mistakes I feel are brought by the language itself,
which is why this series is called "Pitfalls in Go".
If you're reading this and have made similar (or even the same) mistakes,
*it's not your fault*.
As they say, "it's a poor carpenter who blames his tools".
However, if you rip off the safety equipment from your table saw and inadvertently cut off a finger... well, you probably had that coming.
This is programming in Go.

## My Mistake

Let's look at some sample code:

```go
func doSomething(thing *Thing) (*blah.someType, error) {
	result, err := thing.anotherThing.someAction() // anotherThing is a pointer

	if err != nil {
		return nil, err
	}
	return result, nil
}
```

This code looks perfectly reasonable, which is why it's so dangerous.
If `anotherThing` is `nil`, then this function call will panic.
Worse, if `thing` is `nil`, then you will also panic.
This sounds like a "duh" statement, but I'm willing to bet if you've never been bitten by this before, then you probably glossed over this realization.
It's very easy to check if the last thing is not `nil`.
*It's very easy* to forget to check if the first thing is not `nil`.

This is now a giant red flag 🚩 for me when I review code.
Code should be structured to try to avoid this pattern if at all possible.

## My Neighbor's Mistake

My office neighbor pinged me the next day and said they had a strange segfault.
The first thing I noticed was something like this:

```go
func someFunc (*some.GrossPointer, error) {
	var somePointer *some.GrossPointer
	/// <Some Logic>
	/// ...
	return somePointer, nil
}
```

You should *always* try to use short assignment (`:=`) as often as possible in Golang.
It's there for a reason.
As an exercise, try to assign `nil` to a pointer using short-assignment. 🏋️

A `var` declaration of a native type will allocate and assign a sentinel value to that binding.
Some examples are:

```go
var someInt int // 0
var someString string // ""
var someBool bool // false
var waitGroup sync.WaitGroup // allocated WaitGroup
```

This is fine and dandy, but we might have a real problem on our hands when we declare a pointer with `var` because it defaults to a value of `nil`.
If there is some code path that allows the binding to not be set to a non-`nil` value (which is incredibly easy to accidentally do since Go is built on side-effects), then we *will* be bit by an NPE bug at some point.

A returned tuple of a `nil` pointer and a `nil` error fundamentally breaks the `Result` pattern.
Your call was either successful, or it was not.
If it was successful, then there is no error.
If it was a failure, then there is an error.
Because of this implied covenant, the user of your API is likely much more adept at writing `if err != nil` than `if returnedThing == nil`.

That's why I no longer allow a `var` declaration of a pointer through code review unless there's a *really* good reason.

## Conclusion

Pointers are a necessary way of life in Go, but you'll be much happier if you strive to not initialize with `nil`.
