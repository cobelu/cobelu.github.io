---
layout: post
title: Adventures in Scala - Scalafix Options
tags: [scala, software]
featured: false
hidden: false
---

Use `scalafix`!

## About

[Scalafix](https://scalacenter.github.io/scalafix/) is an *essential* tool if you're working in Scala.
Although I prefer no-frills solutions (the less you can modify, the better), scalafix is *the* linter for Scala.

## Options

Although *you should totally throw errors when there are unused assignments* (Google made this decision based on years of experience while designing Go),
you may not be able to convince your team to do this.

[The docs for the `RemoveUnused` setting are here](https://scalacenter.github.io/scalafix/docs/rules/RemoveUnused.html).
If you want to only remove unused *imports*, the scalafix docs do not explain this well at all.
Your `.scalafix.conf` file would look something like this:

```conf
rules = [
  RemoveUnused
]
RemoveUnused.privates = false
RemoveUnused.locals = false
RemoveUnused.patternvars = false
RemoveUnused.params = false
```

Note that *you have to explicitly set the other parameters to `false` beacuse they are all set to `true` by default, as shown in the docs*.

## Let's Be Clear

If you are spending more time worrying about the formatting/linting parameters, then you are doing it wrong.
Remember that the point is to make your life easier later.
This is why I personally prefer a combination of [Black](https://black.readthedocs.io/en/stable/) and [Ruff](https://docs.astral.sh/ruff/) when I write Python.
I don't waste time worrrying about setting parameters.
Instead, I just write and let it clean up after me.
The point is: I put away my tools and sweep my shop when I'm finished for the day.

## Running in CI

Why run only locally when you can run in CI?
All you have to do is run:

```bash
scalafixAll --check
```

## Why Does This Matter?

### Warning: Rant Alert

One problem with modern code formatters (e.g., IntelliJ) is that they like to format your code.
If you don't format your code, there's a good chance someone else on your team will!

The possibilities of this scenario are as follows:

* This change might accidentally show up in a PR.
  * Someone will likely comment that it doesn't belong.
  * The raiser of the PR also has to go back and remove the changes.
  * CI has to run again.
* The import fixes might even get merged.
  * Commit history doesn't make sense.
  * Unnessecary merge conflicts can be created.

In short, *everybody loses when you don't use a linter* to format your imports at an absolute minimum.
You either waste time preventing the unnecessary changes from landing, or you create unnecessary changes that do not pertain to the purpose of the PR.

Let's return to the idea of unoptimized imports.
When you enforce optimized imports, you can easily deal with any conflicts by taking both changes in the import block area and then optimizing the imports.

## Conclusion

Use a linter!
Use a formatter!
Personally, I can't understand how any team could possibly maintain a codebase without them.
*It doesn't have to be perfect*, but needs to exist.

## Disclaimer

I later learned that `scalafix` does not play well with implicits.
Be careful when using!
