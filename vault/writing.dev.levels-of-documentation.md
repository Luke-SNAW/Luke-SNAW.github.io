---
id: uhh5iydw9l8ws6sewxlu09y
title: Levels of documentation
desc: ""
updated: 1674004772922
created: 1664150177559
---

> https://news.ycombinator.com/item?id=32909343

## powersurge360

I am becoming increasingly skeptical that good internal documentation is even possible. I've been working in software development for around 12 years and have _never_ seen it done well and asking around the best I've heard offered up is the equivalent of an internal stack overflow.
For a while, I thought that maybe an exception would be having a technical writer on staff but after reading this post I'm significantly disheartened on that front too. I'd be interested to hear if anyone on hacker news has experienced good internal documentation and even more interested if any of you folks have experienced anything truly _great_.

For my contribution, I've found that documentation fails for a couple of reasons. The first is the burden of correctness. The people who most would like documentation are also the people who most need the documentation and they usually are also the people most likely to be reluctant to contribute to the documentation because they don't feel they can accurately represent the information. Imagine someone ramping into a feature and spending a few days reverse engineering how it works, collecting info, etc. Sometimes they'll put it up somewhere but a lot of the time contributing partial information feels 'wrong'.

And the second bit I find to be a big reason why documentation efforts fail is just the sheer friction of putting it into the documentation store to begin with. In confluence, for example, if you have a bit of information it can be tough to work out how to categorize it, where in the hierarchy it should go, etc, etc. Or if it's a GitHub wiki you want to put it somewhere that it is discoverable but also be careful that it's 'correct' because you don't want to break backlinks if it gets recategorized.

I've mostly given up on it at this point. Instead, I take detailed personal notes and make them publicly available. It doesn't have to be correct because being advertised as personal notes means that it's my opinion on the truth rather than objective fact. It isn't far away from my codebase, I can just tap a short keybinding in my editor to type my notes or search them and I can link directly from the notes to lines of code in files to jump back and forth. The particular system I use means that if I write a short snippet of code to solve a one off issue (like calling a path helper to derive a URL that I can't find in the interface) I can even drop it in a code block and execute it right from my note-taking tool. It isn't ideal for sure but I've gotten way farther in having a shareable knowledge base this way than I have in literal years of trying to get a shared, useful documentation store spun up.

### P5fRxh5kUvp2th

The issue is that people seem to equate "good documentation" with complete.
It's just not possible to do this. I think it would be better to talk about "effective documentation".

My opinion on the matter:

Three levels of documentation

1. high level documentation that describes the problems and the goals from the business perspective

2. mid-level documentation that describes the architecture that gets us there

3. low-level documentation, aka code.

high level gives you direction (where), mid-level gives you context (what), low-level gives you implementation (how)

You need the what to understand the how, and you need the where to understand the what.

The other piece is an acceptance that you can't document away the need for tacit knowledge.

To draw an analogy.

No amount of documentation is ever going to allow a kid to hop on a bike and ride it perfectly the first time. That is not what it means to teach a child to ride a bike. Instead the goal is to have enough documentation to minimize the amount of time it takes that child to gain the tacit knowledge necessary to ride a bike acceptably.

Once you accept the above and lower your bar, "effective documentation" becomes much more achievable.

#### tremon

One of the reasons this is hard is because it's not that easy to really separate the three levels of abstraction. It's very difficult to state the business requirements neutrally, without coloring in any technical sort of solution (especially since the technical solution is usually what the customer asks for), and it's equally hard for many people to write a high-level technical design without filling in (or assuming) various implementation details.
In my team, I have started spelling out more concretely what I expect from the documentation at various levels. Keeping with the three levels specified by the GP, we always document:

1 - business rationale: what are we building, and who are we building it for (enumerate the stakeholders and their processes)

2 - component diagram: a graphical sketch of what different building blocks are involved (datastores, api endpoints, webservers, etc), and showing the direct connections between them

2 - data flow diagram(s): showing entry, exit and storage points for each class of data moving through the system

3 - starter documentation: what does a developer need to know/do before working on this project? This includes tooling, pointers to outside documentation, and a reading guide pointing to the rest of the project's documentation.

The rest of the low-level documentation is the responsibility of the team itself.

By insisting on documenting the second layer mostly graphically, there is less potential for overlap between the different layers. Of course, no documentation system is perfect, but I find the above has suited us quite well for what we do (we write business integration software, no huge client applications or software suites. YMMV, obviously).

#### tremon

> I love this separation of aspects and the graphical representation to nudge out overlap.
> How do you keep the layers consistent? How do you keep track what update to some layer is not covered in some other layer yet? Is that visible right in your layers? or some outside backlog?

The simple answer is that we try to keep most of the documentation (layers 2 and 3) in the same repository as the code itself, though that in itself is no guarantee that the documentation is up-to-date. Layer 1 documentation mentions explicitly which changes are part of which project, so the project timeline (which is external to the development team) should show if a mentioned project is supposed to have been completed already.
There are no airtight rules other than being mindful of your own processes. Our workflow generally looks like this:

Changes to level 1 documentation are done by the product or project manager in preparation for the work, so it's pretty easy to make that part of the documentation lead, rather than lag, the implementation. It's stored in the project wiki, rather than with the code. But that wiki is still git-based, which means we have an easily auditable changelog to check when a particular piece of information was last updated.

Layer 2 changes are usually done by (senior members of) the development team, but it's done in the week before the implementation starts. Since we use those diagrams to communicate with the rest of the development team about the changes required, the documentation updates happen rather organically.

I find that layer 3 documentation updates tend to be the hardest to capture in a process, because the code itself is much more in flux than the higher layers. What helps us here is that our developers know that the codebase they're working might not be worked on again until months in the future, so it's in their own interest too to keep the documentation correct. That said, we do have an explicit check for documentation updates in our project delivery checklist.

The most challenging situation is when we discover during development that an architecture redesign is required, but most of the time an architecture adjustment also means we need to re-evaluate the workload and possibly the delivery date, which basically means our process resets and we re-involve the product or project manager. Funnily, this then usually results in more documentation rather than less...

We sometimes also have a 2-person development team for small changes (never 1 person though), in which case all three layers are handled by the same people. But because they're updated in different stages of the project, and because they're already used to the same workflow in larger teams, the small team size doesn't affect the documentation quality as much as I initially feared.

---

> https://c4model.com/
