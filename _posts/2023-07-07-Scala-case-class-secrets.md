---
layout: post
title: Adventures in Scala - Case Class Secrets
tags: [scala, coding]
featured: false
hidden: false
---

## Afraid of Your Own Reflection

Scala has some awesome superpowers with `reflection`.
Yes, Scala can inspect itself ([you should read more here](https://docs.scala-lang.org/overviews/reflection/overview.html)), and it's incredibly useful in certain situations!
Unfortunately, use of reflection can incur a noticeable overhead.
In addition, there's a pretty steep learning curve.

Let's consider one situation when you might consider using reflection:
Having a class instance represent a row to be written to a CSV.
In this case our objective is to iterate over since we will later convert the values to strings.
One way to approach this is to use reflection to figure out what the fields are:

```scala
import scala.reflect.runtime.universe.{runtimeMirror, termNames, typeOf}

case class SomeClassClass(someField: Int, anotherField: String, yetAnotherField: Boolean)

object Main extends App {

    val someInstance = SomeClassClass(42, "Hello", true)
    val mirror = runtimeMirror(getClass.getClassLoader)
    val someClassType = typeOf[SomeClassClass]
    val constructorSymbol = someClassType.decl(termNames.CONSTRUCTOR).asMethod
    val instanceMirror = mirror.reflect(someInstance)
    val objMirror = instanceMirror.reflectConstructor(constructorSymbol)()

    someClassType.members.foreach { member =>
      if (member.isTerm && member.asTerm.isVal) {
        val fieldMirror = objMirror.reflectField(member.asTerm)
        val fieldValue = fieldMirror.get

          println(s"Field Value: $fieldValue")
        }
    }
}
```

## Introducing... Product

Did you know that a Scala `case class` inherits from `Product` ([see the doc page here](https://www.scala-lang.org/api/2.12.9/scala/Product.html))?

This doesn't seem particularly special upon first glance.
However, it can help us a lot!
Let's look at an example:

```scala
case class SomeClassClass(someField: Int, anotherField: String, yetAnotherField: Boolean)

object Main extends App {
    val someInstance = SomeClassClass(42, "Hello", true)

    val fields = someInstance.productIterator.foreach { fieldValue =>
        println(s"Field Value: $fieldValue")
    }
}
```

Wow!
We just removed *a ton* of code to accomplish the same thing!

## Gimme the Deets

Our primary discovery is the `productIterator` function.
Let's peek at [its definition](https://www.scala-lang.org/api/2.12.9/scala/Product.html):

```scala
trait Product {
    // ...
    def productIterator: Iterator[Any]
    // ...
}
```

`Any` is *very* generic for a return type.
If we needed to consider the type, we could use a `match` statement in order to guarantee that we treat it appropriately.

## All Together, Now

We're almost finished (I promise)!
Our final takeaway is putting everything together.
Luckily, Scala is super powerful at string interpolation.
Let's look at how string interpolation can be used as we generate a row for a CSV file from a Scala-backed representation:

```scala
case class SomeRowInDatabase(someField: Int, anotherField: String, yetAnotherField: Boolean)

object Main extends App {
    val someInstance = SomeRowInDatabase(42, "Hello", true)

    val fieldsAsCsvRow = someInstance.productIterator.map(x => s"${x}").mkString(",")
}
```

For all intensive purposes, we have reduced the lines needed to accomplish our task from *several* to *only one*!
Huzzah!

## Final Takeaways

* Reflection is powerful but not always intuitive or lightweight.
* The `Product` trait has a nifty function called `productIterator`.
* Case classes inherit from `Product`.
* If you need to reuse data (e.g., a test), then take advantage of your lagnuage's amazing typing features.
* It's preferable to convert from real types to strings than the other way around.
* Scala Case Classes are *super* powerful! Use them as often as you can!
