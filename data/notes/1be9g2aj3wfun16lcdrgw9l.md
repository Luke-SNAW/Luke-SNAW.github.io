
> https://thenewstack.io/angular-qwik-creator-on-how-js-frameworks-handle-reactivity/

Three approaches:

1. values
2. signals
3. observables

Angular and React use values and take a coarse-grained approach, re-rendering everything when data changes.

Vue is more fine-grained and will skip re-rendering unchanged components.

Svelte compilers code to be more efficient.

Qwik downloads only the minimal code needed through signals and resumability, making it highly optimized for start-up performance.

Solid uses signals to be the most fine-grained, only executing code initially.

While Solid is best for reactivity, Hevery argued Qwik has the best start-up performance since client-side code is minimized.

---

Reactive programming in JavaScript allows developers to create more dynamic and responsive applications. Hevery, who works as CTO at the [headless CMS](https://thenewstack.io/headless-cms-vs-no-code-website-builders/) [builder.io](https://www.builder.io/), explained it more precisely as updating the state or a variable and having the UI reflect that.

He identified the ways reactivity happens:

**Values:** A piece of data that can be assigned to a variable or passed to a function. With values, the framework periodically has to check to see if the value has changed. “I think this is why frameworks like Angular and React are so popular, because there’s nothing you have to learn,” he said. “It’s just regular JavaScript code that you place anywhere. It just does the right thing, at the expense that the framework has to go and check this stuff over and over and over.”

**Signals:** A value you place in a “bucket.” Signals allow the bucket to act as a traffic cop for values. It’s “all the rage,” Hevery said, with Svelte recently adding a signals-like capability called Ruins.

“Signals allow you all the system because it’s in a bucket, the bucket acts like a traffic cop, and as a result, the bucket tells the framework when there is an access — both to read access and write access,” he added. When a signal is read, the framework sends a message that someone read the value and it goes on to the next value.

However, signals have no time concept.

**Observables:** A more powerful, complicated version of signals that supports values one time. Time is fundamental to observables, he said, comparing it to a pipeline that carries the values. Observables leverage subscriptions, which are a way to receive notifications when changes are made to a data source, to change values. “The thing to notice about observables is that the way you create subscriptions is you do it explicitly,” he said.

Observables have become popular over the past five years, he said.

He explained how different frameworks deal with reactivity, ranging from what he called the coarse approach of [Angular](https://thenewstack.io/the-angular-renaissance-why-frontend-devs-should-revisit-it/) and [React](https://thenewstack.io/dev-news-react-still-king-vercel-ai-tools-netlify-connect/) to the more fine-grained approach of [Svelte](https://thenewstack.io/all-about-svelte-the-much-loved-state-driven-web-framework/), [Qwik](https://thenewstack.io/misko-hevery-on-why-qwik-will-improve-javascript-frameworks/) and [Solid](https://github.com/solidjs/solid), with [Vue](https://thenewstack.io/vue-2023/) in between the extremes.

[Reactivity scale](https://cdn.thenewstack.io/media/2023/09/94537576-reactivity-scale.png)

## **Angular and React**

“What makes something fine-grained is that the framework can be precise in the sense that if the value changes, the framework knows exactly what to do,” Hevery said. “If on the other hand, you change the value in the framework, I don’t know what has to change, let’s rerun all the components — that’s coarse-grained reactivity.”

The comparison wasn’t to say one was better than the other, but to pinpoint how each deals with reactivity, he said. But, his argument was that more fine-grained frameworks have to do less work re-rendering or re-computing whenever the value changes than the frameworks that are coarser.

“React and Angular are coarse-grained, meaning that whenever a value changes, the framework has no idea how to do it and so it just reads us everything and re-renders everything, and rebuilds the wrap again,” he said.

He demonstrated what he meant on each framework using a counter program. With Angular and React, the framework starts the counter with the implementer, executes it and then the framework learns about the display. After it executes the display, it learns about the data binding and that the display doesn’t have any more children. Then it goes back to the implementer and does the exact same thing, he said.

“Notice what’s happening during the bootup of the framework,” he said. “The framework has to go and visit every single component on a page in order to learn about the application.”

After he told the program to move ahead in the count, the framework not only did the UI update, but every single place went from count one to count two. That means the framework re-executed everything, he explained.

“Why did it revisit everything? Because the state was associated with the counter, and because the state was associated the counter, the framework starts at the counter and re-renders everything below it,” he said.

Developers can use a wrapper and make a promise but that’s a lot of additional work, he added, noting that lazy loading isn’t an option.

“If a component is in the render tree, lazy loading is not going to do anything,” he said. “As a matter of fact, it would make a good argument that it makes the situation worse, because of how rendering happens, how the promises actually get resolved, it will actually have to re-render more times, not fewer times.”

[Reactivity chart](https://cdn.thenewstack.io/media/2023/09/d7170f55-reactivity-chart-use-this.png)

## Vue

The code was very similar in Vue as in React and Angular, he said. Again, in Vue, every single component has to be revisited, he said. The framework has to learn about the application and the way it does that is to re-execute all the components, which is hydration, he added.

But there is a difference.

“In this case, the framework re-rendered the counter, re-rendered the wrapper, the display, but did not render the incrementer,” he said. “So out of the box, the framework was a little more intelligent and realized, ‘Oh, you have new data.’ The state associated with the counter, that state value was not passed down into the incrementer. Therefore I don’t have to descend into the incrementer to rerun it.”

When he hits plus one, the only thing that updates is the display.

“Now, the reason why this works in this way, is because Vue has signals — it’s not called signals, it’s call refs, but fundamentally, they’re signals,” he said. “What’s happening here is that a signal is created at the counter.”

## Svelte

Svelte is similar but has a compiler and so is really good at figuring out what things didn’t change, he said. It also has two different reactivity systems, he added — a reactivity system within the Svelte file, which the compiler does, and then a reactivity system outside of Svelte files called stores. The new version of Svelte also offers a third reactivity system called Ruins, which are closer to signals, he said.

“Svelte, at the beginning, had to execute all the components,” he said. “Notice a a pattern. Everybody that does hydration has no choice but to execute all the components to learn about the system, so everybody gets along.”

## Qwik

Qwik doesn’t have hydration; instead, it has resumability. That means the application can pause its execution on the server and resume it on the client without having to reload the entire application.

“Notice that the value is updating, but nothing is re-executed,” Hevery said. “What is interesting here is that the code associated with the incrementer did not show up on the client. Instead, the only thing that showed up on the client is the closure associated with the button.”

The closure shows up a piece of code that tells it to take the count and increment by one.

“Because it signals, the framework knows directly which [DOM](https://thenewstack.io/write-to-the-dom-or-not-when-js-frameworks-are-necessary/) element needs to be updated, because we’re only modifying the value of the DOM and not the structure of the tree in this particular example,” he said.

The framework doesn’t need to bring the display component into the client at all, because it knows this value is directly tied to this DOM element, he added. In this case, the developer can just update the DOM.

“What’s interesting about Qwik and why I’m kind of excited about it is, is that the only code that showed up that’s application-specific — the frame will have to be downloaded — and that always is the case,” he said. “The only application-specific tool that showed up in the client is the click listener associated with the button. Nothing else. To me, that is the ultimate kind of reactivity.”

That said, he considered Qwik less fine-grained than Solid because under certain circumstances, in Qwik, a component will execute only when it’s a structural DOM change; if it is just updating the value, then no component has to be downloaded.

## Solid Reactivity

Solid uses [hydration](https://thenewstack.io/javascript-hydration-is-a-workaround-not-a-solution/), which causes all of the things to happen at once, he said. Solid downloads the code and executes all the pieces associated with it at the startup, but it never re-executes the code again. That’s because signals allow it to hook everything up and the code doesn’t get executed even if it’s a structural change. That makes Solid more fine-grained in its reactivity than Qwik, but he still thinks Qwik has an advantage over Solid.

“The big advantage of Qwik is the fact that this code never shows up,” he said. “In Solid, the code still shows up to the client; it has to so that Solid can figure out what’s going on. In the case of Qwik, it never shows up in a client.”

However, Solid is the king of the hill in terms of fine-grained reactivity, he summarized.
