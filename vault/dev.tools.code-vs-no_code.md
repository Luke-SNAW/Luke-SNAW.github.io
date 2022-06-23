---
id: ja7ebcppxm73uxmqol3tkug
title: Code Vs No-code
desc: ""
updated: 1655971556995
created: 1655970734509
---

> https://jasonmorrissc.github.io/post/2022-02-24_no-code/  
> https://news.ycombinator.com/item?id=31843378

There was a conversation on Twitter this week that helped to clarify my thinking about something, and I wanted to share.

There is a sort of tension between “code” and “no-code” (sometimes “low-code”) solutions.

People who consider themselves software developers see people trying to use no-code solutions to do things that the no-code solutions are not good at, and they get frustrated that the capabilities of those tools has been overestimated.

They are taking something that is really happening, and they are interpreting it really wrong. It’s useful and important to understand how, and why.

### The Complexity/Effort Curve

Let’s simplify the world, and pretend that effort is a single dimension, where things are always “harder” or “easier” along a single spectrum. Let’s also simplify the world and pretend that the complexity of the software project is also on a single dimension that goes from “simple” to “complex.” Neither of these things is true, but it helps to pretend.

If those things are true, then each software tool, whether a programming language, an app, or a no-code solution that sits somewhere in the middle between the two, has an effort/complexity curve. This line maps how difficult it is to use this tool for a task of the given complexity.

All tools are going to have a line with a positive correlation, but the shape of the line will differ. If a tool is very hard to learn, but very powerful, it will start high, and flatten out faster. Like, say, a programming language.

![](https://jasonmorrissc.github.io/code_graph.png)

If a tool is easy to learn, and useful for simple things, but the simplifications become obstacles when you get into higher complexity, then the line will start low, and accellerate upward. Like, say, a no-code solution.

![](https://jasonmorrissc.github.io/no_code_graph.png)

Now, if you are a person who knows both programming languages and no code tools, this seems like a simple problem. The combination of the two lines looks like this, and you can see the level of complexity at which they cross.

![](https://jasonmorrissc.github.io/both_graph.png)

This is why programmers who are familiar with no-code tools say things like “people overestimate what these tools can do.” Because they see people on the right side of the dotted line, using no-code solutions, and they assume that the person must misunderstand where the orange line actually lies.

That’s not what’s happening. In the mind of the person who uses no-code tools and is not a programmer, this is what’s happening.

![](https://jasonmorrissc.github.io/what_they_know.png)

They don’t know the shape of the curve for programming, because _that_ is the thing they _haven’t_ used. They may not understand the curve for no-code tools perfectly, but they definitely understand it better.

Given that information, what decision would you make?

You would obviously use the tool you have.

But even if we could educate people on the positions of the relative curves, the vertical dotted line represents best alternative in the abstract. It does not reflect the thing that the person actually cares about. If they are looking at doing something that is slightly beyond the point where using the no code tool is the best option, they are worried about new effort, not existing effort. They know how hard it is to do the things they have done before, and they are willing for future things to be at least that hard.

There is an increased amount of effort that they are willing to go through to get to this new level of complexity, and for each tool, they have a comfort level.

So if you imagine a person who has used the no-code tool for something before, but has never used code before, how do they do the math?

![](https://jasonmorrissc.github.io/new_effort.png)

If you are trying to minimize the discomfort of not knowing what you are doing, you will continue to use the tools you know long after they are no longer the best tools for the job. And the each time you do it, you reduce the apparent cost of using the same tool again.

## So What Do We Do?

We need to tell people where the blue line is, right? We need to educate people better about what tools are good for what.

Sorry, no. Educate all you want, it doesn’t change the fact that in the beginning, the harder tools are harder. No one starts on the black diamond slope. Everyone starts on the bunny slope. People with high tolerance for the difficulty of learning programming are already well served by what we have, and people with a low tolerance for it will not be convinced if we merely insist.

You can _help_ solve this problem by making the curve more visible from the beginning. If you can show people the range of uses of the tool, from simple to complex, and that demonstration is meaningful, then great. But even then, you are going to need to overcome the fact that people do not generally want to start with the harder thing.

So in an ideal world, what we need is tools that have a effort/complexity curve that is both visible, and looks like this:

![](https://jasonmorrissc.github.io/ideal.png)

## How do you do it?

There are a lot of people a lot smarter than me working on that problem. If you’re interested, the [Future of Coding](https://futureofcoding.org/) community is one that has a lot to say on the topic.

There are two main problems. The first is how to get the beginning of the curve lower. That’s the problem that the people selling no-code solutions are tackling, and with real success. They are empowering people, and that is a thing people will pay for.

For that problem, some of the answers seem to be to specialize the tools to small problem domains, eliminate text as the primary user interface, and replace it with something that fits the domain of the problem. It is a design problem, and one that people have made a lot of progress on.

The other main problem is how do you avoid the making complexity more expensive?

This is less obvious. Domain specificity can help, because you can say “if you want more, go elsewhere”, and then combine tools that each do a small thing well. Tying no-code tools together, in a no-code way, is the basic idea behind tools like Zapier, which have been wildly successful. But people inevitably want to do more, and it becomes harder to support in the simplified interface.

Another possibility that I’m pursuing with Blawx is the idea that it doesn’t need to be just one tool. You can have the beginner’s no-code tool that teaches the person to use the advanced code tool. Blawx lets the user see what s(CASP) code is being written for them. In that way, using Blawx can teaches you s(CASP), and you are less trapped inside the tool you already know when you reach its limits. But commercial no-code solutions often do not want their customers to escape in this way, so it may not be realistic to expect from commercial no-code solutions.

Another possibility is a tool that modifies itself in sophistication along with the user. We could have “beginner mode” and “advanced mode”, and try to detect when the features of the advanced mode would help what the user is currently doing. Imagine a programming language that doesn’t introduce the concept of a function until after you type almost the same code twice.

I have seen nothing of the sort, it’s just an idea.

Another possibility is that programming languages already have a sort of optimal effort/complexity curve at the high complexity end, so if we can just lower the start of the curve for an actual programming language, that solves the problem.

You can paint efforts to teach programming to children into this box, to some degree. Or, efforts to teach programming at all. But even in the world of Scratch and Blockly, the people involved insist they are not trying to replace programming languages, they are trying to promote the learning of them. Ultimately, they expect people to type code into a development environment. That has always seemed like a lack of vision, to me.

No one, that I am aware of, is trying to build a programming language that scales in complexity all the way from good-for-kids to general-purpose programming language.

### The Point

The point is, if people are choosing to do something one way, and not the “better” way, the problem is never with the people, the problem is with the “better” way. People will do what costs the least, but the costs are measured in stress, ambiguity, effort, and human experience.

Consider a hammer. A hammer is designed to do a specific thing. In the context of that thing, how to use it is obvious. But more than that, when you pick it up, you can feel intuitively what you are capable of now that you weren’t without it. You can imagine using it to do simple things, and complicated things. And you can imagine, and maybe even aspire to, getting better at using it.

That is the experience that any software tool should aspire to. Obviously valuable, obviously scalable, intuitive. Learning it should feel like play.

The fact that we programmers, who lived in the sliver of time shortly after the invention of programming, managed to acquire the skills to deploy it, doesn’t mean it has reached its evolutionary apex. Programming can be much, much better than it is. But only if the people who already understand it can genuinely focus on the interests of the people who don’t, without the hubris of assuming that their aspiration should be to become like us.

It is undoubtedly possible to share the power we have, without forcing people through what we went through to gain it. Abstraction and formalization are irremediably hard to learn. Everything else can be made easier.

---

> No-code or low-code still means you're creating software, even if you're using a drag-and-drop UI to do so. And if you're building software, you're going to want things like version control, environments, code review, (test code) etc. Unfortunately, most of these tools have zero ability to do these things, or have really half-baked imitations of them, and as a result the apps you've built in no-code/low-code are unable to scale as your company grows.

> For no code to work one needs to be sure the framework can handle the requirements well, so customizations and workarounds wont be needed. To know the requirements sufficiently well one usually needs something in production, and years of experience with it. Why bother with no/low code then? If a more modern reimplementation is needed, it can be elegantly implemented in one of the bazzilion software stacks out there.  
> Another big disadvantage is lack of developers that like those kind of things and know them well. Those who do know those frameworks usually cost a lot more. Lots of those relatively niche things, such as mulesoft, are really just means to strengten the vendor lock in, and are sold to management, not engineering leads, on the premise of lessening the reliance on actual engineering. Which of course is a lie.

> I've worked a lot with no/low code solutions. There actually ended up being a lot of code! Surprise. Code is an interface between human desires and customising computers. There are infinite human desires, thus there will be a need for an interface that is 'code', even if it isn't a big file with scary ASCII characters.
>
> > My last project with a no-code solution was a visual designer where you flow-chart all the logic for workflows. At a very small scale, it might make sense but even for our meager need it was blown out so big that no one could really understand or modify it. And, worst of all, we were locked into this proprietary solution.  
> > In the end, I re-wrote the entire project in regular code and the end result works better and is easier to modify. We don't need to pay expensive consultants anymore. No extra licensing fee. No special software/server/hosting requirements. And any programmer can work on it -- I can even put new hires on it.
> >
> > > Rewrite in code is way easier than developing in code from scratch. I think your scenario reflects the main benefit of no-code, to let business users fix their own requirements.
> > >
> > > > In this case, this is absolutely true. All the requirements were well established and converting it was very quick because of it. But ultimately that doesn't matter because the reason the re-write was done was because the no-code solution failed in it's goal.
> > > > The process of developing this solution was funny. We had an absolutely fantastic team doing the requirements and the process was all agile except when it came to the tool itself. At that point, it turned into a waterfall project where everything had to be nailed down before the work was done.  
> > > > I can mock up a application form very fast so there's really no need for a tool to do that every so slightly faster but in a proprietary and limited way.

> I think “code” is already at the right layer of abstraction. “Code” already solves this problem and has the curve the author’s looking for. “No-code” is a simple case of the wrong abstraction.
>
> > It's all abstractions. Python code is no-C-code. C code is no-assembly-code. And so on...
