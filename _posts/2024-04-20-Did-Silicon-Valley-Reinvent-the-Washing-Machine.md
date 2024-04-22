---
layout: post
title: Did Silicon Valley Reinvent the Washing Machine?
tags: [rant, engineering]
featured: false
hidden: false
---

"Live Free or Die": Analog Edition

## The Status Quo

My apartment complex used to have a card system for their laundry services.
It was a credit-card-sized reloadable card, which had an EMV-style chip in it to be read by the machine.
The total for a wash and a dry was $6.

## The Part Where Things Go South

Unfortunately, the self-help point-of-sale terminal was constantly down.
This meant it was impossible to load your card for often a week or two at a time until a service person could come out and fix the machine.
Thus, you might end up going a week or more without doing laundry.
Obviously, this is problematic.

## Enter "The Disruptor"

This is where "the disruptor", Tumble, comes in.
My apartment complex changed providers to Tumble in 2024.
Tumble is an app which allows self-service of the laundry machines via their app.
Unfortunately, the cost to use service for a wash and a dry is $10.
That's a sigificant difference, which we all are reasonable to assume is to pay engineers to maintain an app (with many significant bugs of course, but that's not important right now).

## Why Should I Care?

### The Status Quo Was Preferable

**Most laundry rooms in apartment complexes are in the basement**.
Basements are often under a giant slab of concrete, which is a cellular signal deadzone.
Ergo, there is no cellular service in the laundry room, which means that the Tumble app is not able to reach the backend service.
Bluntly, *the Tumble app is borderline unusable*, and **no change from engineering will ever fix that** because a fundamental mistake of an assumption was made at the beginning of the design phase.
You *must* consider how the user will use your service.
One does not simply throw an app over the fence in a desparate bid to "disrupt".
Unfortunately, too many have gotten rich from this practice, and it's hard to discourage.

### "Old People"

Once again, this is a case of Silicon Valley innovation, which ultimately makes things more difficult for the elderly.
If you are an older person (like my grandmother), you've just been shuttered out from yet another simple, yet important, aspect of your life because you do not have a smart phone to run the app.
I *never* approve of this, and I *never* will.
Everytime I think about moving to a feature phone, I am immediately held back by the realization that my apartment door requires a smart device via the Latch app in order to open.
If you wish to sell a product , *you absolutely must consider users who do not have smart technology*.
Thankfully, Latch has a card key to be used with their locks, but Tumble has no analog backup.
*This is unacceptable*.

## Conclusion

I recognize I look ridiculous when I write so many italicized and bolded statements,
but the number of "disruptors" actively making life more difficult for everyone is shocking.
Not everything needs "disrupting".
However, many things do need refining, and we should always welcome the changes after serious evaluation.
Once again, I find myself screaming into the void, "plan for the offline case".
It will happen.
