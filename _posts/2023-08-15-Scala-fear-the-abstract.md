---
layout: post
title: Adventures in Scala - Fear the Abstract
tags: [scala, software, coding]
featured: false
hidden: false
---

## Not Everything Should be Public

This morning, I had the same problem *twice*!
That warrants a blog post, right?

One of the reasons we use Scala is because of it's interopability with Java.
We don't tend to write much Java, but we do interface with a reasonable amount of it.
That said, although APIs are accessible across languages, the patterns don't always match up cleanly.
The differences between the two can make interopability difficult at points.

One difficulty that hit me in a sudden realization:
*Java's abstract classes are very bad for public APIs*.

## Abstract Classes - The Documentation Brick Wall

The particular example I can suggest we look at is the `NettyServerBuilder` in the `grpc` library.
[The documentation (the first thing I see when I search for the name) is viewable here](https://www.javadoc.io/doc/io.grpc/grpc-netty/1.16.1/io/grpc/netty/NettyServerBuilder.html).

The specific example we should look at is the following function.

```java
// Creates a server builder configured with the given SocketAddress.
static NettyServerBuilder forAddress(SocketAddress address)
```

None of this seems unreasonable... yet.
Let's peek at the definition of `SocketAddress`.

```java
public abstract class SocketAddress
extends Object
implements Serializable
```

Ok, so we know that it is `abstract`, which means that *we cannot instantiate an instance without first extending the class*.
However, there's absolutely no details on the page about what we *can* use in it's place (what extends it).

We have two options:

1. Extend the class with our own implementation.
2. Dig through documentation to find an example.
3. Search the web for an example from someone else.

Realistically, all three of these options suck.
They are all terrible options because *the responsibility of good documentation is to make sure none of these three things have to happen*.

After a quick search, you find [this post on Stack Overflow](https://stackoverflow.com/questions/73335423/grpc-server-to-start-on-specific-ip-address) with some poor person that had to answer their own question.
You can hear Alex Trebek's voice say, "I'm sorry, but the correct answer was 'What is `InetSocketAddress`?'".

## A Tangent

I have meant for several weeks to post about my least favorite feature of Scala: `trait`s.
This concept is what I struggled with the most when I was learning Scala.
They clutter the namespace and make code difficult to navigate.
We tend to overuse traits as bloated carriers of helper functions instead of using them to logically group related things.
However, in this post they play an important purpose.
Ok, tangent over.

## How Not to Suck

Then, how do we get our API docs to "not suck"?
Take a look at an incredibly (arguably the most) common trait in Scala: `iterable`.
[The documentation (the first thing I see when I search for the name) is viewable here](https://www.scala-lang.org/api/2.12.7/scala/collection/Iterable.html).

Notice anything different between the two doc sheets?
**Scala provides a `Known Subclasses` box to give us a quick reference of commonly used things that inheret from this trait!**

Boom!
We didn't have to write meaningless code that should have been provided to us by the library's owner!
We didn't have to dig through documentation!
We didn't have to search the web for (possibly questionable) examples from Stack Overflow!
Everything we needed is there, ready for us to go!

## An Admission

I'm a little hard on Java.
[If you look at the documentation for Java's `Iterable` interface](https://docs.oracle.com/javase/8/docs/api/java/lang/Iterable.html),
then you'll realize that Java can do this as well for interfaces.

## Takeaway

Java's abstract classes are powerful tools, but this pattern is *really* starting to *show its age*.
If you're going to provide documentation with the use of an abstract class in a public api,
then you *absolutely must* provide at least one example with an implementation class.
*Better yet, use an interface.*
Still better, use Scala 😉!
At the *very least*, provide a helper function to give you a bland (minimal) instance of that thing.
If your user had to leave the IDE to figure out how to use your API, your documentation is likely lacking.
