---
id: 88st12x3pi51cvyokddzd91
title: 'If You Thought the Speed of Writing Code Was Your Problem You Have Bigger Problems
desc: ''
updated: 1773800660881
created: 1773800490870
---

> https://andrewmurphy.io/blog/if-you-thought-the-speed-of-writing-code-was-your-problem-you-have-bigger-problems

This article argues that focusing on **increasing code writing speed**, particularly with AI tools, is often misguided as it doesn't address the true **bottlenecks** in software delivery. The **Theory of Constraints** suggests that optimizing non-bottleneck steps actually worsens the system, leading to increased inventory and slower overall delivery. The real bottlenecks typically lie in **understanding what to build**, the **processes after code is written** (reviews, testing, deployment), **deploy trust issues**, **lack of post-ship feedback**, and **organizational coordination problems** like excessive meetings.

---

It's Tuesday morning. Your VP of Engineering is standing in front of a slide deck, vibrating with the kind of excitement usually reserved for people who just discovered cryptocurrency in 2017. They've just come back from a conference. Or maybe a vendor dinner. Three glasses of pinot noir and a demo, and now they have _news_.

> "We're rolling out AI coding assistants across every team. Early numbers show a 40% increase in code output. This is going to transform our velocity."

The room does that thing where half the people nod along and the other half develop a sudden interest in their laptops. Your staff engineer is doing that face. You know the face - it's the one where they're calculating whether to say something or just update their LinkedIn later.

Nobody asks the question that matters, which is: velocity toward _what_, exactly?

Because here's what just happened. Your VP looked at your entire software delivery organization, identified the one thing that was already pretty fast, and decided to make it faster. They found a station on the assembly line that was _not_ the bottleneck, and threw money at it.

If you know anything about how systems work, you know this doesn't just fail to help. It makes everything actively worse.

## Goldratt would like a word

In 1984, Eli Goldratt wrote [_The Goal_](https://amzn.to/4sGsdMU), a novel about manufacturing that has no business being as relevant to software as it is. It's also the most useful business book you'll ever read that's technically fiction, which is _almost_ the exact opposite of most KPI frameworks.

The core idea is the Theory of Constraints, and it goes like this:

Every system has exactly one constraint. One bottleneck. The throughput of your entire system is determined by the throughput of that bottleneck. Nothing else matters until you fix the bottleneck.

That's the part most people get. Here's the part they don't, and it's the part that should scare you:

> **When you optimize a step that is not the bottleneck, you don't get a faster system. You get a more broken one.**

Think about it mechanically. If station A produces widgets faster but station B (the bottleneck) can still only process them at the same rate, all you've done is create a pile of unfinished widgets between A and B. Inventory goes up. Lead time goes up. The people at station B are now drowning. The pile creates confusion about what to work on next. Quality tanks because everyone's triaging instead of thinking.

> You didn't speed anything up. You created a traffic jam and called it productivity.

## The horror show, or: what actually happens when you "3x code output"

I bet some of you are already living this. I've lived it. It sucked.

Your developers are producing PRs faster than ever. Great. Wonderful. Gold star. Someone get the confetti cannon. Now those PRs hit the review queue, and your reviewers haven't tripled. Nobody tripled the reviewers. Nobody even _thought_ about the reviewers, because the reviewers weren't in the vendor's slide deck.

So PRs sit. A day. Two days. A week. The author has context-switched to their next AI-assisted feature and can barely remember what the first one did by the time review comments land. "Can you explain what this function does?" they ask, staring at code they wrote eight days ago, which in developer memory is roughly the Jurassic period.

Reviews start getting rubber-stamped because there are simply too damn many of them to review properly. Someone approves a PR they didn't really read. We've all done it (don't look at me like that). It merges. CI takes 45 minutes, fails on a flaky test, gets re-run, passes on the second attempt (the flaky test is fine, it's always fine, until it isn't and you're debugging production at 2am on a Saturday in your underwear wondering where your life went wrong. Ask me how I know... actually, don't). The deploy pipeline requires a manual approval from someone who's in a meeting about meetings. The feature sits in staging for three days because nobody owns the "get it to production" step with any urgency.

Meanwhile, the developer has already shipped two more PRs. The queue grows. WIP goes through the roof. Everyone has six things in flight and nothing actually done. Cycle time (the thing that actually measures how fast you deliver value to users) gets _worse_.

You are producing more code and shipping less software. You have made your situation measurably, demonstrably worse, and you have a dashboard that says productivity is up 40%.

> Congratulations. You've built a factory that's world-class at producing inventory that sits on the floor and rots. Someone's getting promoted for this.

I have seen this exact movie play out at three different companies. The dashboard goes up. The shipping goes down. And nobody connects the two because the dashboard is the thing they're reporting to the board, and the board doesn't know what cycle time is, and nobody wants to be the person who explains it.

And here's the bit that really keeps me up at night: a lot of this AI-generated code? Nobody fully understands it. The person who "wrote" it didn't really write it. They prompted it, skimmed it, maybe ran it once. When it breaks in production at 2am, the person on-call didn't write it and the person who prompted it can't explain it. You've just increased the surface area for incidents while _decreasing_ the number of humans who can reason about the system.

> More code, less understanding. That's not a productivity gain. That's a time bomb with a nicer dashboard.

## So where's the actual bottleneck?

If it's not writing code (and it almost never is), then where should you be looking? Walk the value stream. Follow a feature from "someone had an idea" to "a user got value from it." I promise the bottleneck will jump out and wave at you - it might even flip you off because you've been ignoring it.

### 1. You don't know what to build

This is the one nobody wants to talk about because it's embarrassing. Your PM hasn't talked to a real user in two months. Your requirements arrive as a Jira ticket with three sentences and a Figma link to a design that was approved by someone who's never used the product. Your engineers are making fifty micro-decisions a day about behaviour, edge cases, and error handling that nobody specified, because nobody thought about them.

And they're _guessing_.

I once watched a team spend six weeks building a feature based on a Slack message from a sales rep who paraphrased what a prospect maybe said on a call. Six weeks. The prospect didn't even end up buying. The feature got used by eleven people, and nine of them were internal QA. That's not a delivery problem. That's an "oh fuck, what are we even doing" problem.

> And writing code faster just means you arrive at "oh fuck" sooner.

When you speed up code output in this environment, you are speeding up the rate at which you build the wrong thing. You have automated the guessing. You will build the wrong feature faster, ship it, watch it fail, and then do a retro where someone says "we need to talk to users more" and everyone nods solemnly and then absolutely nothing changes.

> The bottleneck is understanding the problem. No amount of faster typing fixes that.

### 2. Everything after the code is "done"

I put "done" in quotes because in most orgs, code being written is maybe 20% of the journey. The other 80% is your code sitting in various queues, slowly ageing, like a forgotten sandwich in the office fridge.

I've watched features where the code took an afternoon and it took two months to reach production. Two. Months. The code didn't get slower. Everyone around the code got in its way.

PR review. CI. Staging. QA. Security review. Product sign-off. Deploy window. Canary rollout. The actual pipeline of getting code from a developer's branch to a user's screen is a long series of handoffs, waits, and queues. Most of the time, your code is sitting still. Waiting for a human to look at it. Waiting for a pipeline to run. Waiting for someone to give it permission to exist.

If you've ever watched a PR approval come through at 4:55pm on a Friday and thought "well, that's shipping on Monday I guess," you know exactly what I'm talking about.

> If you've ever seen a "quick fix" take nine days to reach production and lost the will to live somewhere around day six... yeah, that. The code was done ages ago. Everything after it was the bottleneck.

If you want to ship faster, look at where things are _waiting_. Count the hours of actual work versus the hours of sitting in a queue. I guarantee the ratio will make you want to put your head through a wall.

### 3. The deploy trust spiral

I can't count the number of teams I've worked with that were scared to deploy. Tests are flaky, observability is a mess, nobody trusts the canary process, and the last time someone deployed on a Thursday it ruined everyone's weekend. So what do they do? They batch changes into bigger releases. Which are riskier. Which makes deploys scarier. Which makes everyone batch _more_.

> Congratulations, you've built a fear spiral.

Now add faster code output to this environment. More code, same terrified deploy culture. The batches get bigger. The risk gets higher. The releases get less frequent. You have given a team that was already scared of shipping even more reasons to not ship. Incredible work.

### 4. You shipped. Did it work? Who knows.

This one pairs with "you don't know what to build" because it's the same disease on the other end of the pipeline. You built the thing. You shipped the thing. And then... nothing. No analytics worth looking at. No user interviews after launch. Nobody circling back to check whether the feature actually solved the problem it was supposed to solve.

So you guess on the next feature too. And the one after that. The entire product roadmap is a series of educated guesses with no feedback between them.

> Faster code output in this environment just means you're spinning the "build, ship, shrug" cycle faster.

You arrive at "we have no idea if this worked" more often, learn nothing each time, and somehow call that velocity.

### 5. Your calendar is a load-bearing wall

Sometimes the bottleneck isn't technical at all. It's the meeting you need to get a decision. The three teams who need to agree on an API contract but haven't talked to each other in a month. The architect who's a single point of approval on every significant design choice and has a two-week backlog because apparently we built a system where one person's calendar is a load-bearing wall. Or my personal favourite: the planning process that takes six weeks, runs quarterly, and means you can't start working on something urgent for another five weeks because "it wasn't in the plan."

> I have sat in rooms where the entire discussion was about why a feature hasn't shipped yet, and the answer was literally "we're waiting for a meeting with someone who's on holiday."

Not a technical problem. Not a code problem. A calendar problem. We spent more time _talking about_ the feature than building it. At one point someone suggested we have a meeting to discuss the meeting. I wish I was joking. Now I need a shower, and some whiskey.

These are coordination problems. Human problems. Messy, political, _nobody-wants-to-own-them_ problems.

Writing code faster does precisely nothing for any of this. Zero. Your bottleneck is the org chart, and no amount of Copilot is going to refactor that.

## What to do instead (the unsexy part)

You knew this section was coming. The boring bit. I'm not going to pretend this is glamorous, because it isn't. Nobody's going to write a LinkedIn post about it. Nobody's going to give a keynote about it at a vendor conference. There's no swag.

Here goes:

**Map your value stream.** Literally follow a feature from idea to production. Write down every step. Write down how long each step takes. Write down how long things sit _between_ steps. The gap between steps is where your cycle time lives. This will be depressing. Do it anyway. Bring snacks.

**Measure cycle time, not output.** If you're measuring lines of code, PRs merged, or "story points delivered" and not measuring how long it takes from commit to production to users using it, you're optimising for the wrong thing. You're counting widgets at station A and ignoring the pile on the floor. Stop it. I mean it.

**Find the wait states and kill them.** If PRs wait two days for review, fix review. Pair programming, smaller PRs, dedicated review time, async review norms, whatever works for your team. If deploys wait for a manual approval, automate it or at least make it a Slack button instead of a calendar invite. If decisions wait for a meeting, make smaller decisions that don't need meetings.

**Stop starting and start finishing.** WIP limits exist for a reason. It's better to have three things done than ten things in progress. Every item in flight is context-switching tax, and context-switching is where good engineers go to slowly lose their minds and start writing manifestos on internal wikis that nobody reads.

**Talk to the people doing the work.** Your developers already know where the bottleneck is. They complain about it in standups. They've been making memes about it in Slack for months. They just assumed nobody was listening, and honestly? They were probably right.

## The point

Go back to that Tuesday morning. Your VP is up there with their slide about 40% more code output. What they should have said, what would have actually been useful, is this: "We did a value stream analysis and found that features spend an average of nine days waiting between steps. We're going to cut that in half."

That's not sexy. It doesn't fit on a vendor's slide deck. You can't sell it as a product. There's probably no conference talk in it (actually, this is giving me ideas...). But it's the thing that would actually make you ship faster.

The speed of writing code was never your problem. If you thought it was, the gap between that belief and reality is where all your actual problems live. The competitive advantage doesn't go to the team that writes code fastest. It goes to the team that figured out what to build, built it, and got it into users' hands while everyone else was still drowning in a review queue full of AI-generated PRs that nobody has the time or the energy to read.

> Fix the bottleneck. It's not the keyboard.
