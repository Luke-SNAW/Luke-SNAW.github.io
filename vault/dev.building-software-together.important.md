---
id: 186lrn3wlhoxnrbvko6ge2p
title: "Chapter 2: The Important Stuff"
desc: ""
updated: 1663223794711
created: 1662531230396
---

> https://buildtogether.tech/important/

The worst mistakes people make are related to people, not software, so before we look at version control or testing, we need to talk about overwork, meetings, and resolving arguments.

> ### Not writing software takes less time
>
> [[Sedano2017](https://buildtogether.tech/bibliography/#Sedano2017)] found that software development projects have nine types of waste: building the wrong feature or product, mismanaging the backlog, rework, unnecessarily complex solutions, extraneous cognitive load ([Appendix F](https://buildtogether.tech/thinking/)), psychological distress, waiting and multitasking, knowledge loss, and ineffective communication. _None of these are software issues,_ so if you only think about the code in your project and not about the people writing it, everything will take longer and hurt more than it needs to.

## Crunch Mode

I can't remember who I was trying to impress. Instead, what I remember is how much of the code I wrote in those all-nighters I threw away once I'd had some sleep. My mistake was to confuse "long hours" with "getting things done". You can't produce software (or anything else) without doing some work, but you can easily do lots of work without producing anything of value. Scientific study of overwork goes back to at least the 1890s—see [[Robinson2005](https://buildtogether.tech/bibliography/#Robinson2005)] for a short, readable summary. The most important results are:

1. Working more than eight hours a day for more than a couple of weeks of time lowers your total productivity, not just your hourly productivity—i.e., you get less done _in total_ in [crunch mode](https://buildtogether.tech/glossary/#crunch_mode) than when you work regular hours.
2. Working over 21 hours in a stretch increases the odds of you making a catastrophic error just as much as being legally drunk.

These facts have been verified through hundreds of experiments over the course of more than a century, including some on novice software developers [[Fucci2020](https://buildtogether.tech/bibliography/#Fucci2020)]. The data behind them is as solid as the data linking smoking to lung cancer. However, while most smokers will at least acknowledge that their habit is killing them, people in the software industry still talk and act as if they were somehow immune to science. To quote Robinson's article:

> When Henry Ford famously adopted a 40-hour workweek in 1926, he was bitterly criticized by members of the National Association of Manufacturers. But his experiments, which he'd been conducting for at least 12 years, showed him clearly that cutting the workday from ten hours to eight hours—and the workweek from six days to five days—increased total worker output and reduced production cost… the core of his argument was that reduced shift length meant more output.
>
> …many studies, conducted by businesses, universities, industry associations and the military, …support the basic notion that, for most people, eight hours a day, five days per week, is the best sustainable long-term balance point between output and exhaustion. Throughout the 30s, 40s, and 50s, these studies were apparently conducted by the hundreds; and by the 1960s, the benefits of the 40-hour week were accepted almost beyond question in corporate America. In 1962, the Chamber of Commerce even published a pamphlet extolling the productivity gains of reduced hours.
>
> But, somehow, Silicon Valley didn't get the memo…

I spent two years at a data visualization startup. Three months before our first release, the head of development "asked" us to start coming in on Saturdays. We were already pulling one late night a week at that point (without overtime pay—our boss seemed to think that ten dollars' worth of pizza was adequate compensation for four hours of work) and most of us were also working at least a couple of hours at home in the evenings. To no one's surprise, we missed our "can't miss" deadline by ten weeks, and had to follow up our 1.0 release with a 1.1 and then a 1.2 to fix the crash-and-lose-data bugs we'd created. We were all zombies, and zombies can't code.

Hours like these are sadly still normal in many parts of the software industry, and may actually be worse now that so many people are working from home. Designing and building software is a creative act that requires a clear head; it only takes a couple of minutes to create a bug that will take hours to track down later. As Robinson writes:

> Productivity varies over the course of the workday, with the greatest productivity occurring in the first four to six hours. After enough hours, productivity approaches zero; eventually it becomes negative.

It's hard to quantify the productivity of programmers, testers, and UI designers [[Sadowski2019b](https://buildtogether.tech/bibliography/#Sadowski2019b), [Forsgren2021](https://buildtogether.tech/bibliography/#Forsgren2021)], but five eight-hour days per week has been proven to maximize long-term total output in every industry that has ever been studied. There is no reason to believe that ours is any different.

Ah, you say, but that's _long-term_ output. What about short bursts now and then, like pulling an all-nighter to meet a deadline? That's been studied too, and the results aren't pleasant. Your ability to think drops by 25 points for each 24 hours you're awake. Put it another way, the average person's IQ is only 75 after one all-nighter, which puts them in the bottom 5% of the population. Two all nighters in a row and their effective IQ is 50—the level at which people are considered incapable of independent living.

The catch in all of this is that people usually don't notice their abilities declining. Just like drunks who think they're still able to drive, people who are deprived of sleep don't realize that they're not finishing their sentences (or thoughts). They certainly don't realize that they're calling functions with parameters in the wrong order or that the reason the tests are failing is that they've forgotten to redeploy the application—again.

The first and most important lesson in this chapter is therefore to think very hard about what's more important—how much you produce or how much of a martyr you appear to be—and to pace yourself accordingly.

## Time Management

... Should you tackle one thing that is high effort and high importance or three things that are individually less important but require the same total effort? Laying things out on a grid can't answer that question, but at least it can tell you what the question is.

> How to prioritize: always finish first the tasks that will allow other people to continue/start/finish their work. — Yanina Bellini Saibene

> ### Open offices suck
>
> Open offices were created so that (mostly male) managers could keep an eye on (mostly female) office workers, and to reduce air conditioning costs [[Eley1995](https://buildtogether.tech/bibliography/#Eley1995)]. They lower productivity in every other way we can measure [[Bernstein2018](https://buildtogether.tech/bibliography/#Bernstein2018)]; sadly, the same is true of other interruption-rich environments like your favorite coffee shop. If you really want to be productive, you should avoid both.

Finally, you will be more productive in the long run if your back doesn't ache, and being away from the keyboard gives your brain a chance to reflect on what you've just been doing. You should therefore take a five-minute break every hour. Checking email doesn't count: get up and stretch, refill your water bottle, or go and restack the dishwasher. You'll be amazed at how often you can solve a problem that's been baffling you for an hour by taking a short walk…

## Meetings

The previous section explained how to be productive individually, but what about being productive with others? The most important thing is running meetings efficiently, and the key to doing that is to distinguish between:

- [Status meetings](https://buildtogether.tech/glossary/#status_meeting) for keeping everyone up to date on what everyone else is doing and for making simple decisions when the options are well understood.
- [Discussion meetings](https://buildtogether.tech/glossary/#discussion_meeting) for weighing alternatives and making complex decisions.
- Co-working sessions like brainstorming sessions and programming sprints that are devoted to the content of the project rather than its operation.

### Status Meetings

Every team should have a short weekly status meeting. For each meeting, create a table in a shared document like the one in [Table 2.1](https://buildtogether.tech/important/#important-status).  
…

> ### Are you a blowfish or a clam?
>
> [NOAA's guide](https://coast.noaa.gov/ddb/) to dealing with disruptive behaviors has useful labels and even more useful advice for handling people who may send meetings off course.

### Decision Meetings

Decision meetings are for issues that will have more long-term impact on the project or that team members disagree about. Since the stakes are higher, they need more structure:

**Decide if there actually needs to be a meeting.**

If the only purpose is to share information, send a brief email instead: most people can read faster than they can speak.

**Write an agenda.**

If nobody cares enough about the meeting to prepare a point-form list of what's to be discussed, the meeting probably doesn't need to happen. (Note that "the agenda is all the open issues in our GitHub repo" doesn't count.)

**Include timings in the agenda.**

Doing this helps prevent early items stealing time from later ones. The first estimates with any new group are inevitably optimistic, so expect to revise them upward for subsequent meetings. But don't have second or third meeting just because the first one ran over time: instead, try to figure out _why_ it ran over and fix the underlying problem.

**Select a moderator.**

Put one person in charge of keeping items on time, selecting the next person to speak, chiding people who are having side conversations or checking email, and asking people who are talking too much to get to the point. The moderator should _not_ do all the talking: in fact, the moderator will talk less in a well-run meeting than most other participants.

**Prioritize.**

Tackle the most important issues first, even if they're the longest, because the little ones always take more time than you expect.

**Require politeness.**

No one gets to be rude, no one gets to ramble, and if someone goes off topic, it's the moderator's job to say, "Let's discuss that elsewhere."

**No interruptions.**

This rule is a special case of the one above, since treating other people with respect is the sincerest form of politeness. Participants should raise a hand (physically or electronically) when they want to speak. The moderator should keep track of the queue and give each person time in turn.

**No distractions.**

Side conversations make meetings less efficient because nobody can actually pay attention to two things at once. More importantly, if someone is checking their email or texting a friend during a meeting, it's a clear signal that they don't think the speaker or their work is important. This doesn't mean a complete ban on technology—people may need accessibility aids or be waiting for a call about childcare—but by default phones should be face down and laptops should be closed during in-person meetings.

**Take minutes.**

As discussed below, someone other than the moderator should take point-form notes about the most important information that was shared and about every decision that was made or every task that was assigned to someone.

**End early.**

If the meeting is scheduled for 10:00--11:00, aim to end at 10:50 to give people a break before whatever they're doing next.

As soon as the meeting is over, add the minutes to the project's wiki, version control repository, or shared cloud drive. Please don't email minutes to everyone: our inboxes are full enough, and the more places new team members need to search in order to find things, the more likely they are to miss something important.

Sharing the minutes ensures that:

**People who weren't at the meeting can follow what's going on.**

We all have to juggle tasks from several projects or courses, which means that sometimes we can't make it to meetings. Checking a shared record is more accurate and more efficient than asking a colleague, "What did I miss?"

**Everyone can check what was actually said or promised.**

Accidentally or not, people often remember things differently; writing them down gives everyone a chance to correct mistakes and misinterpretations.

**People can be held accountable.**

Whoever has to draw up the agenda for the next meeting can start with the action items from the previous one.

If you would like to become better at sharing information and making decisions, there is no better place to start than [[Brookfield2016](https://buildtogether.tech/bibliography/#Brookfield2016)], which catalogs fifty different techniques for managing discussions and explains when and how each is useful.

## Air Time

One problem with meetings is that some people may talk far more than others. Other people may be so accustomed to this that they don't speak up even when they have valuable points to make.

...

## Making Decisions

The first release of GitHub's [Minimum Viable Governance](https://github.com/github/MVG) guidelines included this:

> **2.1. Consensus-Based Decision Making** Projects make decisions through consensus of the Maintainers. While explicit agreement of all Maintainers is preferred, it is not required for consensus. Rather, the Maintainers will determine consensus based on their good faith consideration of a number of factors, including the dominant view of the Contributors and nature of support and objections. The Maintainers will document evidence of consensus in accordance with these requirements.

It sounds reasonable, but it is harmfully wrong. Every team has a power structure: the question is whether it's formal or informal—in other words, whether it's accountable or unaccountable [[Freeman1972](https://buildtogether.tech/bibliography/#Freeman1972)]. In the latter case, decisions will effectively be made by the people who are the most self-confident or stubborn rather than by those with the most insight.

To guard against this, groups need to spell out who has the authority to make which decisions and how to achieve consensus. In short, they need explicit [governance](https://buildtogether.tech/glossary/#governance).

[Martha's Rules](https://buildtogether.tech/glossary/#marthas_rules) [[Minahan1986](https://buildtogether.tech/bibliography/#Minahan1986)] are a practical way to do this in groups of up to a few dozen people, and work very well for smaller teams too:

1. Before each meeting, anyone who wishes may sponsor a proposal. Proposals must be filed at least 24 hours before a meeting in order to be considered, and must include:

   - a one-line summary
   - the full text of the proposal
   - any required background information
   - pros and cons
   - possible alternatives

2. A quorum is established in a meeting if half or more of voting members are present.
3. Once a person has sponsored a proposal, the group may not discuss or vote on the issue unless the sponsor or their delegate is present.
4. After the sponsor presents the proposal a [sense vote](https://buildtogether.tech/glossary/#sense_vote) is cast:

   - Thumbs up: who likes the proposal?
   - Thumbs down: who is uncomfortable with the proposal?
   - Thumbs sideways: who can live with?

5. If everyone likes or can live with the proposal, it passes with no further discussion.
6. If the majority is uncomfortable with the proposal, it is sent back to its sponsor for further work. (The sponsor may decide to drop it if it's clear the majority isn't ever going to support it.)
7. Otherwise, the group has a brief moderated discussion. After 10 minutes, or when no one has anything further to add, the moderator calls for a straight yes-or-no vote on the proposal. If a majority votes "yes" it is adopted; otherwise, it is returned to the sponsor for further work.

...
