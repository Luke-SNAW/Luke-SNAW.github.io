---
id: 3lvscq8lxm09t82g0owulpe
title: The Expressivity Limitations of Object-Oriented Programming
desc: ""
updated: 1699596181081
created: 1699595829952
tags: OOP
---

> https://two-wrongs.com/expressive-limitations-of-oop.html
>
> The document discusses the limitations of object-oriented programming for encoding knowledge. It argues that knowledge takes the shape of rich propositions involving various relationships, but OOP can only represent is-a and has-a relationships. This inadequate representation leads to confusing code when trying to express domain knowledge. While classification trees are insufficient, cramming knowledge into OOP relationships creates unnecessary problems. The document suggests being mindful of the propositions we aim to encode and considering alternative representations beyond classic OOP if needed. Overall, it argues the shape of our knowledge should drive our code structure rather than restricting knowledge into limited OOP relationships.

tl;dr: Writing software is encoding knowledge. Knowledge takes the shape of propositions. Compressing rich propositions into _is-a_ and _has-a_ relationships does not lend itself to clarity.

That was dense. Let’s back up a little bit.

---

I’m learning a little bit of _cognitive task analysis [^1] at the moment, and one of the first tools the authors present are concept maps[^2]. Concept maps are based on the core idea that \_propositions are the fundamental unit of knowledge_.

[^1]: Working Minds: A Practitioner’s Guide To Cognitive Task Analysis\_; Hoffman, Klein, & Crandall; Bradford Books; 2006.
[^2]: If you do an image search on the web for concept maps, you will see a lot of mind maps – it is a common misconception that concept maps and mind maps are the same thing. They are not. Concept maps have proven themselves useful in studying expertise, whereas mind maps … I don’t actually know if mind maps are useful for anything.

I’m not the right person to strictly define propositions, but you probably get the right idea if you think of a proposition as a statement that, if you would make it more concrete, could become a single testable hypothesis. Here are a few examples of propositions[^3]:

- The gasoline engine is off when the vehicle is stopped.
- High voltage parts incorporate electromagnetic shielding.
- The vehicle may cause sound interference in some third party-produced radio parts.
- The service plug is used only when the vehicle is subject to high voltage.
- A label is usually attached to the front side window.
- This system does not guarantee absolute security against all vehicle thefts.
- The indicator light goes off after the power switch has been turned to on.
- The units on the gauges differ depending on the target region.
- The warning indicators inform the driver of the status of the vehicle’s systems.
- Regeneration refers to conversion of kinetic to electrical energy.
- The hybrid system indicator requires the shift lever in drive.

[^3]: I just pulled arbitrary quotes from a document I happened to have open on my second monitor anyway.

Look at the richness of those statements! We have temporal conditions (“when” and “after”), statistical generalisations (“usually” and “may cause”), preconditions in both directions (“used only when” and “requires”), statements of subcomponents (“incorporate”), linguistic abstraction (“refers to”), psychological statements (“inform”), functional dependencies (“differ depending on”).

This is what knowledge looks like. _A_ can be related to _B_ through a wide variety of abstract relationships. This matters for software design, because programming is literally translating our knowledge about the problem into a form the computer can execute. The shape of our knowledge has direct consequences on the shape of our code.

Now, what does object-oriented programming look like? We tell students that it allows exactly two kinds of propositions:

- a car _is-a_ vehicle, and
- a car _has-a_ shift lever.

That’s it. This is not enough to encode the richness of our knowledge about a domain.[^4] Expertise researchers have also discovered this; classification trees are simply insufficient to express knowledge, and if we try, we end up with complicated ontologies that have long since lost any disceranble connection to the original problem.

[^4]: Imagine trying to express “the service plug is used only when the vehicle is subject to high voltage” using those two relationships. You’re likely to end up with confusing artifacts like a `ServicePluggable` which is-a vehicle!

Shoehorning knowledge into the two classic object-oriented proposition types creates problems that are auxiliary to the one we’re trying to solve.

But we can do better!

The first step is to be mindful of what we are doing. Whenever we find ourselves creating a new type of object – especially if it’s one we struggle to find a good name for – we can stop and think about exactly what sort of proposition it is we’re trying to write the code for, and if there’s a better way to express it. If we do this consistently, we may come up with new useful patterns to encode various types of propositions.[^5]

[^5]: And if you happen to look for a way to innovate on programming language design, take a hint from the research around expertise, and come up with first-class ways to encode other propositions.

---

Some preview readers have had a recurring misconception, which I want to set straight: I’m not claiming _is-a_ and _has-a_ are the only types of abstraction available object-oriented _languages_. As a reader pointed out, most object-oriented languages have other types of abstractions which are _not_ the object-oriented parts, like interfaces (_responds-to_), plain functions[^6], and more.

[^6]: Sometimes only available as class methods, but still.

This is specifically what is meant by “stop and think \[…\] if there’s a better way to express it”. It seems to me as if the two object-oriented propositions is-a and has-a are a very popular hammer, and I think we can do a better job of illustrating to people why and how not everything is a nail.
