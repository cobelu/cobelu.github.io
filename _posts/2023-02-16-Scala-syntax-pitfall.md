---
layout: post
title: Adventures in Scala - Pitfalls of Implicit Returns
tags: [scala, coding]
featured: false
hidden: false
---

## Nested Dangers

Although you should avoid nesting `if`s, you are sometimes forced to do so in order to get things out the door with a major rewrite, which may cause more problems to accidentally be created instead of solved.

Consider this perfectly acceptable chunk of code:

```scala
val (thing1, thing2) = {
    if (cond1) {
        7, 8
    } else {
        3, 4
    }
}
```

Suppose we need to add an extra branch to check for a new condition:

```scala
val (thing1, thing2) = {
    if (cond1) {
        if (cond2) {
            (1, 2)
        }
        val something = doSomething()
        if (something) {
            (5, 6)
        }
        (7, 8)
    } else {
        (3, 4)
    }
}
```

This change would seem intuitive to the early Scala programmer because you get hooked on ditching the `return` keyword *fast*.
This change looks inconspicuous, but there's a huge issue that's easy to miss!
Consider the behavior on the following set of inputs:

```scala
val cond1 = true
val cond2 = true
def doSomething(): Boolean = true
```

What are the values of `thing1` and `thing2`?
You may be shocked to realize after a first pass that they were `(7, 8)`?
*What happened here*?
Well, it's very easy to do!
This is a great example of what happens when we combine functional and object-oriented principles.

Let's look at this block:

```scala
if (cond2) {
    (1, 2)
}
```

This block returns `(1, 2)`, but the result is not stored into anything!
If we write a `return`, we will anger the Scala compiler, which does not want us to ever call `return` and will give us a compiler warning!
If we had simply used the `return` keyword, we would get what we intended: `(1, 2)`.

Getting rid of syntax isn't always the answer! Everything is always a balance!
