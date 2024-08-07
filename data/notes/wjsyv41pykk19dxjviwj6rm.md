
> https://without.boats/blog/coroutines-and-effects/
>
> The passage discusses the relationship between effect systems and coroutines. It explains that effect systems, like those found in languages like Koka, and coroutines, like Rust's async functions, are in some ways isomorphic to each other. The key difference is that coroutines yield control to their caller, while effectful expressions in effect systems yield control to their handler. The author argues that coroutines strike a good balance, as they are statically typed, lexically scoped, and unlayered, making them a promising approach for handling effectful functions. The passage also contrasts effect systems with Rust's use of the Result type and async/await syntax to model effects.

For the past few months I’ve been mulling over some things that Russell Johnston made me realize about the relationship between effect systems and coroutines. You can read more of his thoughts on this subject [here](https://www.abubalay.com/blog/2024/01/14/rust-effect-lowering), but he made me realize that effect systems (like that found in Koka) and coroutines (like Rust’s async functions or generators) are in some ways isomorphic to one another. I’ve been pondering the differences between them, trying to figuring out the advantages and disadvantages of each.

A few weeks ago, Will Crichton posted something on [Twitter](https://twitter.com/tonofcrates/status/1770560175835058573) that helped bring the contrast into sharper focus for me:

> The entire field of PL right now: what if it was dynamically scoped…. but statically typed…………..? (effects, capabilities, contexts, metavariables…)

I’m just a humble language designer (and not a theorist of anything, especially not PL), so my focus is the difference in user experience and affordance. But this seems like a cutting insight and this property of effect handlers - static typing but dynamic scoping - seems to me to be a good jumping off point for understanding the difference between effect handlers and coroutines from a user perspective.

## Background

### What is a coroutine?

A coroutine is a function which can yield control back to its caller before finishing. The caller then has a reference to the state of the coroutine when it yielded, so it can resume the coroutine again if it so chooses. It’s possible to model many meaningful “effects” using coroutines by having the coroutine yield. For example:

- A coroutine can perform IO “asynchronously,” by yielding a value like `Pending` when IO is being performed.
- A coroutine can be iterable by yielding values as it traverses some collection.
- A coroutine can model exceptions by yielding an exception value (in this case, resuming the coroutine would have no effect).

Rust, for example, models both asynchrony and iteration using coroutines. On the other hand, exceptions are not modeled this way; instead they are modeled with the `Result` type. Specifically, Rust uses “stackless” coroutines, but this distinction is not very important to the concepts in this post.

### What is an effect handler?

I need to be clear, because terminology has become muddied in the Rust community: this post has nothing in particular to do with “effects generics” as conceptualized by the Rust project, which is a different set semantic features related to how Rust handles effects from “effects systems” as they appear in the literature. In this post, I am focused on effect systems as proposed in languages like [Koka](https://koka-lang.github.io/koka/doc/index.html) and [Effekt](https://effekt-lang.org/). And my understanding of these systems may be imperfect or wrong, but this is how they operate as I understand them.

In an effect system, in addition to a type, an expression will have an _effect_. An effect is an additional “kind” in the formal, type system sense of the word (in the same way that lifetimes are another “kind” in Rust). In general, expressions inherit the effects of other expressions they contain. Functions inherit the effects of their body.

For example, Koka has a “diverging” effect, which means that an expression may diverge (that is to say, it may not finish evaluating). An expression containing a diverging expression is also diverging. So you can distinguish in the type system between a function that is guaranteed to finish and a function that may not finish (this is imperfect, of course, because of the undecidability of the halting problem; some functions that do not diverge will be marked diverging).

However, these languages also have a concept of _effect handlers_, which take an expression with an effect and “handle” it, producing an expression without that effect. Not all effects can be handled (for example, as far as I understand it is not possible to meaningfully handle the diverging effect), but some can. The semantics of what it means to handle an effect are where effect systems become similar to coroutines.

When a handleable effect occurs, an effectful expression yields control to the nearest-most handler of that effect, which may or may not yield control back. This can be used to model all of the same sorts of effects as coroutines. For example:

- An IO effect can yield control to the IO handler, which will yield back to the expression when IO is complete.
- An iterable effect can yield control to the loop consumer for each value, which yields back to the iterable to continue iteration.
- An exception effect can yield control to an exception handler, which will not yield control back.

## The difference is between static and dynamic scope

The key difference between coroutines and effect handlers is that coroutines yield control to their caller, but effectful expressions yield control to their handler. The difference of affordance this implies is the materially significant advantage of coroutines over effect handlers.

Let’s imagine a programming language in which every function is a coroutine which can yield `Pending` or an exception (to model both IO and exceptions) and there are multiple kind of call operators that “handle effects” differently:

- There is an ordinary call operator that can only be used on coroutines that never yield (these coroutines are effectively pure functions)
- There is an asynchronous `().await` call operator that can be called on coroutines that yield `Pending`, which yields `Pending` and then calls them again (so it can only be called from within another coroutine that yields `Pending`)
- There is an exception-throwing `()?` call operator that can be called on coroutines that yield an exception, which yields the exception outward.
- There is a combined `().await?` call operator that can be called on coroutines that yield `Pending` and exceptions, to forward both effects.

Let’s suppose you wanted to do an HTTP request in this language (which performs IO and can also raise an exception representing some sort of IO error):

```fallback
fn get_blog() -> HttpResponse yields (Pending | Exception) {
    http::get("https://without.boats").await?
}
```

Now, let’s contrast this to a similar language which models IO and exceptions using effects. In this language, there is no need for special call operators: a function which has an IO or exception effect can call functions which also have IO or exception effects:

```fallback
fn get_blog() -> HttpResponse effect (IO | Exception) {
    http::get("https://without.boats")
}
```

The difference between these features is that the call to `http::get` must be annotated with the `await` and `?` syntax to forward its effects, whereas with effect handlers the forwarding of effects by a callee is implicit.

I want to take one more step back and then I promise I will reach a conclusion. There are definitions of coroutines other than the one I gave, especially older ones. If you were to closely read [Wikipedia](https://en.wikipedia.org/wiki/Coroutine), you would find a slightly different definition, and what I’ve called coroutines are addressed instead as “generators” or “semicoroutines.” In the older definition, a coroutine can specify where it yields control. This is actually based on a model of program execution in which there is no program stack: instead, every coroutine is a global singleton, and yielding control to it means continuing it wherever it last left off. For semicoroutines, in contrast, calling a coroutine produces a new stack frame which can only be resumed by code with a reference to that stack frame.

The program stack is such a universal model of program execution today that we treat it as inevitable, but like everything else it had to be invented. It was invented to support recursive function definition, but it has other advantages in the way that it enables local reasoning: from the body of a function, there is exactly one dynamic jump point - wherever it returns to. From the point of view of the caller, this is now statically known: the function will jump back to the point at which it is called.

This rule can only be violated when a language introduces new features that allow additional dynamic jump points. One that has long been popular is the notion of exceptions, which unwind the call stack to the point at which they are being handled. There are two kinds of exceptions: unchecked exceptions, which are totally untyped, and checked exceptions, which require an annotations on any function which could throw them.

**Effect handlers are a generalization of checked exceptions**, with all of the pros and cons of that feature. They require you to annotate functions that have an effect, but they do not require you to annotate _calls_ at which the effect can occur. Therefore, when examining the body of a function, to understand when the effect occurs requires examining the type signature of every function that is called. Since this is meaningful control flow, it seems very valuable to be able to identify points at which an error occurs without examining the signatures of each function call. This is why Rust features `Result` and the `?` operator instead of checked exceptions.

There’s an axis of evaluation here with three points: a language could model an effect in a way which is totally unchecked at compile time: both dynamically typed and dynamically scoped. Unchecked exceptions (including panics) are an example of this; so is blocking IO. And a language could model the effect in the type system, but with a dynamic scope. Checked exceptions and effect handlers are both examples of this. And a language could model the effect in a way which is both statically typed and lexically scoped. This is what Rust does for these effects with both `Result` and `async/await`.

(You may notice that there’s a fourth spot in the design space not covered here: dynamically typed and lexically scoped. An example in this category would be the async/await feature in dynamically typed languages like Python and JavaScript; you must annotate asynchronous calls with `await` to get their result, but if you fail to do so it is not a compile-time error.)

```fallback
                                          │   EXCEPTIONS          │   IO
──────────────────────────────────────────┼───────────────────────┼───────────────
                                          │                       │
  DYNAMICALLY TYPED & DYNAMICALLY SCOPED  │   panicking           │   blocking
                                          │                       │
   STATICALLY TYPED & DYNAMICALLY SCOPED  │   checked exceptions  │   IO effect
                                          │                       │
     STATICALLY TYPED & LEXICALLY SCOPED  │   Result              │   async/await
                                          │                       │
```

These are not the only language features that can be used to model effects, and other features also fall into one of these buckets. For example, monads are also statically typed and lexically scoped. However, a major objection to monads is that they model effects in a specifically layered way, so that for example there is a distinction between an `IO<Result<T, E>>` and a `Result<IO<T>, E>`. Coroutines on the other hand are order-independent: all coroutine that yield `Pending` and `Exception` have the same type, there is no distinction of order. The same is true of effect handlers.

This has appeared in Rust for example with the debate about the design of [async iterators](https://without.boats/blog/poll-next). Designs based on `async fn next` introduce an arbitrary ordering by introducing multiple coroutines, whereas designed based on a single coroutine do not make a distinction; the coroutine just yields items as well as `Pending`. This was the crux of Russell Johnston’s argument in the post I linked earlier: this unlayered property is shared by coroutines and effect handlers, and is an advantage of these features.

On the other hand, by modeling errors with `Result` instead of some sort of coroutine, Rust _does_ introduce an ordering. This is mostly fine because of the fact that a function which “throws an exception” (by evaluating to an `Err`) is not supposed to be resumed, though it introduces some quirks where for example there’s no way to distinguish between an iterator of `Result`s (which may continue after one is an `Err`) and an iterator which throws an error (which will not continue). If instead a generator could “yield an exception,” it would be a different type from a generator that yields a sequence of `Result`s. But I don’t find this inadequacy to come up in practice that often, so I’m content to leave it as theoretical work for a future language to solve.

Overall, coroutines strike me as the most promising way to handle many kinds of effectful functions because they seem to be in the design sweet spot: They are statically typed, lexically scoped, and unlayered. This is why my starting point for handling effects in any language would be a coroutine feature (though if the language were not under Rust’s constraints, I would prefer if it were a stackful coroutine feature so they could be recursive).
