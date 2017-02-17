---
layout: post
title:  "Keep It Simple, Stupid"
date:   2017-02-17 02:24:20 +0000
---


I built a web app called Project Organizer, in Sinatra. It's designed to help users keep track of their projects and its associated tasks.  Currently, its funtionality is fairly straightforward:

- Create and view projects
- Create and view tasks for each project
- Mark tasks completed
- Expect projects to be marked completed when all tasks are done
- Delete tasks, projects and account

### Video walkthrough
[![IMAGE ALT TEXT](https://img.youtube.com/vi/13SoAVfOfas/0.jpg)](http://www.youtube.com/watch?v=13SoAVfOfas "Video Title")

When I was coming up with how to design the app I had an overambitious idea in my head.  Group projects could be created; other uses could join these projects; the moderator of a group project can assign tasks and set due dates; people could collaborate on the same task etc.

However, when it came to trying to map out my object relations it became impossible to try and figure out all the ActiveRecord associations.  Then someone told me something I took to heart: *Keep It Simple, Stupid*.

Suddenly, it clicked. Why try and build everything I wanted to do into version 1.  I'm building this on my own and I have a limited amount of time I can afford to take on this.  The fact I wanted to do everything all at once was...well *stupid*.
So I kept it simple:

- User has many Projects
- Project has many Tasks

Trying to build functional models, controllers and views with those simple relationships would be more than enough work for a budding developer such as myself.  Get that all working crisp and clean first, then build up from that in later versions.  Simple.

[link to the github repo if you're interested](https://github.com/jilustrisimo/project-organizer)
