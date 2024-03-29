---
layout: page
title: Projects
# featured_image: /assets/images/pages/projects/quickie.jpg
---

>“We have a strategic plan. It’s called doing things.” <cite>― Herb Kelleher ―</cite>

## [FliteKlub](https://github.com/cobelu/FliteKlub)

Sorry, it's private!
I'd like to put it out as a commercial app someday.
It's a prototype of a scheduling app for flight clubs.
I wrote it in Dart using the Flutter framework (did I mention I love Flutter?!).
I actually wrote two backends because I was evaluating both a SQLAlchemy/FastAPI stack in Python and a Fiber/GORM in Go.
Both are good choices, but I felt that FastAPI was safer and the built-in Swagger integration was much appreciated.
I am also not fond of the way GORM handles one-to-many and many-to-many relationships.

## [FoilToDxf](https://github.com/cobelu/FoilToDxf)

A quick tool written in Python to convert `dat` files to `dxf` files for importing airfoils into CAD.

## [Barnscrapers](https://github.com/cobelu/BarnScrapers)

Sorry, it's private!
I wrote a Barnstormers scraper to look for an engine for my aircraft project.
If you'd like to use it, then get in touch!
It makes looking for a plane or parts much easier if you're in the market to buy.
It's written in Python with requests, sqlite, and mailgun.

## [Odlaw](https://github.com/cobelu/Odlaw)

Odlaw was the final project for CSCI2390, Privacy-Conscious Computer Systems.
The goal of the project was to help DBAs search for client data in order to quickly package and ship a GDPR-compliant user data report.
[You can read the final paper here](https://cs.brown.edu/courses/csci2390/assign/project/report/odlaw.pdf).

![The Odlaw Logo](assets/images/pages/projects/odlaw.png)

## [LocoStow](https://github.com/cobelu/LocoStow)

LocoStow was the final project for CSCI2270, Topics in Database Management.
Chris Cataldo and I considered how geotemporal data storage could be implemented more effectively.
We built a geotemporal hashing library in Rust.
Attributes in time-series are not able to be treated as first-class citizens.
We determined that looking at a specific case of attribute, a geographic coordinate, would be the most prudent direction to pursue.

![LocoStow](assets/images/pages/projects/loco_stow.png)

## [Bully](https://github.com/cobelu/BuildLog)

Need to document an experimental aircraft build?
Tired of Kitlog, blogging sites, or even handwritten notes?
Me too!
Bully is a builder's logging tool, written in Java.
The project was an excuse for me to learn the JavaFX framework since my undergraduate courses utilized the Swing framework.

![The Bully Logo](assets/images/pages/projects/bully.png)

## [The Chaos Game]()

I learned about The Chaos Game while taking PHYS311 Classical Mechanics.
You could play the game by hand, but I'm a computer scientist, so I wrote a quick Python program to play it for me.
I like how the Turtle package it simulates the point-by-point nature of the game.

![The Chaos Game](assets/images/pages/projects/chaos-game.png)

## [PRRC](https://github.com/cobelu/PRRC)

The Pi Rick-Roll Controller (PRRC) came to fruition when I realized that somebody had written a Python package to interface with the Chromecast protocol.
It rick-rolls every Chromecast device on your connected network.
Use with caution!

## [Picard](https://github.com/cobelu/Picard)

The Picard (a portmanteau of Pi Aviation Conditions Indicator/nod to Star Trek) is a Pi-powered device to show aviation weather conditions on a series of LEDs.
Many thanks to Michael DuPont, whose REST API powers the project.
