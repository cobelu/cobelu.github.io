---
layout: post
title: Thoughts on Aircraft Design Part 2
tags: [aerodynamics, airplane, design]
featured: true
featured_image_thumbnail:
featured_image:
hidden: false
---

# More Thoughts on Aircraft Design

Uh oh, I've been reading aircraft design textbooks again!
**Warning: I am not an aircraft engineer** (just an enthusiast).
What follows is a *simplification* of concepts in aerodynamics.

Recently, I looked through Ladislao Pazmany's *Light Airplane Design*.
This isn't really a textbook *per se*.
Instead, it's more of a walkthrough of *why* Pazmany made certain decisions while he was designing the PL-1/PL-2.
It's a lovely, aerobatic low-wing that was used by several air forces as a trainer across the Asian continent. 

## I Love Hershey Bars (Wings)

One page that I keep coming back to is the page comparing the typical stalling behavior of different wing shapes.
The PL-1 and PL-2 have a "Hershey Bar Wing", which is a wing of constant chord.
In other words, when viewed from the top, the wing is a boring rectangle.
You can view the glass as half-empty ("This is boring!"), or you could choose to view the glass as half-full ("This only requires one rib pattern!").
I choose to be an optimist here.

An ellipse is the most efficient wing shape we could use.
The most notable example of this is the Supermarine Spitfire. 
Unfortunately, constructing that ellipse is very difficult if we're not working with composite materials.
But wait, there's more!
At such slow speeds as most of general aviation (<200 mph/<320 kmh), the aerodynamic gains are mostly unrealized.
Further, the design naturally stalls in a way such that the turbulent air passes over most or maybe even all of the ailerons, as noted by Pazmany.
That's bad!
**This results in lost aileron effectiveness in high angles of attack**
(Hold onto this information; we'll need this for later!). 

![The Supermarine Spitfire and its elliptical wing ([Airwolfhound](https://commons.wikimedia.org/wiki/File:Spitfire_-_Season_Premiere_Airshow_2018_(cropped).jpg)).](assets/images/posts/2021/06/4412.jpg)

"Hershey bar" wings do not naturally exhibit this property, so they tend to have good aileron authority, even at high angles of attack.
This makes sense if you think about it: the ailerons are typically placed at the end of the wing.
Typically, a wing should be designed such that it stalls *from the root to the tip*.
Thus, the buffeting air is not going to reach all the way to over the entire ailerons.
All of these facts contribute to why the Vans line of aircraft, *the* most successful kitplanes, all use untapered wings.

## The CX4's Atypical Wing

The CX4 has an atypical wing: 8 ft. (approximately) constant chord main panels with trapezoidal extensions, which in sum approximates an ellipse.
This is not inherently bad.
However the ailerons are 8 ft. long and are positioned on the main wing panel.
*That leaves the tips of the wing without a control surface!*

I need to clarify *why* this was done.
Dave needed all extrusions used on the aircraft to be limited to 8 ft. long.
This made shipping the materirals substantially more affordable.
On the aerodynamics side, **we're forcing function to follow form**.

Let's go back to the wing design's implications.

## This Is B-A-D

Finally, we're *almost* to the hooplah of this whole shindig.
There's been a lot of talk in the Thatcher community lately about two things:

1. The gear needs to be extended.
2. The ailerons are not big enough.

So, without further ado... here are my *unpopular* opinions.

### The Gear Does Not Need to be Extended

I have though *a lot* about this.
Engineering is about balancing your trade-offs to make the best possible final design decisions.
If you extend the gear, you will be able to more effectively perform three-point landings.
This is good!
Three-pointers are easier than wheel landings, and they also allow you to land slower, which is safer if something goes wrong during the landing.
Pitch is speed in an aircraft.
In order to achieve a slower landing speed, you need to have a higher angle of attack.

However, the CX4 was **not** designed for this.
Remember, we said earlier that elliptical wings tend to have poor roll authority at high angles of attack.
Further, the CX4's ailerons are placed *inboard*!
The culmination of these choices results in *very* poor roll control at high angles of attack, which is exactly what builders are noting.
[Well, there's your problem](https://knowyourmeme.com/memes/well-theres-your-problem)!

## 1 + 1 = 3

I'm not finished with my Thatcher.
I will likely face the same problems that other builders/fliers have.
Frankly, I don't care.
The CX4 fit my mission as an affordable, fun aircraft.
There isn't anything else quite in its class unless I were to design it myself, so maybe that day will come sometime soon.

## Summary

The CX4 likely exhibits poor authority because of its wing planform.
The proposed changes to improve handling are a trade-off which have their downsides.
A better approach would be to design a new wing of equivalent area with a rectangular planform.
