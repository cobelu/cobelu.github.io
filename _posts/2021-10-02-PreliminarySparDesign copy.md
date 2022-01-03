---
layout: post
title: Fixing a Perfectly Good Spar
tags: [airplane, design, structure]
featured: false
hidden: false
---

# Fixing a Perfectly Good Spar

We've all heard the saying: "if it ain't broke, don't fix it".
I've been thinking very hard about how to "improve" the CX4.
Of course, I don't plan to incorporate my changes in my first airplane build.
However, I am keeping track of them for project #2.
One structure of the CX4 that needs revision is the spar.
Tapering the 3/16" extruded angle aluminum is very difficult.
If we could redesign it to safely substitute 1/8" extrusion angle, we could make the part much easier to build.
We'd also save weight.
Heck, if we saved enough weight, then we could save the builder some time by not having them taper the caps at all.

Yes, messing around with a wing spar is serious business.
It's important that you don't make a mistake when designing the things which keep you from falling out of the sky.
Luckily, we have an existing structure, which we can utilize to design something that is of *equivalent* strength.
At the moment there is no concern to design something stronger.
Instead, we are focused with *designing something at least as good*.
OK, how do we do that?

## Pick a New Airfoil

This is the part where I have to back up and explain another change that I feel should be made.
The CX4's airfoil needs to be replaced.
I've written in the past how I'm a fan of the Riblett GA30A-415.
It's a 15% thick airfoil with it's thickest point located at 30% of the chord length.
On paper, it competes with the NACA 4415, a thicker version of what went on the Aeronca Champ.

## Preliminary Sizing

Great, so we've selected an airfoil.
If we do some preliminary sizing, we'll find that a 44" constant chord should work well with a 23' wingspan.
That will yield 10' main wing panels and a 3' center section spar.
This is important because extrusion angle is typically sold in lengths of 20'.
Further, we will have almost the same amount of wing area and an aspect ratio around 6.
Awesome!

Now, we find that 15% of 44" is about 6.5".
Perfect!
By selecting a thicker airfoil, we increased our spar web height by an entire inch!
This may not sound like a lot, but *increasing the spar web height is the most efficient way to increase moment of inertia*.
Increasing moment of inertia means making the spar more difficult to bend, so that's what we want.
The question remains: is this enough to change the materials?

## Number-Crunching

It's time to pull out the calculator.
If you're me, that means trying to implement a moment of inertia calculator in Rust.
Why?
Because Rust.
That's why.
Then, you get tired of it all and just switch to Google Sheets.
I don't have the sheets link set up so you can use it yourself (sorry!), but [you can verify it exists for yourself](https://docs.google.com/spreadsheets/d/1tXDSn85MDPpcaq5BnqviH8qIzU9IJrgyHdACOGwkWqM/edit?usp=sharing).

## Results

I compared our design to Dave's and found the following:

* The cap could be reduced from 1-1/2" x 1-1/2" x 3/16" extrusion angle to 1-1/2" x 1-1/2" x 1/8" extrusion angle.
* The web could be reduced from 0.040" aluminum to 0.032" aluminum.
* The doubler can be reduced from a total of 3/8" to 1/4" 2024-T3/T4 aluminum.
* The moment of inertia at the root is 10.29 in^4 for Dave's design.
* The moment of inertia at the root is 10.58 in^4 for our design.

## Conclusion

Simply changing the airfoil in this case seems like a very good decision.
I haven't crunched the numbers for weight yet, but we've lost so much weight by downsizing our angle and doublers.
It feels like we should be able to not have to taper the caps and still have the same weight as Dave's design in the end.

Thanks for reading about my insane pipe dream.
Until next time!

## Addendum

I crunched the numbers on the alumunum structure with weights provided by Aircraft Spruce.
I found that our structure is 0.02 lb. lighter that Dave's!
With a proper airfoil, we were able to size the spar such that we could have the same weight and we don't even have to taper the caps.
*This saves hours of work* for a builder, and it also saves the builder some money!

Later, I'll use Schrenk's method to start considering loading, so I can test it in SolidWorks.
