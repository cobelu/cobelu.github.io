---
layout: post
title: Linux Fixes - Linux for the New Year (and You Can Too!)
tags: [linux]
featured: false
hidden: false
---

My New Year's Resolution...

# Use Linux!

## Why I Fail Everytime

In the past, I have always failed to fully switch to Linux.
*This time will be different*.
Let me explain.

## Background

I swapped laptops with my mom because her 2017 MacBook Air (my college laptop) is no longer supported for MacOS updates.
It is one of my favorite laptops ever made because both the battery and the SSD are easily replaced.

## It Starts with the Distro

I know that it's easy to spend too long arguing about which distro is best, but I can assure you that my preferred distro is Pop!_OS.
In fact, the built-in keyboard shortcuts are so intuitive to me that I refuse to use anything else (except maybe Elementary OS).
The aesthetic modifications to GNOME are cleaner than that of stock Ubuntu.
The fonts are easy to read.
The dark mode looks good.
System 76 has a poor track record for contributing to OSS, but they do a fantastic job about thinking how people use computers. 

# The Dreaded `Ctrl` Key

The largest reason I normally fail at using Linux is the `Ctrl` key.
Not this time!
I got around this by swapping the `Ctrl` and `Cmd` key.
That way, I'll actually have acess to the right `Ctrl` key.

I found that swapping this modifier keys is the best compromise to use.
I can get by with almost all of my keyboard shortcuts being *close enough*.
The important thing is that when I save, copy, or paste, my thumb is going to instinctively touch the command key.
I need my thumb to do the work.

In order to do this, create a file `~/.xmodmaprc`.

```
! Erase existing bindings
clear Control
clear Mod4
! Map key 37 (left ctrl) to Super_L (i.e. 'cmd')
keycode  37 = Super_L
! Map key 133 (left cmd) to Control_L (i.e. 'ctrl`)
keycode 133 = Control_L
! Map key 37 (right ctrl) to Super_R (i.e. 'cmd')
keycode 105 = Super_R
! Map key 133 (right cmd) to Control_R (i.e. 'ctrl`)
keycode 134 = Control_R
! And update modifier settings
add control = Control_L Control_R
add mod4    = Super_L Super_R
```

These were my swaps.
If you are working on a different machine, you can find your particular key codes with:

```
xev -event keyboard
```

## Visual Studio Code

I love developing in VSC.
It's super lightweight, and languages I prefer to work in (Go, Rust, etc.) have solid extensions for VSC.
If you do all of your editing in one editor, you only have to remap one IDE!
You can remap your VSC shortcuts to be more like that on Mac.
A subset of updates to your `keybindings.json` file would look something like this:

```json
// Place your key bindings in this file to override the defaultsauto[]
[
    {
        "key": "ctrl+=",
        "command": "-workbench.action.zoomIn"
    },
    {
        "key": "ctrl+=",
        "command": "editor.action.fontZoomIn"
    },
    {
        "key": "ctrl+shift+-",
        "command": "workbench.action.zoomOut"
    },
    {
        "key": "ctrl+-",
        "command": "editor.action.fontZoomOut"
    }
]
```

I prefer to have a difference between editor zooming and workbench zooming because I have poor eyesight and need to quickly adjust font size without adjusting the sizes of all things in the workbench.

## Grrrr... Wi-Fi No Worky

You should be prepared for Wi-Fi not working!
Stock Ubuntu worked out of the gate because it presented me an option on the USB installer startup to install additional drivers.
You should come prepared to your Linux installation with a USB-Ethernet dongle.

## You Can Do It!

I just want to wrap up by pointing out that *you can do it*!
It can seem impossible to switch, but there are ways to get around your problems.
Once you have your settings dialed in, be sure to back them up for your next Linux installation!
