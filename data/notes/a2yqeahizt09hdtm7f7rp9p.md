
> https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/  
> https://news.ycombinator.com/item?id=32745318

> This post explains my reasoning for migrating from Common Lisp to Julia as my primary programming language, after a few people have asked me to elaborate. This article is the product of my experiences and opinions, and may not reflect your own. Both languages are very well designed, and work well, so I encourage you to do your own research and form your own opinions about which programming languages work best for you.

## [From Python to Common Lisp](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#from_python_to_common_lisp)

I first started using Common Lisp in January of 2008. Before that, I was using Python for most of my programming tasks, and a colleague was ocassionally making fun of my code, re-implementing snippets in Common Lisp, as an unsuccessful attempt to help me see the light. I distinctly remember telling myself that I would never use such a language with so many parentheses and structure that was very much outside of the norm. I was using Python because it was easy and fast to get my ideas into working code.

One day, purely out of boredom, I started reading [Practical Common Lisp](https://gigamonkeys.com/book), a book introducing Common Lisp, which is still the oft-recommended introductory reference today. After only a few days, I found myself swimming in parentheses, fully content, and without even finishing the book. How did I go from one extreme to another? The answer was quite simple: even as a beginner to the language, I was _more_ productive than I was with years of Python experience, which speaks volumes in my opinion, given that Python is often boasted as being great for rapid application development.

From 2008 to 2022, I was writing my code exclusively in Common Lisp, every day. I was able to get my ideas into working code quickly and effectively. The interactivity that the language was built around from the ground up made that possible. There was no latency, or waiting for the language at all. I could live in a running Lisp image and iteratively define my programs from the inside out, or in whatever way I wanted to, with immediate feedback after each change. This interactive and iterative development workflow was especially important to me, given I am mainly a graphics programmer; I write game engines, games, graphics algorithms, procedurally-generated imagery, simulations, and other related applications.

## [From Common Lisp to Julia](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#from_common_lisp_to_julia)

After 7 years of developing software in Common Lisp, in 2015, I started to grow increasingly frustrated with various aspects of the language, which I will mention later, so I started looking for a secondary language, as to not keep all my eggs in the same basket, so to speak. It was at this time that I first heard about Julia. I read through the entire manual and I was impressed with everything it had to offer. It was though, still in its infancy, and I didn't pursue it any further.

Continuing to use Common Lisp, the next stop on the timeline is 2017, when [a notable Lisp figure made the announcement of switching to Julia](https://tamaspapp.eu/post/common-lisp-to-julia/). I am not a data scientist, but this post still made me look into Julia once more, and I actually tried using it this time. To cut a long story short, I'll just say that I had a very rough time, and encountered quite a few surprises due to the language not being stable yet (and a year away from its v1.0 release). Once again, I dismissed it, but I kept it around for quick REPL experiments every now and then, and to watch it progress as a language with each subsequent release.

2020 was a depressing year for a lot of people, being stuck inside due to the pandemic. It was also depressing for me, because a long-term project of mine, a game engine, was proving to be inadequate without a serious rewrite. This was the spark that ignited my transition as a programmer into other domains, although still graphics-related. As such, I began sketching out a simple graphics math library in Julia, but I didn't get very far before I started to miss Common Lisp. This was however, my first attempt at writing Julia code, and I was impressed with the language overall. I ended up going back to Common Lisp, writing various small utilities and graphics algorithms.

In 2022, I realized that I was going to be "stuck" using Common Lisp forever unless I accepted the loss of some language features not present in any other language, and especially not all of them combined in a single language. I studied a handful of programming languages, including, but not limited to Scheme, Racket, Raku, Go, and Rust. Rust was the only one on this list that I have studied for many years prior, but it was the popular language gaining a lot of traction, and I re-explored it to see if I could swallow it. The answer was "no", and a "no" to all the other languages I've tried.

In June of 2022, I forced myself to stop using Common Lisp, and wrote a small math library in Julia over a couple of weeks in my free time. In writing this library, it helped me to see just how similar Common Lisp and Julia are to each other, which isn't obvious at the surface level. I found myself appreciating it more than ever, and I went on to write another library that received a lot of positive feedback from the community. It is now September, and I still have not touched Common Lisp, nor do I have a desire to. Julia just seems to tick all the boxes for me.

## [Why I No Longer Use Common Lisp](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#why_i_no_longer_use_common_lisp)

Common Lisp is a fantastic language, but it just isn't for me. Most of the problems I have with the language are social issues more than technical issues. The combination of all of the following issues, are what led me to become increasingly frustrated with the language over time, in no particular order.

### [Editor support](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#editor_support)

Common Lisp is not a language that is designed to just be edited in any old text editor or IDE. It was designed for total interactivity with an iterative development workflow from the ground up. This goes much farther than incremental compilation or hot code reloading found in some other languages, Julia included. Features like CLOS and the Common Lisp condition system are very dynamic and interactive in nature.

For example, when an exceptional situation occurs, such as, but not limited to an error, the debugger "pops up" in your editor, where you can decide what to do. Such choices might be to inspect the state of local variables in any of the stack frames, evaluate arbitrary code in the context of any of the stack frames, and more. While the debugger is active, your program is basically in a "paused" state, and you are free to go and edit functions and other definitions, and then tell the debugger to continue execution of your program after such repairs are made. You can even do this completely programmatically, with or without unwinding the stack, to take full control over what should happen for an exceptional situation. Most other languages have this feature in the form of an "exception system", but they contain only a subset of what is possible with the Common Lisp condition system, and most notably, the call stack is unwound before you get the chance to handle an exception, which means it is too late and lacking context of how to properly handle it in most cases.

The Common Lisp inspector lets you visually traverse an object hierarchy, exploring every bit of detail about the state of your program, or changing their values, all built-in to your editor.

Compiling functions and other definitions is simply a key binding with the cursor over that definition in your editor. The result is instantaneous, and changes are seen by your running program immediately.

All of this fancy interactivity is made possible by an editor plugin, that far exceeds the scope of a Language Server Protocol server. As such, editor support is extremely lacking in any editor that is not Emacs. There _is_ support in other editors, but it is nowhere near as complete and convenient as it is in Emacs.

I don't really like to be forced to use a particular editing environment to program in a language. I am a Vim user at heart, and while there are similar plugins for Vim, they are very awkward to work with and only offer a subset of the abilities of the Emacs plugin. Emacs can also be made to behave similarly to Vim, but the complexity and mis-features of Emacs is still there rearing its ugly head when you least expect it. For years, I have had to deal with using Emacs as my editing environment, and I disliked every moment of it.

### [Language Evolution](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#language_evolution)

Common Lisp is not just a language; it is a document describing how to implement a language. As such, there are multiple implementations of this ANSI standard, each with their own set of features.

Writing portable Common Lisp can be difficult or impossible at times. One often needs to reach for portability libraries that unify the interface of particular features between the different implementations.

The fact that Common Lisp is a standard is both a blessing and a curse. Many developers consider this to be the former, as your code is much less likely to break over time. For others, it means that the language is frozen in time. For instance, it:

- predates Unicode
- makes no mention of threading
- does not mandate IEEE-754 floating-point encoding
- no foreign function interface (FFI) described
- no garbage-collection interface defined
- no networking support

and much more. All of these features are left to be implemented by third-party libraries, and if possible, portability libraries that allow them to function with a unified interface between all implementations of Common Lisp.

Additionally, the standard is incredibly hard to navigate, especially as a beginner trying to learn the language. In many places it is very ambiguous, or erroneous, and often leads to long debates in the Common Lisp communication forums.

### [Software Versioning and Deployment](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#software_versioning_and_deployment)

There is no built-in package[^1] manager for Common Lisp. Installing new software is done with a third-party library, that is usually included in each implementation of Common Lisp, but is not part of the language standard. Implementations often include very old versions of this software, so updating it with a local copy is often a good idea. Additionally, this software ([ASDF](https://asdf.common-lisp.dev/asdf.html)), does not handle downloading software from the Internet; all software must exist locally on your filesystem.

There exists another third-party piece of software, [Quicklisp](https://www.quicklisp.org/beta/), that wraps ASDF, and is used to download newer software versions from the Internet, forwarding the installation to the underlying ASDF utility.

Quicklisp, while it works well for the small open-source Common Lisp community, is far from ideal. It ships with one "dist" installed, the "quicklisp" dist. This is a collection of metadata that describes where the latest version of each package can be downloaded, and its dependencies. When you install a piece of software, you are installing it from the official Quicklisp dist repository, not from the upstream repository.

The Quicklisp dist is curated by the Quicklisp maintainer, who ensures that all software builds successfully (in isolation; no checks are done to ensure that a piece of software is compatible with other software in the same dist). The Quicklisp maintainer downloads software from upstream once every month or two, to be included in a dist. No versioning or compatibility information is taken into account; users just receive the latest version of a piece of software that may or may not be compatible with other software a developer uses with it.

Infact, Common Lisp developers rarely version their software at all, because they offload the responsibility of deployment to the Quicklisp maintainer, with nothing to be done on their part. This model is far from ideal for any serious developer in my honest opinion. You never know what version of your software users will receive, unless you submit a particular branch for Quicklisp to track, rather than the main branch of your repository. Even if you employ this approach, users of your "stable" software will be pulling in transitive dependencies that may not employ this approach, and there is practically no way for you to deploy your software with compatibile dependencies without maintaining your very own Quicklisp dist. Most users will not go through the trouble of installing more than the builtin Quicklisp dist though. Common Lisp developers seem not to care much about reproducible builds, or taking on the responsibility of software deployment on their own.

Because the official Quicklisp dists are released once every month or two (which is an eternity in the software world), developers cannot push hot-fixes or address user-reported problems in a timely manner, unless they run their own dist and convince their users to use that, or convince their users to clone directly from upstream, and place it in a particular location on their filesystem that Quicklisp looks for to override dist versions.

I am of the very strong opinion that developers should be responsible for deploying and versioning their own software, without the aforementioned downsides of relying on a single point of failure to do so for them.

### [Documentation](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#documentation)

Common Lisp libraries are rarely ever documented. "Docstrings" and code comments are not user documentation. A successful open-source project to be well-received by the public needs to have real offline user documentation, complete with plentiful usage examples, tutorials, imagery, and anything else that will transition a user more easily. This does not really need much explaining – Common Lisp software is mainly targeted at other developers that aren't afraid to read code and modify it to their liking.

### [Software Quality](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#software_quality)

Common Lisp software is of usually very high quality – if you take into consideration that it was more than likely developed by a single person and then stopped being maintained shortly thereafter. Common Lisp programmers are usually exceptional thinkers and writers of code, but they are often just one person – they cannot think of every edge case, find every major bug, write documentation, or keep interest over other priorities for very long.

This hints at a very real problem with Common Lisp: it has a tendency to attract people that employ the 'NIH syndrome' and refuse to collaborate. There is a large overlap of software available, and there is a large selection of low-hanging fruit for new developers. This coupled with the fact that the language is small, relatively speaking, hurts the language immensely.

In my opinion, this is due to the language being incredibly malleable. [It is usually much easier to re-implement an idea than it is to use/fix someone else's implementation](https://news.ycombinator.com/item?id=13441793). This is because Common Lisp code is so flexible that one can shape it to one's own thought processes. After all, code is just a projection of one's thought processes.

This problem is recursive, in that we have many "50%" solutions to the same problems, and the next round of developers will create another set of solutions to add to the pile.

Common Lisp, due to its flexibility, seems to cater very much towards single developers, and this shows brightly in the library ecosystem.

### [Programming Paradigm](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#programming_paradigm)

Common Lisp is a multi-paradigm programming language. That said, it's most prominent feature enables object-oriented programming in a unique way. While you can mix programming paradigms, it is nearly impossible to get away from OOP, with it being baked deep into the language.

Arguably, one of the best features of Common Lisp is the Common Lisp Object System (CLOS). The language is designed from the ground up with an object-oriented approach, though most modern programmers would not recognize it as object oriented because it has a very unique approach. A major difference in CLOS relative to most other object systems is that it disassociates methods from classes, and solves some real problems that have plagued other OOP implementations, such as multiple inheritance. Additionally, the object system is fully customizable with the Meta-Object Protocol (MOP), allowing one to change how the object system behaves at every level.

While I do think that CLOS is very nice, and it is hard to live without it, I also think that OOP in general does not fit every programming problem. Infact, for most applications, I would much rather have parametric polymorphism instead of ad-hoc polymorphism that you get with Common Lisp generic functions.

Generic functions in Common Lisp do not have arity-overloading like they do in Julia and other languages with generic functions. A generic function in Common Lisp has a fixed arity, and defines a protocol. Many people like this idea, but I don't.

Additionally, most of the language proper is not generic. For example, you cannot redefine what it is to be a sequence, extending them to other collection types or iterators. There is an extension present in some implementations called "extensible sequences" that partially solves this problem, but it cannot be made portable having its existence in only a handful of implementations. The reason for this comes down to the fact that invoking generic code in Common Lisp carries a small performance penalty, so any code which might be used in a performance-critical context, will be pressured to be made non-generic.

User-defined types in Common Lisp come in three forms: classes, structs, and types. `defclass` defines a class, `defstruct` defines a struct, and `deftype` defines a type.

Structs are rarely ever used except in performance-critical code, as they do not work seamlessly with the interactive development workflow of Common Lisp; redefining them is undefined behavior. Additionally, they only support single-inheritance.

User-defined types are merely type aliases for existing types.

Generic functions can only specialize their parameters on a class name, not a type. While every class has a type of the same name, the inverse is not true. One cannot define a method that operates on the integral range `[0, 10)` for example. It is however, possible to dispatch on a value, but only if that value is `EQL`-comparable, which is the case for scalars, not aggregates.

While CLOS is extremely powerful, and can be bent to do all sorts of nice tricks, these fundamental flaws are encountered on an almost daily basis in my programming, and I always wish for true parametric polymorphism with generic type parameters to stand in for a class of types.

### [Community](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#community)

The open-source Common Lisp community is the smallest out of any programming language community I have participated in. It is often hard to get the help you need, and even more difficult to find someone to collaborate with on a project, as most developers prefer to work alone.

Getting help is also often a problem. Experienced Common Lispers assume a basic understanding of the language, good style practice, and familiarity with Emacs and the associated Common Lisp tooling installed. Asking for help as a beginner, and posting a small snippet of code, more often than not results in a wall of text of replies asking the user to fix their style before they can consider helping. This is quite dissuading as a newcomer, and detracts from the user's learning path. In extreme cases, which are not rare at all, the community can be quite inflammatory towards newcomer questions, as they often get very upset over incorrect terminology or improperly formatted code.

Even as an experienced Common Lisper, I tend not to partake in such discussions, as it is bad for my health. I actually have a disability, and there have been times when engaging in these discussions have contributed adversely to my condition. [The community can just be flat-out toxic a lot of the time](https://eli.thegreenplace.net/2006/10/27/the-sad-state-of-the-lisp-user-community/).

### [Performance](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#performance)

If ultimate performance is your goal, Common Lisp is not the best choice for a language. While it is entirely possible to write code that can compete with the speed of C, it largely depends on the Common Lisp implementation, and making trade-offs that cripple the interactivity of the language.

Runtime performance gains can be achieved by not utilizing the dynamic dispatch feature of generic functions, which are inherent to class-based programming with CLOS. Instead, structs are typically used for creating aggregate types, as their field accessors are not generic, but regular functions, and redefining their definitions is undefined behavior.

Type annotations usually have to be sprinkled throughout the code, and macros and compiler macros have to be used to transform code into more efficient representations at compile time.

Arrays need to be specialized to pack immediate values into memory, rather than pointers to be chased to somewhere in heap memory. Element types that can be specialized are completely implementation-dependent, and almost always limited to scalars only. Arrays of structs, arrays of arrays, and many other data structures are usually not possible without performance implications.

Writing performant code in Common Lisp is not for everyone, and it most certainly cannot be done portably; what might run fast on one implementation may run poorly on another. The moment you start writing implementation-specific code, in my honest opinion, you are better off using another programming language (which can also be considered writing implementation-specific code).

## [Why I Prefer Julia As My Primary Programming Language](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#why_i_prefer_julia_as_my_primary_programming_language)

Julia is such a wonderful language. It's hard to describe why I like it so much, but some of the reasons are listed below. In short, Julia is very similar to Common Lisp, but brings a lot of extra niceties to the table.

### [Editor support](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#editor_support__2)

Julia editor support is among the top in its class. You are not limited to a single editor to get the full experience of this dynamic programming language. There are well-polished editor plugins for a variety of editors, and there even exists [an organization](https://github.com/JuliaEditorSupport) dedicated to improving the Julia editor tooling.

Personally, I use Vim (Neovim, actually) along with [LanguageServer.jl](https://github.com/julia-vscode/LanguageServer.jl) and the experience is very pleasant.

### [Language Evolution](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#language_evolution__2)

Julia does not have a language standard like Common Lisp does. It is free to evolve as the unique problem space it is attempting to address is further explored.

I consider this a good thing. I do not want a language frozen in time. I like to see growth, and Julia has been growing rapidly for many years, both in terms of adoption and the rate of new packages becoming available.

### [Software Versioning and Deployment](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#software_versioning_and_deployment__2)

Unlike Common Lisp, Julia gives the developer the responsibility of distributing their software. This is, however, very painless due to the built-in package manager, [Pkg.jl](https://pkgdocs.julialang.org/), in addition to package registries and related tools.

I host my software on GitHub, and the process of making my software discoverable to the wider Julia community is very simple. All I have to do is leave a comment on the commit I want to publish, and a GitHub bot takes care of analyzing my software, and merging it into the official package registry if it meets all of the requirements. The process is similarly simple for other hosting platforms, or if self-hosting.

Once a package is in the official registry, it can be installed by anyone using the builtin package manager, which conveniently has a special mode built in the the REPL for managing packages.

Reproducibility of builds is also handled very well. All Julia project environments contain a manifest file that records the exact versions of all transitive dependencies, along with a unique identifier for disambiguation, should the name of a project be found in multiple registries. Distributing this manifest file to a colleague is all that is needed for them to reproduce your exact development environment. It's all very painless.

Pkg.jl is a very well-designed package manager offering a lot of features. I encourage you to read the documentation to discover everything it can do. It is by far the best package manager I have ever used.

### [Programming Paradigm](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#programming_paradigm__2)

Julia is not an object-oriented language. Infact, it doesn't have classes at all. It has a unique type system that, at first glance, seems quite limiting in that only leaf nodes of the hierarchy can be instantiated. Intermediary nodes are abstract types which cannot be instantiated, but can be used to define behavior on entire classes of objects, even disjoint hierarchies by means of traits.

The fact that you can only instantiate concrete leaf node types may seem a bit limiting, but it drastically simplifies generic function method applicability, makes it much easier to reason about programs, and encourages developers to employ a composition over inheritance architecture.

Type parameterization and zero-cost generic functions are one of the primary reasons I switched to Julia. Writing efficient code couldn't be easier, and I don't have to sacrifice code clarity in doing so. Infact, I don't have to think about efficiency much at all apart from having a strong understanding of data structures and algorithms that every computer scientist should have.

One other notable difference between Common Lisp and Julia generic functions, is optional parameters can have specializations in Julia, in which case multiple methods are generated for each arity. Common Lisp forbids generic functions from differing in signature, so this is simply not possible in Common Lisp without a Meta-Object Protocol extension.

### [Community](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#community__2)

The Julia community is one of its strongest qualities, and is quite large. It is fragmented into various sub-communities: Slack, Zulip, Discourse, Discord, and IRC, to name a few. I am an active member of the Julia Zulip community, and questions I have get answered almost immediately. Additionally, this group of people is very welcoming to new users, and make me feel like part of the team.

Languages looking to improve their community image should look no further than Julia. It is truly a wonderful group of people to be a part of.

### [Performance](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#performance__2)

Julia code is fast – very fast. Even without knowing about common pitfalls like abstractly-typed fields, and type instability, in my experience, code runs much faster than highly hand-optimized Common Lisp code using an implementation known to generate efficient machine code.

Infact, the first version of my most recent project saw an order of magnitude difference when ported from Common Lisp to Julia, without any effort or attention to optimization techniques. This says a lot to me, because a great deal of time was spent optimizing the Common Lisp code to be as fast as possible without sacrificing maintainability or readability.

Julia code just performs good, and is very readable by default.

The final stable version of my recent project ported to Julia, complete with minor optimizations, saw a performance increase of 2 to 3 orders of magnitude. Functions that took milliseconds to execute were on the scale of nanoseconds in Julia, and code quality didn't suffer.

This is largely due to the excellent JIT compiler of Julia, and its rich type system. Generic functions in Julia do not carry any performance overhead, and type parameterization is even possible, allowing one to define functionality for a whole class of types without any runtime dispatch penalty.

## [Conclusion](https://mfiano.net/posts/2022-09-04-from-common-lisp-to-julia/#conclusion)

I have had my eye on Julia for many years, and I now consider it ready to be my "everyday" programming language.

Its strong focus on types and generic programming make it ideal to solve complex problems in an efficient manner, and without type annotations all over the place. Julia's type inference engine is actually extremely good, and constant propagation always surprises me at just how well it works.

Being able to use Julia in my editor of choice was another big plus in my book. I _really_ dislike Emacs _that_ much.

The community is very friendly, knowledgeable, and inclusive.

One thing I did not compare above is both languages' macro systems. This is because Julia macros are very similar to Common Lisp, and there are better resources to learn about them. One thing I will point out, is that Julia macros do automatic gensym'ing, as opposed to opt-in with Common Lisp, though you can opt-out on a per-symbol basis. This makes macros hygienic by default. Additionally, Julia has "generated functions", which to a Common Lisper, can be thought of as a compiler macro; their input arguments are types, not expressions, that are expanded after type inference. This allows you to generate more efficient code that cannot be determined at the syntax level.

Also not mentioned, is Julia's module system, which is very similar to Common Lisp's package system. Symbols are string-interned by the parser in much the same way as Common Lisp. The only thing worth pointing out here, is that modules can be hierarchical, unlike Common Lisp packages, and there is no need for Common Lisp's "package-local nicknames" extension, as this feature is baked into the Julia module system already.

In summary, you can tell the Julia designers were well aware of Common Lisp, and their attempts to make its ideas more convenient really shows once you become familiar enough with the language. I consider Julia to be a Lisp, just without the parentheses. It _really_ is not that far off from Common Lisp if you squint really hard, and that eased my transition quite a bit.

[^1] The term _package_ in Common Lisp is actually similar to _module_ in Julia. Common Lisp developers refer to what most other languages refer to as packages, as _systems_ instead.