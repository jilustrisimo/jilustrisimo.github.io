---
layout: post
title:  "How to Think About Debugging"
date:   2017-08-09 01:43:09 -0400
---

*preface: There will be no code in this blog. This is for anyone who stuggles with the thought process of how to debug an app.*

A lot of new students to programming easily become baffled when it comes to debugging an app.  They can end up changing code blindly and exacerbating the problem or simply stare at their screen, frozen, unable to comprehend what to do.  If you're new to programming and this is seeming familiar, don't worry.  It's normal to feel stuck like this, especially if you're just starting out.  It's possible you're just seeing every function or method individually and are unable to see how they connect.  Keep reading and hopefully this can help your thought process on how to think about data flow in an app and how to approach debugging it.

Imagine yourself as the supreme ruler of a small town, you're the mayor, the city council, the chief of police etc.  I know, it might not look like much but its still your town.  Your app, your code, **is** this town.  All the different parts of your program are the buildings and houses.  Imagine the roads as the way all those different components communicate, and the cars going up and down the roads are like data flowing through your app.

Now imagine there's a bug, for our analogy let's call it a criminal.  The error messages are like your citizens calling in to report a crime, where it took place and what happened.  If you're unable to determine the problem and how to fix it just by looking at the errors you can set a breakpoint.  Breakpoints like `pry`, `debugger` or whatever is available to you are like if the police are setting up a premitter or road block by where the incident happened thereby not allowing anything to go through without them being able to see it.

There's another thing too, unlike actual police and actual mayors, **you** can rewind and freeze time in our little scenario.  You can push data through your app as many times as you want, recreating the bug each time with your breakpoint in place already.  So with that, you're able to look at the data that hits the breakpoint.  If the bug already happened then set your breakpoint a tiny bit earlier.  Think of it like tightening a perimeter or moving a road block further up the road, except you can have the same set of cars hitting your roadblock as many times as you want, so you can keep moving it until its right before the bug or incident takes place.  From there you can manipulate and test data to stop the bug ::ahem:: criminal ::ahem:: before it occurs.

Thats all there is to it.  Get in the mindset of how data flows through your app and you'll be exponentially better at being able to debug it.
