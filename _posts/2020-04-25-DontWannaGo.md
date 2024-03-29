---
layout: post
title: I Don't Wanna Go!
tags: [programming, rant]
featured_image_thumbnail: Gopher
featured_image: assets/images/posts/2020/04/gopher.jpg
featured: false
hidden: false
---

I've been using the Go programming language for my graduate distributed systems course. 
Despite the hype I've heard for Golang, using it has not been the highlight of my semester.
I'd like to share why I have come to be weary of this beloved language.

## It's Not Polite to Point

Consider a struct reference in C.
Suppose we have a `Cat` struct.

```c
struct Cat {
    int lives;
};
```

We can access the cat's field `doesPurr` by using the `.` operator.

```c
int main() { 
    struct Cat kitty;
    kitty.lives = 9;
}
```

If we have a reference to cat, we can access the cat's field variable one of two ways.
We can derefence the reference and modify the field, or we can access the field with the `->` operator.
Both accomplish the same goal, and both are shown below.

```c
int main() {
    struct Cat *kittyPtr = &kitty;
    (*kittyPtr).lives = 8; // The tradition
    kittyPtr->lives = 7; // The "syntactic sugar"
}
```

Although C can be somewhat archaic,
it is *explicitly* clear if we are dealing with either a cat or a *reference to* a cat.
[The full code can be viewed here if desired](https://repl.it/repls/NervousGrossCrypto).

Now, let's consider the same idea in Go.
Similarly, we define a `Cat` struct.
Again, we can use the `.` operator to access and set a field.

```go
package main

import "fmt"

type Cat struct {
    lives int
}

func main() {
    kitty := Cat{}
    kitty.lives = 9
}
```

We can still get a reference to our cat.

```go
...

func main() {
    kitty := Cat{}
    kittyPtr := &kitty
}
```

Nothing seems wrong... yet.
What happens if we want to change the cat's number of lives?
That snippet of code would be as follows.

```go
...

func main() {
    kitty := Cat{}
    kitty.lives = 9 // Access by .
    kittyPtr := &kitty
    kittyPtr.lives = 9 // Access by .
}
```

Whoa there, tiger!
Go does not make a syntactic distinction between the `Cat` and the `*Cat`.
However, the `Cat` posseses the `lives` field,
while the `*Cat` is a pointer to the `Cat` which contains the `lives` field.
There is a **huge** difference between the two.
*This corner-cutting feature drives me crazy!*
If you have experience with C, then you are probably not concerned.
In fact, you're probably delighted that you don't have to reach for that shift key!

On the other hand,
this makes it very difficult to convey the concept of a reference to a student.
When I learned C in my undergraduate operating systems course, 
I did not understand why there was concern about pointers.
Sure, it was something unordinary compared to Java, 
but the differences between a struct a pointer to a struct were always clear.
This critical concept was constantly reaffirmed in my head when working on the labs.
Everytime I used the `->` notation,
I was forced to say to myself, "I am dereferencing this and accessing a field."

[The example code for this section can be found here](https://play.golang.org/p/4epkDbbkbxF).


## Too Many Assignments

I know many people who love to return more than one value at a time.
Those people would be happy to know that Go alllows you to return multiple values.
Without exception throwing, Go often depends on this practice for error handling.
Suppose we have some function that returns an integer and an error.
This is typical pattern in Go, and I've written an example below.

```go
package main

import (
	"fmt"
)

func tryFunc() (result int, error err) {...}

func main() {
    result, err := tryFunc()
    if err != nil {
        panic()
    }
    fmt.Printf("The result is: %v\n", result)
}
```

There is a slight inconvenience in the fact that this style will result in repetitive code
([and I'm not the only person who thinks so](https://www.toptal.com/go/4-go-language-criticisms)), but there is nothing inherently wrong with this.
However, what happens if we call it a second time?

```go
...
    result1, err := tryFunc()
    if err != nil {
        panic()
    }
    fmt.Printf("The first result is: %v\n", result)
    result2, err := tryFunc()
    if err != nil {
        panic()
    }
    fmt.Printf("The second result is: %v\n", result)
...
```

We are reassigning a value to `err`.
You can make the argument that this is only done for error handling,
but there is nothing stopping us from writing poor code.
This problem becomes more apparent in the example below.

```go
...

func someFunc() (int, int) {...}

func main() {
    result1, result2 := someFunc()
    fmt.Printf("Result1 is %v, and Result2 is %v", result1, result2)
    result3, result1 := someFunc()
    fmt.Printf("Result1 is %v, and Result3 is %v", result1, result3)
}
```

The way we are encouraged to use Go is to separate assignments and reassignments,
yet we are mixing them together.
That feels weird!
For example, the code below will not compile.

```go
package main

import (
	"fmt"
)

func main() {
    result := 1
    fmt.Printf("Result is %v", result)
    result := 2 // Can't do this!
    fmt.Printf("Result is %v", result)
}
```

The accompanying compiler error would be `no new variables on left side of :=`.
Now, I can read.
It says "no new variable**s**".
It's important to remember that the short variable declaration operator (`:=`) is a way to [quickly and implicitly assign a value to a variable](https://golang.org/ref/spec#Short_variable_declarations).
Reassignment is handled with the `=` operator.
The ability to reassign a value to a variable with an assignment operator in one case and not the other feels inconsistent.

[I'm not alone on my concerns over the short assignment operator](https://www.reddit.com/r/golang/comments/9xnizp/go_short_declarations_are_evil/).
The linked post features the response that this is a scoping and shadowing issue,
but being allowed to practice these bad habits is... well... bad.
Even I think I'm being a bit pedantic.
I should mention that I did not initially have any issues with this.
However, when I realized what I was doing, 
I could not stop thinking about it.

[The example code for this section can be found here](https://play.golang.org/p/6f7d_lyIfV8).


## Get Your Priorities Straight

While working on a Distributed Systems lab, my parter had handed me a commit with a compile warning:
"loop variable i captured by func literal".
A quick explanation is in [this straightforward post](https://stackoverflow.com/a/58151372).
To illustrate my point, the code looked something like the code below.

```go
package main

import (
	"fmt"
)

func doSomethingWith(i int) {...}

func main() {
    for i := 0; i < 10; i++ {
        go func(){
            doSomethingWith(i)
        }()
    }
}
```

It should instead look like the code below.

```go
...
    for i := 0; i < 10; i++ {
        go func(anotherI){
            doSomethingWith(anotherI)
        }(i)
    }
...
```

The compiler warned us becasuse the "bad" implementation can exhibit unintended behavior.
[This is such a common mistake that it got its own page on the Go GitHub repo](https://github.com/golang/go/wiki/CommonMistakes#using-goroutines-on-loop-iterator-variables).
You must note that I am **not** against this compiler warning!
The compiler is informing us some funky things can happen,
and we want to know that.
My point is: if this is a "mistake", then why is this only worth a compiler *warning*?

Don't you find it annoying that Go will throw a compile *error* for an unused variable?
It does this to help you write better code because "[an unused variable is often a bug in your code](https://npf.io/2014/03/unused-variables-in-go/)".
Yet, even picky languages like Rust will only issue a compiler *warning*.
Further, Go does not tolerate unused imports.
I feel like I'm punished everytime I instictively save after declaring my imports.
Visual Studio Code immediately proceeds to remove the lines of code I wrote just beforehand.

All of this seems completely bass-ackwards!
In fact, it's *absurd*!
I do not regularly program in Rust.
However, if I were to sum up one of the most important ideas of Rust: 
"I should not be able to do anything wrong, but when I do, I know I'm doing it wrong".
Go does not follow this mentality.
There are places where Go seems to react too much or too little.
It has trouble reacting "just right".

[The example code for this section can be found here](https://play.golang.org/p/9OtdFJkidSw).


## Conclusion

Although I find it incredibly easy to write code (fast!) in Go,
I have not enjoyed programming using it.
Many of the language's nuances are incredibly concerning to me.
Simply put: I don't wanna Go!

Cover photo courtesy of [Wikimedia](https://commons.wikimedia.org/wiki/File:Pocket_gopher_-_Pacific_Grove_Museum_of_Natural_History_-_DSC06653.JPG).