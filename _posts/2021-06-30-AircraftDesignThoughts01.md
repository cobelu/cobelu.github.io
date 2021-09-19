---
layout: post
title: Thoughts on Aircraft Design Part 1
tags: [aerodynamics, airplane, design]
featured: true
featured_image_thumbnail: GA30A-412
featured_image: assets/images/posts/2021/06/30A-412.jpg
hidden: false
---

# Thoughts on Aircraft Design

One of my COVID reads has been *GA Airfoils* by Harry Riblett.
Some people love Riblett's airfoils.
They helped make the Sonerai, BD-5, and Bearhawk become better, safer planes. 
Some people hate them.
There is some concern about their performance at low Reynolds numbers.
Either way, there's a lot to take away from his work.

I don't have access to a wind tunnel, so I have to do my tests with XFOIL and XFLR5.
I keep a Windows machine around just to use SolidWorks, which I also use for XFOIL.
The learning curve is incredibly steep.
Normally, I use a Mac, so I use XFLR5 more often.
Of course, all I can do is click buttons, so the data provided is not 100% realistic.

The Thatcher CX4 I am building has a lot of interesting "features".
I don't particularly love all of them, and I have a mental list of things I would revise if I build another.
One interesting tidbit is that nobody in the builders' community really knows what the airfoil actually is.
I originally read that it utilized a Clark Y, which is not a particularly efficient airfoil.
In fact, it's a terrible, outdated choice from the 1920's that shouldn't be used on anything besides a model.
Later, I found out that the CX4 uses a NACA 4412, which was famously used on the Aeronca Champ.

![The venerable NACA 4412.](assets/images/posts/2021/06/4412.jpg)

In order to not need a wing jig, Dave Thatcher drew a flat bottom on the 4412.
It saves a lot of time to build the wing on a flat table without a jig.
Unforunately, this decision degrades performance quite noticeably.

![Performance degrades when a flat bottom is used.](assets/images/posts/2021/06/4412_comp.jpg)

Now, using the 4412 is a 12%-thick airfoil with a maximum thickness at 30% of the chord.
The equivalent Riblett airfoil is a GA30A-412.
Again, using a Riblett airfoil does not magically solve all of your problems.
However, it does yield some impressive performance gains.

![The impressive GA30A-412.](assets/images/posts/2021/06/30A-412.jpg)

Later, I considered the flat-bottom modification to the GA30A-412 and had some fascinating results.
Instead of a noticeable degradation like on the NACA, performance change was almost negligible!
Amazing!
This is a fantastic little airfoil, and I wish someone in the Thatcher community would try using this instead.
They'd likely see a bit of performance improvements in takeoff, climb, and cruise.

![Results are impressive to say the least!](assets/images/posts/2021/06/30A-412_comp.jpg)

I'm not a fan of Riblett's constant rambling, whining, and copyright violations in *GA Airfoils*.
On the other hand, some of these airfoils are fantastic choices for GA to adopt.
