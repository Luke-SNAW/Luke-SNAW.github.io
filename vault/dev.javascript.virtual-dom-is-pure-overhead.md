---
id: a8zbwhfmtzwmplthrmphpms
title: Virtual DOM is pure overhead
desc: ""
updated: 1675303158159
created: 1675302568674
---

> https://svelte.dev/blog/virtual-dom-is-pure-overhead

Let's retire the 'virtual DOM is fast' myth once and for all

[Rich Harris](https://twitter.com/Rich_Harris) Dec 27 2018

If you've used JavaScript frameworks in the last few years, you've probably heard the phrase 'the virtual DOM is fast', often said to mean that it's faster than the _real_ DOM. It's a surprisingly resilient meme — for example people have asked how Svelte can be fast when it doesn't use a virtual DOM.

It's time to take a closer look.

## What is the virtual DOM?

In many frameworks, you build an app by creating `render()` functions, like this simple [React](https://reactjs.org/) component:

```js
function HelloMessage(props) {
  return <div className="greeting">Hello {props.name}</div>
}
```

You can do the same thing without JSX...

```js
function HelloMessage(props) {
  return React.createElement(
    "div",
    { className: "greeting" },
    "Hello ",
    props.name
  )
}
```

...but the result is the same — an object representing how the page should now look. That object is the virtual DOM. Every time your app's state updates (for example when the `name` prop changes), you create a new one. The framework's job is to _reconcile_ the new one against the old one, to figure out what changes are necessary and apply them to the real DOM.

## How did the meme start?

Misunderstood claims about virtual DOM performance date back to the launch of React. In [Rethinking Best Practices](https://www.youtube.com/watch?v=x7cQ3mrcKaY), a seminal 2013 talk by former React core team member Pete Hunt, we learned the following:

> This is actually extremely fast, primarily because most DOM operations tend to be slow. There's been a lot of performance work on the DOM, but most DOM operations tend to drop frames.

> It's fast! Because the DOM is slow!  
> [Screenshot](https://svelte.dev/blog/virtual-dom-is-pure-overhead#:~:text=Screenshot%20from%20Rethinking%20Best%20Practices%20at%20JSConfEU%202013) from [Pete Hunt, Rethinking Best Practices](https://www.youtube.com/watch?v=x7cQ3mrcKaY) at JSConfEU 2013

But hang on a minute! The virtual DOM operations are _in addition to_ the eventual operations on the real DOM. The only way it could be faster is if we were comparing it to a less efficient framework (there were plenty to go around back in 2013!), or arguing against a straw man — that the alternative is to do something no-one actually does:

```js
onEveryStateChange(() => {
  document.body.innerHTML = renderMyApp()
})
```

Pete clarifies soon after...

> React is not magic. Just like you can drop into assembler with C and beat the C compiler, you can drop into raw DOM operations and DOM API calls and beat React if you wanted to. However, using C or Java or JavaScript is an order of magnitude performance improvement because you don't have to worry...about the specifics of the platform. With React you can build applications without even thinking about performance and the default state is fast.

...but that's not the part that stuck.

## So... is the virtual DOM _slow_?

Not exactly. It's more like 'the virtual DOM is usually fast enough', but with certain caveats.

The original promise of React was that you could re-render your entire app on every single state change without worrying about performance. In practice, I don't think that's turned out to be accurate. If it was, there'd be no need for optimisations like `shouldComponentUpdate` (which is a way of telling React when it can safely skip a component).

Even with `shouldComponentUpdate`, updating your entire app's virtual DOM in one go is a lot of work. A while back, the React team introduced something called React Fiber which allows the update to be broken into smaller chunks. This means (among other things) that updates don't block the main thread for long periods of time, though it doesn't reduce the total amount of work or the time an update takes.

## Where does the overhead come from?

Most obviously, [diffing isn't free](https://twitter.com/pcwalton/status/1015694528857047040). You can't apply changes to the real DOM without first comparing the new virtual DOM with the previous snapshot. To take the earlier `HelloMessage` example, suppose the `name` prop changed from 'world' to 'everybody'.

1. Both snapshots contain a single element. In both cases it's a `<div>`, which means we can keep the same DOM node
2. We enumerate all the attributes on the old `<div>` and the new one to see if any need to be changed, added or removed. In both cases we have a single attribute — a `className` with a value of `"greeting"`
3. Descending into the element, we see that the text has changed, so we'll need to update the real DOM

Of these three steps, only the third has value in this case, since — as is the case in the vast majority of updates — the basic structure of the app is unchanged. It would be much more efficient if we could skip straight to step 3:

```js
if (changed.name) {
  text.data = name
}
```

(This is almost exactly the update code that Svelte generates. Unlike traditional UI frameworks, Svelte is a compiler that knows at _build time_ how things could change in your app, rather than waiting to do the work at _run time_.)

## It's not just the diffing though

The diffing algorithms used by React and other virtual DOM frameworks are fast. Arguably, the greater overhead is in the components themselves. You wouldn't write code like this...

```js
function StrawManComponent(props) {
  const value = expensivelyCalculateValue(props.foo)

  return <p>the value is {value}</p>
}
```

...because you'd be carelessly recalculating `value` on every update, regardless of whether `props.foo` had changed. But it's extremely common to do unnecessary computation and allocation in ways that seem much more benign:

```js
function MoreRealisticComponent(props) {
  const [selected, setSelected] = useState(null)

  return (
    <div>
      <p>Selected {selected ? selected.name : "nothing"}</p>

      <ul>
        {props.items.map((item) => (
          <li>
            <button onClick={() => setSelected(item)}>{item.name}</button>
          </li>
        ))}
      </ul>
    </div>
  )
}
```

Here, we're generating a new array of virtual `<li>` elements — each with their own inline event handler — on every state change, regardless of whether `props.items` has changed. Unless you're unhealthily obsessed with performance, you're not going to optimise that. There's no point. It's plenty fast enough. But you know what would be even faster? _Not doing that._

[React Hooks](https://reactjs.org/docs/hooks-intro.html) doubles down on defaulting to doing unnecessary work, with [predictable results](https://twitter.com/thekitze/status/1078582382201131008).

The danger of defaulting to doing unnecessary work, even if that work is trivial, is that your app will eventually succumb to 'death by a thousand cuts' with no clear bottleneck to aim at once it's time to optimise.

Svelte is explicitly designed to prevent you from ending up in that situation.

## Why do frameworks use the virtual DOM then?

It's important to understand that virtual DOM _isn't a feature_. It's a means to an end, the end being declarative, state-driven UI development. Virtual DOM is valuable because it allows you to build apps without thinking about state transitions, with performance that is _generally good enough_. That means less buggy code, and more time spent on creative tasks instead of tedious ones.

But it turns out that we can achieve a similar programming model without using virtual DOM — and that's where Svelte comes in.

---

## [Pete Hunt](https://news.ycombinator.com/item?id=34615578)

I'm quoted in this blog post so I figured I'd respond. I'm a former member of the React team but I haven't worked on it in a long time.
Largely I agree with everything in this article on a factual basis but I disagree on the framing of the trade-offs. Two points in particular:

1. Before open sourcing React we extensively measured performance on real world applications like mobile search and desktop ads management flows. While there are pathological cases where you can notice the overhead of the virtual DOM diff it's pretty rare that it meaningfully affects the user experience in practice, especially when compared to the overhead of downloading static resources like JS and rendering antipatterns like layout thrash. And in the situations where it is noticeable there are escape hatches to fix it (as mentioned in the article).

2. I disagree with the last sentence strongly. I would argue that Svelte makes huge sacrifices in expressive power, tooling and predictability in order to gain performance that is often not noticeable or is easily achieved with React's memoization features. React was always about enabling front-end engineers to take advantage of software engineering best practices so they could level up velocity and quality. I think Svelte's use of a constrained custom DSL is a big step backwards in that respect so while I appreciate the engineering behind it, it's not a technology I am interested in using.

Even though I disagree on these points I think it is a well-written article and is a pretty fair criticism of React outside of those two points, and I could see reasonable people disagreeing on these trade-offs.

### [The5thElephant](https://news.ycombinator.com/item?id=34617387)

Regarding your second point, this is exactly why I like Vue and Svelte so much over React (which I am also quite familiar with). Coming from a design background and having learned HTML/CSS first, the Svelte and Vue approach to SFCs and templating makes it far easier to understand, write, and visually parse than React where everything is always JS first. I can't think of a situation where Svelte/Vue limited me from doing something you can do in React, and Svelte/Vue make getting into a codebase far more accessible for people with a wider range of skillsets.
The secondary effects of React's popularity have been a significant loss in emphasis on HTML and CSS skills over doing everything in JS which often results in div-soup that is less performant and less capable. HTML and CSS not being first class-citizens as they are in other frameworks means developers simply aren't encouraged to learn them nearly as well as they used to.

Front-end frameworks should not be just for front-end developers. They should be understandable and accessible to people who are not JS first and who come from backgrounds that are not purely engineering. In my experience it is much easier to teach someone familiar with design and HTML/CSS how to explore a Vue or Svelte codebase than a React one, and the JS devs I have worked with who fully learn these libraries have not complained about any limitations compared to React.

### [tobr](https://news.ycombinator.com/item?id=34617908)

I think your conclusion in point 2 is misguided, but I can see where you’re coming from. It’s true that virtual DOM has a lot of expressive power, and Svelte’s templating features are more limited in how you can approach certain problems. I find Svelte’s slots especially challenging for more advanced use cases, and wish they were more composable.

But in my experience, React’s openness to expressive experimentation is not a net positive for maintainability, productivity, or quality. There are lots of footguns, and bad ideas embraced by the ecosystem. HoCs were a terrible idea, and were replaced with an even worse idea, hooks. Compared to that, Svelte’s reactive statements and stores are a bliss.

Arguably, it’s because React has experimented and made those mistakes that Svelte has been able to focus on a constrained DSL that mostly supports the features that are actually a good idea.

#### [Pete Hunt](https://news.ycombinator.com/item?id=34618467)

I think there are two things that are interesting about your point of view.
First, I think a mistake the react team made was not exerting more control over the ecosystem. I think a lot of questionable content marketing pieces ended up as “best practices” which we are still unwinding as a community.

Second, I totally buy the idea that there are multiple personas and that different tools speak to different personas. The sustained popularity of constrained dsls among subsets of the frontend community speaks to this.
