---
layout: post
title: Adventures in Scala - Iterators in the Wild
tags: [scala, software, coding]
featured: false
hidden: false
---

I fell for the oldest trick in the Scala book.

## Iterators are Weird

An `Iterator` is not a collection, but rather a way to access the elements of a collection one by one [see documentation](https://docs.scala-lang.org/overviews/collections-2.13/iterators.html).

## My Mistake

One day at work I was pulling messages from a Kafka queue.
We can create an `Iterator` to pull messages from the consumer like so:

```scala
val someIterator = consumer.poll(java.time.Duration.ofMillis(100)).iterator().asScala
```

I was noticing some strange behavior.
When I tried to debug, *I noticed even stranger behavior*.
That's all I'll say for now.

## Let's Consider an Example

Let's say we want to transform elements in an iterator to produce some final result:

```scala
val someTransformedCollection = someIterator.map(someFunction).map(anotherFunction).toSeq
```

Note, at the end, we actually have a `Stream`.
Elements are lazily fetched because it's probably not a good idea to materialize this entire collection even though we've finished transforming it.
But let's say we made a ~~mistake~~ a happy, little accident along the way, and `someFunction` does not work as intended.
We don't know that the problem is in someFunction, so we wish to inspect the intermediate states, and the natural (and perfectly reasonable) first step is to *log* our results.

Let's make this example more concrete:

```scala
def someFunction(x: Int): Int = x + 1
def anotherFunction(x: Int): Int = x + 2
val someIterator = Seq(1, 2, 3, 4, 5).toIterator
```

Now, we can inspect:

```scala
val someIntermediateCollection = someIterator.map(someFunction)
println(s"someIntermediateCollection: $someIntermediateCollection")
val someTransformedCollection = someIntermediateCollection.map(anotherFunction)
println(s"someTransformedCollection: $someTransformedCollection")
```

Great!
Unfortunately, when we run this, we *actually* get something that looks like:

```
someIntermediateCollection: non-empty iterator
someTransformedCollection: non-empty iterator
```

Geez, that's not helpful.
Let's dive in some more:

```scala
val someIntermediateCollection = someIterator.map(someFunction)
println("someIntermediateCollection")
for (someThing <- someIntermediateCollection) {
    println(someThing)
}
val someTransformedCollection = someIntermediateCollection.map(anotherFunction)
println("someTransformedCollection")
for (someThing <- someIntermediateCollection) {
    println(someThing)
}
```

And once again we inspect:

```
someIntermediateCollection
2
3
4
5
6
someTransformedCollection
```

*Wait!*
Nothing printed in our second section of output!
But we know from our function definition above that we have two functions:

```
someFunction: (x: Int)Int
anotherFunction: (x: Int)Int
```

Thus, our map operations are called on an `Iterator[Int]` and produce an `Iterator[Int]`.
That is, `map` takes some `Collection[A]` and transforms it to a `Collection[B]`.
Further, for every `A` in the starting collection, we should have some corresponding `B` in the transformed collection.
So why are we receiving an empty collection?!
Simple:

> An iterator is not a collection.

Boom!
An `Iterator` can only be iterated on **once**!
It's so easy to get side tracked that we forget the fundamentals.
By trying to inspect it, we used our one and only iteration!
If we try to continue iterating on it, then nothing is left over for us to iterate on.

## Conclusion

Do NOT log iterators!
It is a waste of your time!
If you do log, and you can spare the resources, be sure to materialize the iterator before inspection.
Otherwise, you will only lead yourself down the rabbit hole. 

🐰
