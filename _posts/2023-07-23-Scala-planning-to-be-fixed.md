---
layout: post
title: Adventures in Scala - Yet Another Reason to Document
tags: [scala, software, coding]
featured: false
hidden: false
---

## TL;DR

Please, use Javadocs if you're developing in Scala.
It's already there.
It helps documentation not break.
Be a good person and use them.

## The Lowdown

### Observation 1

Scala is a (*cough*) great language (well, at least compared to a lot of other options).
You get the time-tested, battle-torn lifestyle of Java development with the baked-in goodness of functional programming.
One of my favorite things that come with it: [Javadocs](https://www.oracle.com/technical-resources/articles/java/javadoc-tool.html).
You are free to bash Javadocs as you see fit, but it ranks as one of my favorite features of Java.
The only way I can think to say it is: *it simply works*.

### Observation 2

[Unfortunately, JetBrains has a bit of a sketchy past](https://www.nytimes.com/2021/01/06/us/politics/russia-cyber-hack.html).
While [Metals](https://scalameta.org/metals/) is trying to catch up, it still has a ways to go.
Thus, IntelliJ is my favorite option for developing in Scala.
It has a ton of powerful features that make refactoring easy and quick.

### Observation 3

One thing I've noticed in the wild is something that looks like this:

```scala
case class Car {
    vin: String,
    make: String,
    model: String,
    year: Int, // model year
}
```

In summary, we're looking at a comment for member of the class.
That comment has a purpose.
If that comment were lost,
there would be a loss of understanding of what this class actually represents.
If that comment were lost,
we would not have a full understanding of how that class should be utilized.

## A Side Note

In this simplified example, the developer did not do a good job at naming things.
That's ok!
Picking good names can be *hard*!
The fact that the developer had to leave a comment is good evidence that the member should have been renamed.
Something like `modelYear` would have taken more space, but it would've removed the need for the comment.

## Bring On the "Uh-Oh"

What happens when we decide that we want to add a new field ot this class?
Suppose we introduce an `int` member called mileage.
If we have a large codebase, then we will likely use a tool such as IntelliJ to introduce that new member to all instances.
What happens we do that?
IntelliJ will overwrite the comment as it tries to format things.
Don't believe me?
Give it a shot yourself.

It's easier than you think to lose documentation,
and that can become problematic if you plan to maintain things several years down the road.

## How Could This Have Been Avoided?

The moral of the story is:
*Use a doc-comment!*
It's simple solution that addresses this problem.
If the comment had been made in the documenation comment for the class,
the language server would have left it alone.

[Ryan Marcus, who is now a professor at UPenn, wrote a wonderful article about writing comments](https://rmarcus.info/blog/2018/11/05/good-bad-comment.html) when he was involved in teaching at Brandeis.
When I had a chance to talk to him a few years ago, I brought up this article.
You should give it a read, seriously!

## New Rule

New rule: **we don't shove comments in class definitions!**
They go in the documentation comment for the class!
