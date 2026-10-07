
> Richard P. Gabriel
>
> Lucid, Inc
>
> https://www.dreamsongs.com/RiseOfWorseIsBetter.html

---

This article discusses two contrasting design philosophies in programming: the MIT approach, which emphasizes achieving the "right thing" with complex, ideal solutions, and the New Jersey approach, characterized by simplicity and practicality. The author argues that while the MIT philosophy leads to well-designed systems like Common Lisp and Scheme, the New Jersey approach, exemplified by early Unix and C, offers better survival characteristics in software development. A key example illustrates a discussion between an MIT and a New Jersey programmer about handling system routine errors, highlighting the New Jersey approach's focus on simplicity over complexity.

The author posits that the worse-is-better philosophy prioritizes implementation simplicity, making systems easier to port and use on a variety of machines, thus allowing for widespread adoption. This philosophy conditions programmers to accept some trade-offs in safety and convenience for enhanced performance. The article suggests that while Lisp compilers were competitive with C compilers, the latter gained more traction due to their practicality.

The author concludes that the quest for the "right thing" often results in overly complex systems that take a long time to develop and may only run on advanced hardware. Instead, a more effective strategy is to release a simpler, albeit imperfect solution first, allowing it to gain popularity before iterating towards improvement. Ultimately, the article calls for a reevaluation of the Lisp community's design approach.

- **Design Philosophies**: The document contrasts two design philosophies: the "MIT approach," which emphasizes achieving the ideal solution, and the "New Jersey approach," which prioritizes simplicity and practicality.
- **Worse-is-Better**: The "worse-is-better" philosophy asserts that simpler, less perfect designs can be more successful and widely adopted than more complex, ideal solutions.
- **Survival of Designs**: Despite its flaws, the worse-is-better philosophy tends to have better survival characteristics in software development compared to the idealistic MIT approach.
- **Real-World Examples**: Early Unix and C exemplify the New Jersey approach, demonstrating how simplicity in design can lead to widespread adoption and functionality across various hardware.
- **Portability**: The simplicity of Unix and C allows them to be easily ported to less powerful machines, making them more versatile and widely used.
- **User Conditioning**: Users of worse-is-better systems become accustomed to accepting less-than-ideal functionality, which can facilitate the spread of such systems.
- **Incremental Improvement**: Once a simpler system gains traction, there is potential for gradual improvement towards a more complete solution without overwhelming complexity.
- **Complexity of Ideal Solutions**: The document highlights that pursuing the ideal solution can lead to prolonged development times and complexity, often resulting in software that is difficult to implement and run.
- **Integration Tradition**: The New Jersey approach fosters a culture of component reuse, leading to better integration in software systems.
- **Rethinking Lisp Design**: The author suggests that the Lisp community should reconsider its design philosophy in light of the success of simpler, more pragmatic systems like C and Unix.

---

{an excerpt from "Lisp: Good News, Bad News, How to Win Big." [html](https://www.dreamsongs.com/WIB.html)}

## 2.1 The Rise of _Worse is Better_

I and just about every designer of Common Lisp and CLOS has had extreme exposure to the MIT/Stanford style of design. The essence of this style can be captured by the phrase _the right thing_. To such a designer it is important to get all of the following characteristics right:

- Simplicity -- the design must be simple, both in implementation and interface. It is more important for the interface to be simple than the implementation.
- Correctness -- the design must be correct in all observable aspects. Incorrectness is simply not allowed.
- Consistency -- the design must not be inconsistent. A design is allowed to be slightly less simple and less complete to avoid inconsistency. Consistency is as important as correctness.
- Completeness -- the design must cover as many important situations as is practical. All reasonably expected cases must be covered. Simplicity is not allowed to overly reduce completeness.

I believe most people would agree that these are good characteristics. I will call the use of this philosophy of design the _MIT approach_. Common Lisp (with CLOS) and Scheme represent the MIT approach to design and implementation.

The worse-is-better philosophy is only slightly different:

- Simplicity -- the design must be simple, both in implementation and interface. It is more important for the implementation to be simple than the interface. Simplicity is the most important consideration in a design.
- Correctness -- the design must be correct in all observable aspects. It is slightly better to be simple than correct.
- Consistency -- the design must not be overly inconsistent. Consistency can be sacrificed for simplicity in some cases, but it is better to drop those parts of the design that deal with less common circumstances than to introduce either implementational complexity or inconsistency.
- Completeness -- the design must cover as many important situations as is practical. All reasonably expected cases should be covered. Completeness can be sacrificed in favor of any other quality. In fact, completeness must be sacrificed whenever implementation simplicity is jeopardized. Consistency can be sacrificed to achieve completeness if simplicity is retained; especially worthless is consistency of interface.

Early Unix and C are examples of the use of this school of design, and I will call the use of this design strategy the _New Jersey approach_. I have intentionally caricatured the worse-is-better philosophy to convince you that it is obviously a bad philosophy and that the New Jersey approach is a bad approach.

However, I believe that worse-is-better, even in its strawman form, has better survival characteristics than the-right-thing, and that the New Jersey approach when used for software is a better approach than the MIT approach.

Let me start out by retelling a story that shows that the MIT/New-Jersey distinction is valid and that proponents of each philosophy actually believe their philosophy is better.

Two famous people, one from MIT and another from Berkeley (but working on Unix) once met to discuss operating system issues. The person from MIT was knowledgeable about ITS (the MIT AI Lab operating system) and had been reading the Unix sources. He was interested in how Unix solved the PC loser-ing problem. The PC loser-ing problem occurs when a user program invokes a system routine to perform a lengthy operation that might have significant state, such as IO buffers. If an interrupt occurs during the operation, the state of the user program must be saved. Because the invocation of the system routine is usually a single instruction, the PC of the user program does not adequately capture the state of the process. The system routine must either back out or press forward. The right thing is to back out and restore the user program PC to the instruction that invoked the system routine so that resumption of the user program after the interrupt, for example, re-enters the system routine. It is called _PC loser-ing_ because the PC is being coerced into _loser mode_, where _loser_ is the affectionate name for _user_ at MIT.

The MIT guy did not see any code that handled this case and asked the New Jersey guy how the problem was handled. The New Jersey guy said that the Unix folks were aware of the problem, but the solution was for the system routine to always finish, but sometimes an error code would be returned that signaled that the system routine had failed to complete its action. A correct user program, then, had to check the error code to determine whether to simply try the system routine again. The MIT guy did not like this solution because it was not the right thing.

The New Jersey guy said that the Unix solution was right because the design philosophy of Unix was simplicity and that the right thing was too complex. Besides, programmers could easily insert this extra test and loop. The MIT guy pointed out that the implementation was simple but the interface to the functionality was complex. The New Jersey guy said that the right tradeoff has been selected in Unix -- namely, implementation simplicity was more important than interface simplicity.

The MIT guy then muttered that sometimes it takes a tough man to make a tender chicken, but the New Jersey guy didn’t understand (I’m not sure I do either).

Now I want to argue that worse-is-better is better. C is a programming language designed for writing Unix, and it was designed using the New Jersey approach. C is therefore a language for which it is easy to write a decent compiler, and it requires the programmer to write text that is easy for the compiler to interpret. Some have called C a fancy assembly language. Both early Unix and C compilers had simple structures, are easy to port, require few machine resources to run, and provide about 50%-80% of what you want from an operating system and programming language.

Half the computers that exist at any point are worse than median (smaller or slower). Unix and C work fine on them. The worse-is-better philosophy means that implementation simplicity has highest priority, which means Unix and C are easy to port on such machines. Therefore, one expects that if the 50% functionality Unix and C support is satisfactory, they will start to appear everywhere. And they have, haven’t they?

Unix and C are the ultimate computer viruses.

A further benefit of the worse-is-better philosophy is that the programmer is conditioned to sacrifice some safety, convenience, and hassle to get good performance and modest resource use. Programs written using the New Jersey approach will work well both in small machines and large ones, and the code will be portable because it is written on top of a virus.

It is important to remember that the initial virus has to be basically good. If so, the viral spread is assured as long as it is portable. Once the virus has spread, there will be pressure to improve it, possibly by increasing its functionality closer to 90%, but users have already been conditioned to accept worse than the right thing. Therefore, the worse-is-better software first will gain acceptance, second will condition its users to expect less, and third will be improved to a point that is almost the right thing. In concrete terms, even though Lisp compilers in 1987 were about as good as C compilers, there are many more compiler experts who want to make C compilers better than want to make Lisp compilers better.

The good news is that in 1995 we will have a good operating system and programming language; the bad news is that they will be Unix and C++.

There is a final benefit to worse-is-better. Because a New Jersey language and system are not really powerful enough to build complex monolithic software, large systems must be designed to reuse components. Therefore, a tradition of integration springs up.

How does the right thing stack up? There are two basic scenarios: the _big complex system scenario_ and the _diamond-like jewel_ scenario.

The _big complex system_ scenario goes like this:

First, the right thing needs to be designed. Then its implementation needs to be designed. Finally it is implemented. Because it is the right thing, it has nearly 100% of desired functionality, and implementation simplicity was never a concern so it takes a long time to implement. It is large and complex. It requires complex tools to use properly. The last 20% takes 80% of the effort, and so the right thing takes a long time to get out, and it only runs satisfactorily on the most sophisticated hardware.

The _diamond-like jewel_ scenario goes like this:

The right thing takes forever to design, but it is quite small at every point along the way. To implement it to run fast is either impossible or beyond the capabilities of most implementors.

The two scenarios correspond to Common Lisp and Scheme.

The first scenario is also the scenario for classic artificial intelligence software.

The right thing is frequently a monolithic piece of software, but for no reason other than that the right thing is often designed monolithically. That is, this characteristic is a happenstance.

The lesson to be learned from this is that it is often undesirable to go for the right thing first. It is better to get half of the right thing available so that it spreads like a virus. Once people are hooked on it, take the time to improve it to 90% of the right thing.

A wrong lesson is to take the parable literally and to conclude that C is the right vehicle for AI software. The 50% solution has to be basically right, and in this case it isn’t.

But, one can conclude only that the Lisp community needs to seriously rethink its position on Lisp design. I will say more about this later.

---

## HN

### [d0mine](https://news.ycombinator.com/item?id=41770603)

There is also "satisficing" (vs. maximizing).

Your model of the world is not perfect so instead of trying to find a globally optimal solution, you are satisfied with a local optimum that exceeds some threshold that has to suffices.

https://en.wikipedia.org/wiki/Satisficing
