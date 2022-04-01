---
id: nuuhzhnxwgugngjcc2qzhjd
title: What Color is Your Function?
desc: ""
updated: 1649035073092
created: 1649034460971
---

https://journal.stuffwithstuff.com/2015/02/01/what-color-is-your-function/

# A new language

# What color is your function?

Except wait. Here’s where our language gets screwy. It has this one peculiar feature:

## Every function has a color.

Each function—anonymous callback or regular named one—is either red or blue. Instead of a single function keyword, there are two:

```
blue_function doSomethingAzure() {
// This is a blue function...
}

red_function doSomethingCarnelian() {
// This is a red function...
}
```

There are no colorless functions in the language. Want to make a function? Gotta pick a color. Them’s the rules. And, actually, there are a couple more rules you have to follow too:

## The way you call a function depends on its color.

Imagine a “blue call” syntax and a “red call” syntax. Something like:

```
doSomethingAzure()blue;
doSomethingCarnelian()red;
```

When calling a function, you need to use the call that corresponds to its color. If you get it wrong—call a red function with `blue` after the parentheses or vice versa—it does something bad. Dredge up some long-forgotten nightmare from your childhood like a clown with snakes for arms hiding under your bed. That jumps out of your monitor and sucks out your vitreous humour.

Annoying rule, right? Oh, and one more:

### You can only call a red function from within another red function.

You can call a blue function from within a red one. This is kosher:

```
red_function doSomethingCarnelian() {
doSomethingAzure()blue;
}
```

But you can’t go the other way. If you try to do this:

```
blue_function doSomethingAzure() {
doSomethingCarnelian()red;
}
```

Well, you’re gonna get a visit from old Spidermouth the Night Clown.

This makes writing higher-order functions like our `filter`() example trickier. We have to pick a color for it and that affects the colors of the functions we’re allowed to pass to it. The obvious solution is to make `filter`() red. That way, it can take either red or blue functions and call them. But then we run into the next itchy spot in the hairshirt that is this language:

## Red functions are more painful to call.

For now, I won’t precisely define “painful”, but just imagine that the programmer has to jump through some kind of annoying hoops every time they call a red function.

What matters is that if you decide to make a function red, everyone using your API will want to spit in your coffee and/or deposit some even less savory fluids in it.

The obvious solution then is to never use red functions. Just make everything blue and you’re back to the sane world where all functions have the same color, which is equivalent to them all having no color, which is equivalent to our language not being entirely stupid.

Alas, the sadistic language designers—and we all know all programming language designers are sadists, don’t we?—jabbed one final thorn in our side:

## Some core library functions are red.

# It’s functional programming’s fault!

You might be thinking that the problem here is we’re trying to use higher-order functions.

If we only call blue functions, make our function blue. Otherwise, make it red. As long as we never make functions that accept functions, we don’t have to worry about trying to be “polymorphic over function color” (“polychromatic”?) or any nonsense like that.

But, alas, higher order functions are just one example. This problem is pervasive any time we want to break our program down into separate functions that get reused.

For example, let’s say we have a nice little blob of code that, I don’t know, implements Dijkstra’s algorithm over a graph representing how much your social network are crushing on each other.

Later, you end up needing to use this same blob of code somewhere else. You do the natural thing and hoist it out into a separate function. You call it from the old place and your new code that uses it. But what color should it be? Obviously, you’ll make it blue if you can, but what if it uses one of those nasty red-only core library functions?

What if the new place you want to call it is blue? You’ll have to turn it red. Then you’ll have to turn the function that calls it red.

# A colorful allegory

Of course, I’m not really talking about color here, am I? It’s an allegory, a literary trick. The Sneetches isn’t about stars on bellies, it’s about race. By now, you may have an inkling of what color actually represents. If not, here’s the big reveal:

**Red functions are asynchronous ones.**

...

# I promise the future is better

# I’m awaiting a solution

# What language isn’t colored?

So JS, Dart, C#, and Python have this problem. CoffeeScript and most other languages that compile to JS do too (which is why Dart inherited it). I think even ClojureScript has this issue even though they’ve tried really hard to push against it with their [core.async](https://github.com/clojure/core.async) stuff.

Wanna know one that doesn’t? Java. There you go. In their defense, they are actively trying to correct this oversight by moving to futures and async IO. It’s like a race to the bottom.

C# also actually can avoid this problem too. They opted in to having color. Before they added async-await and all of the `Task<T>` stuff, you just used regular sync API calls. Three more languages that don’t have this problem: Go, Lua, and Ruby.

Any guess what they have in common?

Threads. Or, more precisely: multiple independent callstacks that can be switched between. It isn’t strictly necessary for them to be operating system threads. Goroutines in Go, coroutines in Lua, and fibers in Ruby are perfectly adequate.

(That’s why C# has that little caveat. You can avoid the pain of async in C# by using threads.)

# Remembrance of operations past

# Awaiting a generated solution

# Reified callstacks

But if you have threads (green- or OS-level), you don’t need to do that. You can just suspend the entire thread and hop straight back to the OS or event loop _without having to return from all of those functions._

Go is the language that does this most beautifully in my opinion. As soon as you do any IO operation, it just parks that goroutine and resumes any other ones that aren’t blocked on IO.
