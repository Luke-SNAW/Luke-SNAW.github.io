---
id: h4bdthyszcjle90ytec22xp
title: Tidy First? Kent Beck on Refactoring
desc: ""
updated: 1685491221802
created: 1685490543357
---

> https://www.infoq.com/presentations/refactoring-cleaning-code/

## Overview of Software Design

> Change the structure first. Then change the behavior and it'll be so much easier.

There's a basic loop in software development. Somebody has some idea, ok, the software does some stuff, and we want it to do some new stuff. We want to add a widget. Somebody has the idea, and now somebody has to change the behavior of the program, so used to calculate. Now there's a new option for this, and so we calculate some new stuff. This is conveniently a loop. We got an idea. We change the behavior of the program, and that gives us more ideas for what else we could do with the program, and all is well.

We got this basic loop where we got ideas. We change the behavior of the system, that gives us more ideas. If we just keep doing this loop, idea to behavior to idea to behavior, we're going to start going slower, and bugs are going to come up, and programmers will get frustrated and leave. The new programmer is going to be even slower than the old programmers were. As developers, sometimes we think, here's an idea, but before I just change the behavior, I'm going to **change the structure first**. Then I'm going to change the behavior and it'll be so much easier after I've improved the structure that I win already.

...

## Waiters and Changers

> Software design is an exercise in human relationships between waiters who want new features and changers who want to improve the code structure.

The loop is more complicated, and it becomes even more complicated. Here's where I'm going to finally get to this, software design is an exercise in human relationships. Because we got two kinds of people, I call them waiters and changers. I have the waiters up here. The waiters, maybe had the idea for what the software does next, but they can't do anything to change it. They have to wait. They're patiently, impatiently, a little foot tapping. They're waiting for the software to change. There are a different kind of people in this picture called the changers. The changers, this is the people mostly sitting here, where we know what to do to go in and change the behavior of the software. Already, we've got conflict, because you have waiters who want to see that next behavior change, they want the next feature. You got the changers, though, who know that if we just leave the structure to deteriorate, things are going to get worse. It's going to be less fun to work on, and more bugs, and more annoying. We're going to get further behind. We have a misalignment of incentives. Changers wanting to invest in the structure. Waiters in the short term, they don't even see the structure. It doesn't affect their daily life. They just want that feature as quickly as possible. We come to the first relationship. This waiter-changer relationship is fraught because of the divergence of the incentives, and the different vocabulary, different value systems, different wardrobes. Although I'm working on that. The third book in the series is going to be about using software design to encourage positive waiter-changer relationships.

## Tidy First

## Design Upfront

> Design upfront is a bad idea economically due to the time value of money and spending less and later is equivalent.

## Optionality

## Coupling

> The cost of a software system equals the coupling in the system plus the cost of decoupling.  
> There is a tradeoff between coupling and decoupling, and designers must find a balance.  
> Coupling is when changing one element requires changing another.  
> The cost of big changes in a system comes from its coupling.
