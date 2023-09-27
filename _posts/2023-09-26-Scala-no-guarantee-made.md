---
layout: post
title: Adventures in Scala - No Guarantees Made
tags: [scala, software, coding]
featured: false
hidden: false
---

## The Time I Got Bit By a Convincing Contract

When you write code in a strongly typed, compiled language, you're constantly making *contracts*.
*You are constantly telling the compiler that something has to be a certain way*.
When you tell the compiler that you want something to be a certain way, you *expect* that something to be that certain way.

Here's the thing:
the inclusion of `null` allows, well, a `Null Pointer Exception` (`NPE`).
As far as I'm concerned, this is the worst bug because *it is a bug that should never happen*.
An `NPE` can happen at any time on any thing in Scala even though the language has baked-in functional programming features.
The possibility of sudden, unexpected failure is always there, lurking in the shadows.

I recently was bit an `NPE` of my own fault.
Let's walk through what happened.

## What Happened?

Suppose I want some cache to store an `Option[A]` with a `String` for a key.
I can define a Guava cache in Scala like so.

```scala
import com.google.common.cache.CacheLoader

class SomeCacheLoader extends CacheLoader[String, Option[String]] {
  override def load(key: String): A = {
    Some(s"Loaded key: $key")
  }
}
```

Now, let's initizialize an instance of the loading cache.

```scala
import com.google.common.cache.{CacheBuilder, LoadingCache}

val someLoadingCache: LoadingCache[String, Option[String]] = CacheBuilder.newBuilder()
  .maximumSize(10)
  .build(new MyCacheLoader())
```

Here's where things go to "hell in a handbasket".
Let's attempt to retrieve an item from the empty cache.

```scala
val someKey = "Some Key"
val someValueFromCache = loadingCache.get(someKey)
```

### Sanity Check

What's the value of `someValueFromCache`?
Is it `None` or `null`?
It seems perfectly reasonable upon a quick glance that it is `None` because the return type of `get` is an `Option`.
Unfortunately, it's actually a dreaded `null`!

However, our return type of `get` is `T` because *this is a Java function*.
**We used a Java function in Scala, and it's very easy to forget this**!

Our *contract* says that the returned value will be of type `Option[String]`.
A `get` on a Scala map for some map `S -> T` returns an `Option[T]`.
Since the `T` in this example is an `Option[String]`, we would expect to see an `Option[Option[String]]` as the for the type of `someValueFromCache`.
*It's perfectly reasonable for anyone to look at this code snippet quickly and think that nothing is wrong*.

## How Could This Have Been Prevented?

We had two solutions to avoid this:

1. Use `getOrElse` on the cache with `None` specified as the default. This is my preferred solution because it avoids flattening.
2. Cast the result of the lookup to an `Option` (and be forced to flatten it).

Both of these solutions are perfectly accessible.
Yet, if we don't utilize them, *we will have code that looks like it works but is actually dangerously broken*.
**Now, that's spooky** 👻!

## Takeaway

The safest way to not have a `Null Pointer Exception` is to use a language in which `null` does not exist.
Remember: just because the return type is an `Option`, there is *still a possibility of a Java function returning `null`, and you absolutely must account for it*!
There may be a contract, but `null` makes all contracts *null and void*.
