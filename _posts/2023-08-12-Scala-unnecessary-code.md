---
layout: post
title: Adventures in Scala - An Overture in Unnecessary Code
tags: [scala, software, coding]
featured: false
hidden: false
---

## Seen in the Wild

> "Under Heaven all can see beauty as beauty only because there is ugliness." <cite>― Lao Tzu ―</cite>

Alright, let's look at something I saw recently that struck me as particularly ugly.

### Bad

```scala
val someCollection = Array(1, 2, 3)
if (someCollection.length == 0) {
    List()
} else {
    someCollection.map(x => x + 1).toList()
}
```

Again, we have introduced *unecessary* control flow!
More importantly, we've completely missed the purpose of using a `map` operation.
which leads to more paths to be tested if you want to properly test.

### Good

First, let's recall the behavior of a `map` operation.

```scala
scala> val someCollection = Array.empty[Int]
val someCollection: Array[Int] = Array()

scala> someCollection.map(x => x + 1)
val res0: Array[Int] = Array()
```

Ok, so a `map` over a collection gives an empty version of that collection.
*We don't ever need to check if a collection is empty*.
We've already established the non-empty case behavior from the example above.

Let's bring everything together.

```scala
val someCollection = Seq(1, 2, 3)
someCollection.map(x => x + 1).toList()
```

Boom!
We removed all of the extra, unneeded complexity.
We made it easier to read and understand too.
Functional programming stepped in to save the day once again.
Hooray!

## In Summary

Functional programming exists to make your life easier (I swear!).
If you have the luxury of working in a language with functional paradigms such as Scala, *then it is worth your time to utilize them*.
