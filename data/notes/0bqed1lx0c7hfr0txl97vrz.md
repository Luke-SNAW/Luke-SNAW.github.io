
> It’s hard to learn, but your code will produce fewer nasty surprises  
> BY [Charles Scalfani](https://spectrum.ieee.org/u/charles_scalfani) 23 Oct 2022  
> https://spectrum.ieee.org/functional-programming

**You’d expect** the longest and most costly phase in the lifecycle of a software product to be the initial development of the system, when all those great features are first imagined and then created. In fact, the hardest part comes later, during the maintenance phase. That’s when programmers pay the price for the shortcuts they took during development.

So why did they take shortcuts? Maybe they didn’t realize that they were cutting any corners. Only when their code was deployed and exercised by a lot of users did its hidden flaws come to light. And maybe the developers were rushed. Time-to-market pressures would almost guarantee that their software will contain more bugs than it would otherwise.

---

The struggle that most companies have maintaining code causes a second problem: fragility. Every new feature that gets added to the code increases its complexity, which then increases the chance that something will break. It’s common for software to grow so complex that the developers avoid changing it more than is absolutely necessary for fear of breaking something. In many companies, whole teams of developers are employed not to develop anything new but just to keep existing systems going. You might say that they run a software version of the [Red Queen’s race](https://en.wikipedia.org/wiki/Red_Queen%27s_race), running as fast as they can just to stay in the same place.

It’s a sorry situation. Yet the current trajectory of the software industry is toward increasing complexity, longer product-development times, and greater fragility of production systems. To address such issues, companies usually just throw more people at the problem: more developers, more testers, and more technicians who intervene when systems fail.

Surely there must be a better way. I’m part of a growing group of developers who think the answer could be functional programming. Here I describe what functional programming is, why using it helps, and why I’m so enthusiastic about it.

## With functional programming, less is more

A good way to understand the rationale for functional programming is by considering something that happened more than a half century ago. In the late 1960s, a programming paradigm emerged that aimed to improve the quality of code while reducing the development time needed. It was called [structured programming](https://en.wikipedia.org/wiki/Structured_programming).

Various languages emerged to foster structured programming, and some existing languages were modified to better support it. One of the most notable features of these structured-programming languages was not a feature at all: It was the absence of something that had been around a long time— [the GOTO statement](https://en.wikipedia.org/wiki/Goto).

The GOTO statement is used to redirect program execution. Instead of carrying out the next statement in sequence, the flow of the program is redirected to some other statement, the one specified in the GOTO line, typically when some condition is met.

The elimination of the GOTO was based on what programmers had learned from using it—that it made the program very hard to understand. Programs with GOTOs were often referred to as spaghetti code because the sequence of instructions that got executed could be as hard to follow as a single strand in a bowl of spaghetti.

The inability of these developers to understand how their code worked, or why it sometimes didn’t work, was a complexity problem. Software experts of that era believed that those GOTO statements [were creating unnecessary complexity](https://dl.acm.org/doi/10.1145/362929.362947) and that the GOTO had to, well, go.

Back then, this was a radical idea, and many programmers resisted the loss of a statement that they had grown to rely on. The debate went on for more than a decade, but in the end, the GOTO went extinct, and no one today would argue for its return. That’s because its elimination from higher-level programming languages greatly reduced complexity and boosted the reliability of the software being produced. It did this by limiting what programmers could do, which ended up making it easier for them to reason about the code they were writing.

Although the software industry has eliminated GOTO from modern higher-level languages, software nevertheless continues to grow in complexity and fragility. Looking for how else such programming languages could be modified to avoid some common pitfalls, software designers can find inspiration, curiously enough, from their counterparts on the hardware side.

## Nullifying problems with null references

In designing hardware for a computer, you can’t have a resistor shared by, say, both the keyboard and the monitor’s circuitry. But programmers do this kind of sharing all the time in their software. It’s called shared global state: Variables are owned by no one process but can be changed by any number of processes, even simultaneously.

Now, imagine that every time you ran your microwave, your dishwasher’s settings changed from Normal Cycle to Pots and Pans. That, of course, doesn’t happen in the real world, but in software, this kind of thing goes on all the time. Programmers write code that calls a function, expecting it to perform a single task. But many functions have side effects that change the shared global state, [giving rise to unexpected consequences](https://softwareengineering.stackexchange.com/questions/148108/why-is-global-state-so-evil).

In hardware, that doesn’t happen because the laws of physics curtail what’s possible. Of course, hardware engineers can mess up, but not like you can with software, where just too many things are possible, for better or worse.

Another complexity monster lurking in the software quagmire is called a [null reference](https://en.wikipedia.org/wiki/Null_pointer), meaning that a reference to a place in memory points to nothing at all. If you try to use this reference, an error ensues. So programmers have to remember to check whether something is null before trying to read or change what it references.

Nearly every popular language today has this flaw. The pioneering computer scientist [Tony Hoare](http://www.cs.ox.ac.uk/people/tony.hoare/) introduced null references in the [ALGOL](https://en.wikipedia.org/wiki/ALGOL) language back in 1965, and it was later incorporated into numerous other languages. Hoare explained that he did this “simply because it was so easy to implement,” but today he considers it to be a “billion-dollar mistake.” That’s because it has caused countless bugs when a reference that the programmer expects to be valid is really a null reference.

Software developers need to be extremely disciplined to avoid such pitfalls, and sometimes they don’t take adequate precautions. The architects of structured programming knew this to be true for GOTO statements and left developers no escape hatch. To guarantee the improvements in clarity that GOTO-free code promised, they knew that they’d have to eliminate it entirely from their structured-programming languages.

History is proof that removing a dangerous feature can greatly improve the quality of code. Today, we have a slew of dangerous practices that compromise the robustness and maintainability of software. Nearly all modern programming languages have some form of null references, shared global state, and functions with side effects—things that are far worse than the GOTO ever was.

How can those flaws be eliminated? It turns out that the answer [has been around for decades](https://www.math-cs.gordon.edu/courses/cps323/LISP/lisp.html): purely functional programming languages.

Of the top dozen functional-programming languages, Haskell is by far the most popular, judging by the number of GitHub repositories that use these languages.

The first purely functional language to become popular, called [Haskell](https://www.haskell.org/), was created in 1990. So by the mid-1990s, the world of software development really had the solution to the vexing problems it still faces. Sadly, the hardware of the time often wasn’t powerful enough to make use of the solution. But today’s processors can easily manage the demands of Haskell and other purely functional languages.

Indeed, software based on pure functions is particularly well suited to modern [multicore CPUs](https://spectrum.ieee.org/the-trouble-with-multicore). That’s because pure functions operate only on their input parameters, making it impossible to have any interactions between different functions. This allows the compiler to be optimized to produce code that runs on multiple cores efficiently and easily.

As the name suggests, with purely functional programming, the developer can write only pure functions, which, by definition, cannot have side effects. With this one restriction, you increase stability, open the door to compiler optimizations, and end up with code that’s far easier to reason about.

But what if a function needs to know or needs to manipulate the state of the system? In that case, the state is passed through a long chain of what are called composed functions—functions that pass their outputs to the inputs of the next function in the chain. By passing the state from function to function, each function has access to it and there’s no chance of another concurrent programming thread modifying that state—another common and costly fragility found in far too many programs.

---

### Avoiding Null-Reference Surprises

**A comparison of Javascript and Purescript shows how the latter can help programmers avoid bugs.**

![](assets/images/a-comparison-of-javascript-and-purescript-shows-how-the-latter-can-help-programmers-avoid-bugs.webp)

---

Functional programming also has a solution to Hoare’s “billion-dollar mistake,” null references. It addresses that problem by disallowing nulls. Instead, there is a construct usually called _Maybe_ (or _Option_ in some languages). A _Maybe_ can be _Nothing_ or _Just_ some value. Working with _Maybe\_\_s_ forces developers to always consider both cases. They have no choice in the matter. They must handle the _Nothing_ case every single time they encounter a _Maybe_. Doing so eliminates the many bugs that null references can spawn.

Functional programming also requires that data be immutable, meaning that once you set a variable to some value, it is forever that value. Variables are more like variables in math. For example, to compute a formula, _y_ = _x_2 + 2_x_ – 11, you pick a value for _x_ and at no time during the computation of _y_ does _x_ take on a different value. So, the same value for _x_ is used when computing _x_2 as is used when computing 2_x_. In most programming languages, there is no such restriction. You can compute _x_2 with one value, then change the value of \_x_ before computing 2*x*. By disallowing developers from changing (mutating) values, they can use the same reasoning they did in middle-school algebra class.

Unlike most languages, functional programming languages are deeply rooted in mathematics. It’s this lineage in the highly disciplined field of mathematics that gives functional languages their biggest advantages.

Why is that? It’s because people have been working on mathematics for thousands of years. It’s pretty solid. Most programming paradigms, such as object-oriented programming, have at most half a dozen decades of work behind them. They are crude and immature by comparison.

> Imagine if every time you ran your microwave, your dishwasher’s settings changed from Normal Cycle to Pots and Pans. In software, this kind of thing goes on all the time.

Let me share an example of how programming is sloppy compared with mathematics. We typically teach new programmers to forget what they learned in math class when they first encounter the statement _x = x + 1_. In math, this equation has zero solutions. But in most of today’s programming languages, _x = x + 1_ is not an equation. It is a _statement_ that commands the computer to take the value of _x_, add one to it, and put it back into a variable called _x_.

**In functional programming, there are no statements, only _expressions_.** Mathematical thinking that we learned in middle school can now be employed when writing code in a functional language.

Thanks to functional purity, you can reason about code using algebraic substitution to help reduce code complexity in the same way you reduced the complexity of equations back in algebra class. In non-functional languages (imperative languages), there is no equivalent mechanism for reasoning about how the code works.

## Functional programming has a steep learning curve

Pure functional programming solves many of our industry’s biggest problems by removing dangerous features from the language, making it harder for developers to shoot themselves in the foot. At first, these limitations may seem drastic, as I’m sure the 1960s developers felt regarding the removal of GOTO. But the fact of the matter is that it’s both liberating and empowering to work in these languages—so much so that nearly all of today’s most popular languages have incorporated functional features, although they remain fundamentally imperative languages.

The biggest problem with this hybrid approach is that it still allows developers to ignore the functional aspects of the language. Had we left GOTO as an option 50 years ago, we might still be struggling with spaghetti code today.

To reap the full benefits of pure functional programming languages, you can’t compromise. You need to use languages that were designed with these principles from the start. Only by adopting them will you get the many benefits that I’ve outlined here.

But functional programming isn’t a bed of roses. It comes at a cost. Learning to program according to this functional paradigm is almost like learning to program again from the beginning. In many cases, developers must familiarize themselves with math that they didn’t learn in school. The required math isn’t difficult—it’s just new and, to the math phobic, scary.

More important, developers need to learn a new way of thinking. At first this will be a burden, because they are not used to it. But with time, this new way of thinking becomes second nature and ends up reducing cognitive overhead compared with the old ways of thinking. The result is a massive gain in efficiency.

But making the transition to functional programming can be difficult. My own journey doing so a few years back is illustrative.

I decided to learn Haskell—and needed to do that on a business timeline. This was the most difficult learning experience of my 40-year career, in large part because there was no definitive source for helping developers make the transition to functional programming. Indeed, no one had written anything very comprehensive about functional programming in the prior three decades.

> To reap the full benefits of pure functional programming languages, you can’t compromise. You need to use languages that were designed with these principles from the start.

I was left to pick up bits and pieces from here, there, and everywhere. And I can attest to the gross inefficiencies of that process. It took me three months of days, nights, and weekends living and breathing Haskell. But finally, I got to the point that I could write better code with it than with anything else.

When I decided that our company should switch to using functional languages, I didn’t want to put my developers through the same nightmare. So, I started building a curriculum for them to use, which became the basis for a book intended to help developers transition into functional programmers. In [my book](https://leanpub.com/fp-made-easier), I provide guidance for obtaining proficiency in a functional language called [PureScript](https://www.purescript.org/), which stole all the great aspects of Haskell and improved on many of its shortcomings. In addition, it’s able to operate in both the browser and in a back-end server, making it a great solution for many of today’s software demands.

While such learning resources can only help, for this transition to take place broadly, software-based businesses must invest more in their biggest asset: their developers. At my company, [Panoramic Software](http://www.panosoft.com/), where I’m the chief technical officer, we’ve made this investment, and all new work is being done in either PureScript or Haskell.

We started down the road of adopting functional languages three years ago, beginning with another pure functional language called [Elm](https://elm-lang.org/) because it is a simpler language. (Little did we know we would eventually outgrow it.) It took us about a year to start reaping the benefits. But since we got over the hump, it’s been wonderful. We have had no production runtime bugs, which were so common in what we were formerly using, [JavaScript](https://en.wikipedia.org/wiki/JavaScript) on the front end and Java on the back. This improvement allowed the team to spend far more time adding new features to the system. Now, we spend almost no time debugging production issues.

But there are still challenges when working with a language that relatively few others use—in particular, the lack of online help, documentation, and example code. And it’s hard to hire developers with experience in these languages. Because of that, my company uses recruiters who specialize in finding functional programmers. And when we hire someone with no background in functional programming, we put them through a training process for the first few months to bring them up to speed.

## Functional programming’s future

My company is small. It delivers software to governmental agencies to enable them to help veterans receive benefits from the [U.S. Department of Veteran’s Affairs](https://www.va.gov/). It’s extremely rewarding work, but it’s not a lucrative field. With razor-slim margins, we must use every tool available to us to do more with fewer developers. And for that, functional programming is just the ticket.

It’s very common for unglamorous businesses like ours to have difficulty attracting developers. But we are now able to hire top-tier people because they want to work on a functional codebase. Being ahead of the curve on this trend, we can get talent that most companies our size could only dream of.

I anticipate that the adoption of pure functional languages will improve the quality and robustness of the whole software industry while greatly reducing time wasted on bugs that are simply impossible to generate with functional programming. It’s not magic, but sometimes it feels like that, and I’m reminded of how good I have it every time I’m forced to work with a non-functional codebase.

One sign that the software industry is preparing for a paradigm shift is that functional features are showing up in more and more mainstream languages. It will take much more work for the industry to make the transition fully, but the benefits of doing so are clear, and that is no doubt where things are headed.
