---
id: dvjc48q2a8tm8n0yvqtgylf
title: React I Love You, But You're Bringing Me Down
desc: ""
updated: 1663734714975
created: 1663718149852
---

> François Zaninotto  
> September 20, 2022  
> https://marmelab.com/blog/2022/09/20/react-i-love-you.html  
> https://news.ycombinator.com/item?id=32911492

Dear [React.js](https://reactjs.org/),

We've been together for almost 10 years. We've come [a long way](https://marmelab.com/react-admin/). But things are getting out of hand. We need to talk.

It's embarrassing, I know. Nobody wants to have that conversation. So instead, I'll say it in songs.

## [You Were The One](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#you-were-the-one)

I'm not a first-time JS lover. I've had long adventures with jQuery, Backbone.js, and Angular.js before you. I knew what I could expect from a relationship with a JavaScript framework: Better UIs, more productivity, and a smoother developer experience - but also the frustrations of having to constantly change the way I think about my code to match the framework's mindset.

And when I met you, I was just out of a long relationship with [Angular.js](https://angularjs.org/). I was exhausted by `watch` and `digest`, not to mention `scope`. I was looking for something that didn't make me feel miserable.

It was love at first sight. Your [one-way data binding](https://reactjs.org/docs/thinking-in-react.html#step-5-add-inverse-data-flow) was so refreshing compared to all I knew at the time. An entire category of problems I had with data synchronization and performance simply didn't exist with you. You were pure JavaScript, not a poor imitation expressed as a string in an HTML element. You had this thing, the "declarative component", which was so beautiful that everyone kept looking at you.

You were not the easy type. I had to work on my coding habits to get along with you, but boy was it worth it! At first, I was so happy with you that I kept telling everyone about you.

## [Heroes Of New Forms](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#heroes-of-new-forms)

Things started getting weird when I asked you to handle forms. Forms and input are hard to cope with in vanilla JS. With React, they're even _harder_.

First, developers have to choose between [controlled and uncontrolled inputs](https://reactjs.org/docs/uncontrolled-components.html). Both have drawbacks and bugs in corner cases. But why do I have to make a choice in the first place? Two form strategies are one too many.

The "recommended" way, controlled components, is super verbose. This is the code I need for an addition form:

```jsx
import React, { useState } from "react";

export default () => {
  const [a, setA] = useState(1);
  const [b, setB] = useState(2);

  function handleChangeA(event) {
    setA(+event.target.value);
  }

  function handleChangeB(event) {
    setB(+event.target.value);
  }

  return (
    <div>
      <input type="number" value={a} onChange={handleChangeA} />
      <input type="number" value={b} onChange={handleChangeB} />

      <p>
        {a} + {b} = {a + b}
      </p>
    </div>
  );
};
```

And if there were only two ways, I'd be happy. But because of the huge amount of code required to build a real-life form with default values, validation, dependent inputs, and error messages, I have to use a third-party form framework. And they all fall short one way or another.

- [Redux-form](https://redux-form.com/8.3.0/) looked like a natural choice when we used Redux, but then his lead developer abandoned it to build
- [React-final-form](https://final-form.org/react/), which is full of unfixed bugs, and the lead developer left again. So I looked at
- [Formik](https://formik.org/), popular but heavyweight, slow for large forms, and limited in terms of features. So we decided to use
- [React-hook-form](https://react-hook-form.com/), which is fast, but has hidden bugs and has documentation structured like a maze.

After years of building forms with React, I still struggle to make robust user experiences with legible code. When I look at how [Svelte](https://svelte.dev/blog/write-less-code) deals with forms, I can't help but feel I'm tied with the wrong abstraction. Look at this addition form:

```js
<script>
    let a = 1;
    let b = 2;
</script>

<input type="number" bind:value={a}>
<input type="number" bind:value={b}>

<p>{a} + {b} = {a + b}</p>
```

## [You're Too Context Sensitive](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#youre-too-context-sensitive)

Shortly after we first met, you introduced me to your puppy [Redux](https://redux.js.org/). You couldn't go anywhere without it. I didn't mind at first, because it was cute. But then I realized that the world was spinning around it. Also, it made things harder when building a framework - other developers couldn't easily tweak an app with existing reducers.

But you noticed it, too, and you decided to get rid of Redux in favor of your own `useContext`. Except that `useContext` lacks a crucial feature of Redux: the ability to react to changes in parts of the context. These two are NOT equivalent in terms of performance:

```jsx
// Redux
const name = useSelector((state) => state.user.name);
// React context
const { name } = useContext(UserContext);
```

Because in the first example, the component will only rerender if the user name changes. In the second example, the component will rerender when _any_ part of the user changes. This matters a lot, to the point that we have to split contexts to avoid unnecessary rerenders.

```jsx
// this is crazy but we can't do otherwise
export const CoreAdminContext = (props) => {
  const {
    authProvider,
    basename,
    dataProvider,
    i18nProvider,
    store,
    children,
    history,
    queryClient,
  } = props;

  return (
    <AuthContext.Provider value={authProvider}>
      <DataProviderContext.Provider value={dataProvider}>
        <StoreContextProvider value={store}>
          <QueryClientProvider client={queryClient}>
            <AdminRouter history={history} basename={basename}>
              <I18nContextProvider value={i18nProvider}>
                <NotificationContextProvider>
                  <ResourceDefinitionContextProvider>
                    {children}
                  </ResourceDefinitionContextProvider>
                </NotificationContextProvider>
              </I18nContextProvider>
            </AdminRouter>
          </QueryClientProvider>
        </StoreContextProvider>
      </DataProviderContext.Provider>
    </AuthContext.Provider>
  );
};
```

Most of the time, when I have a performance problem with you, it's because of a large context, and I have no choice but to split it.

I don't want to use `useMemo` or `useCallback`. Useless rerenders is _your_ problem, not _mine_. But you force me to do it. Look at how I'm supposed to build a simple form input to make it reasonably fast:

```jsx
// from https://react-hook-form.com/advanced-usage/#FormProviderPerformance
const NestedInput = memo(
  ({ register, formState: { isDirty } }) => (
    <div>
      <input {...register("test")} />
      {isDirty && <p>This field is dirty</p>}
    </div>
  ),
  (prevProps, nextProps) =>
    prevProps.formState.isDirty === nextProps.formState.isDirty
);

export const NestedInputContainer = ({ children }) => {
  const methods = useFormContext();

  return <NestedInput {...methods} />;
};
```

It's been 10 years, and you still have that flaw. How hard is it to offer a `useContextSelector`?

[You're aware of this](https://github.com/reactjs/rfcs/pull/118), of course. But you're looking elsewhere, even though it's probably your most important performance bottleneck.

## [I Want None Of This](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#i-want-none-of-this)

You've explained to me that I shouldn't access DOM nodes directly, for my own good. I never thought that the DOM was dirty, but as it disturbed you, I stopped doing it. Now I use [refs](https://en.reactjs.org/docs/refs-and-the-dom.html), as you asked me to.

But this ref stuff spreads like a virus. Most of the time, when a component uses a ref, it passes it to a child component. If that second component is a React component, it must forward the ref to another component, and so on, until one component in the tree finally renders an HTML element. So the codebase ends up forwarding refs everywhere, reducing the legibility in the process.

Forwarding refs could be as simple as this:

```jsx
const MyComponent = (props) => <div ref={props.ref}>Hello, {props.name}!</div>;
```

But no, that would be too easy. Instead, you've invented this `react.forwardRef` abomination:

```jsx
const MyComponent = React.forwardRef((props, ref) => (
  <div ref={ref}>Hello, {props.name}!</div>
));
```

Why is it so hard, you may ask? Because [you simply can't make a generic component (in the sense of Typescript) with `forwardRef`](https://stackoverflow.com/questions/58469229/react-with-typescript-generics-while-using-react-forwardref).

```tsx
// how am I supposed to forwardRef to this?
const MyComponent = <T>(props: <ComponentProps<T>) => (
    <div ref={/* pass ref here */}>Hello, {props.name}!</div>
);
```

Besides, you've decided that refs are not only DOM nodes, they're the equivalent of `this` for function components. Or, to put it otherwise, "state that doesn't trigger a rerender". In my experience, each time I have to use such a ref, it's because of you - because your `useEffect` API is too weird. In other terms, `refs` are a solution to a problem you created.

## [The Butterfly (use) Effect](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#the-butterfly-use-effect)

Speaking of `useEffect`, I have a personal problem with it. I recognize that it's an elegant innovation that covers mount, unmount and update events in one unified API. But how is this supposed to count as progress?

```jsx
// with lifecycle callbacks
class MyComponent {
  componentWillUnmount: () => {
    // do something
  };
}

// with useEffect
const MyComponent = () => {
  useEffect(() => {
    return () => {
      // do something
    };
  }, []);
};
```

You see, this line alone represents the griefs I have with your `useEffect`:

```text
    }, []);
```

I see such cryptic suites of cabalistic signs all over my code, and they're all because of `useEffect`. Plus, you force me to keep track of dependencies, like in this code:

```jsx
// change page if there is no data
useEffect(() => {
  if (
    query.page <= 0 ||
    (!isFetching && query.page > 1 && data?.length === 0)
  ) {
    // Query for a page that doesn't exist, set page to 1
    queryModifiers.setPage(1);
    return;
  }
  if (total == null) {
    return;
  }
  const totalPages = Math.ceil(total / query.perPage) || 1;
  if (!isFetching && query.page > totalPages) {
    // Query for a page out of bounds, set page to the last existing page
    // It occurs when deleting the last element of the last page
    queryModifiers.setPage(totalPages);
  }
}, [isFetching, query.page, query.perPage, data, queryModifiers, total]);
```

See this last line? I have to make sure I include all reactive variables in the dependency array. And I thought that [reference counting](https://en.wikipedia.org/wiki/Reference_counting) was a native feature of all languages with a garbage collector. But no, I have to micromanage dependencies myself because you don't know how to do it.

> Seriously?

And very often, one of these dependencies is a function that I created. Because you don't make the difference between a variable and a function, I have to tell you, using `useCallback`, that you shouldn't rerender for anything. Same consequence, same final cryptic signature:

```jsx
const handleClick = useCallback(
  async (event) => {
    event.persist();
    const type =
      typeof rowClick === "function"
        ? await rowClick(id, resource, record)
        : rowClick;
    if (type === false || type == null) {
      return;
    }
    if (["edit", "show"].includes(type)) {
      navigate(createPath({ resource, id, type }));
      return;
    }
    if (type === "expand") {
      handleToggleExpand(event);
      return;
    }
    if (type === "toggleSelection") {
      handleToggleSelection(event);
      return;
    }
    navigate(type);
  },
  [
    // oh god, please no
    rowClick,
    id,
    resource,
    record,
    navigate,
    createPath,
    handleToggleExpand,
    handleToggleSelection,
  ]
);
```

A simple component with a few event handlers and lifecycle callbacks becomes a pile of gibberish code just because I have to manage this dependency hell. All that is because you've decided that a component may execute an arbitrary number of times.

So for example, if I want to make a counter that increases every second and every time the user clicks on a button, I have to do this:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    setCount((count) => count + 1);
  }, [setCount]);

  useEffect(() => {
    const id = setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);
    return () => clearInterval(id);
  }, [setCount]);

  useEffect(() => {
    console.log("The count is now", count);
  }, [count]);

  return <button onClick={handleClick}>Click Me</button>;
}
```

While if you knew how to keep track of dependencies, I could simply write:

```jsx
function Counter() {
  const [count, setCount] = createSignal(0);

  const handleClick = () => setCount(count() + 1);

  const timer = setInterval(() => setCount(count() + 1), 1000);

  onCleanup(() => clearInterval(timer));

  createEffect(() => {
    console.log("The count is now", count());
  });

  return <button onClick={handleClick}>Click Me</button>;
}
```

That's valid [Solid.js](https://www.solidjs.com/) code, by the way.

Finally, using `useEffect` wisely requires reading [a 53 pages dissertation](https://overreacted.io/a-complete-guide-to-useeffect/). I must say, that is a terrific piece of documentation. But if a library requires me to go through dozens of pages to use it properly, isn't it a sign that it's not well designed?

## [Makeup Your Mind](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#makeup-your-mind)

Since we've already talked about the leaky abstraction that is `useEffect`, you've tried to improve it. You've introduced me to [`useEvent`](https://github.com/reactjs/rfcs/blob/useevent/text/0000-useevent.md), [`useInsertionEffect`](https://reactjs.org/docs/hooks-reference.html#useinsertioneffect), [`useDeferredValue`](https://reactjs.org/docs/hooks-reference.html#usedeferredvalue), [`useSyncWithExternalStore`](https://reactjs.org/docs/hooks-reference.html#usesyncexternalstore), and other gimmicks.

And they do make you look beautiful:

```jsx
function subscribe(callback) {
  window.addEventListener("online", callback);
  window.addEventListener("offline", callback);
  return () => {
    window.removeEventListener("online", callback);
    window.removeEventListener("offline", callback);
  };
}

function useOnlineStatus() {
  return useSyncExternalStore(
    subscribe, // React won't resubscribe for as long as you pass the same function
    () => navigator.onLine, // How to get the value on the client
    () => true // How to get the value on the server
  );
}
```

But to me, this is lipstick on a pig. If reactive effects were easier to use, you wouldn't need all these other hooks.

To put it otherwise: you have no other solution than to grow the core API more and more over time. For people like me, who have to maintain huge codebases, this constant API inflation is a nightmare. Seing you wear more and more makeup everyday is a constant reminder of what you're trying to hide.

## [Strict Machine](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#strict-machine)

Your hooks are a great idea, but they come at a cost. And this cost is the [Rules of Hooks](https://reactjs.org/docs/hooks-rules.html). They aren't easy to memorize, they aren't easy to put into practice. But they force me to spend time on code that shouldn't need it.

For instance, I have an "inspector" component that can be dragged around by the end user. Users can also hide the inspector. When hidden, the inspector component renders nothing. So I would very much like to "leave early", and avoid registering event listeners for nothing.

```jsx
const Inspector = ({ isVisible }) => {
  if (!isVisible) {
    // leave early
    return null;
  }
  useEffect(() => {
    // Register event listeners
    return () => {
      // Unregister event listeners
    };
  }, []);
  return <div>...</div>;
};
```

But no, that's against the Rules of Hooks, as the `useEffect` hook may or may not be executed depending on props. Instead, I have to add a condition to all effects so that they leave early when the `isVisible` prop is false:

```jsx
const Inspector = ({ isVisible }) => {
  useEffect(() => {
    if (!isVisible) {
      return;
    }
    // Register event listeners
    return () => {
      // Unregister event listeners
    };
  }, [isVisible]);

  if (!isVisible) {
    // leave not so early
    return null;
  }
  return <div>...</div>;
};
```

As a consequence, all the effects will have the `isVisible` prop in their dependencies and potentially run too often (which can harm performance). I know, I should create an intermediate component that just rendrs nothing if `isVisible` is false. But why? This is only one example of the Rules of Hooks getting in my way - there are many others. One consequence is that a significant portion of the code of my React codebases is spent _satisfying the Rules of Hooks_.

The Rules of Hooks are a consequence of implementation detail - the implementation you chose for your hooks. But it doesn't have to be like that.

## [You've Been Gone Too Long](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#youve-been-gone-too-long)

You've been around since 2013, and you've made a point of keeping backward compatibility as long as possible. And I thank you for that - that's one of the reasons why I've been able to build a huge codebase with you. But this backward compatibility comes at a cost: documentation and community resources are, at best outdated, at worst, misleading.

For instance, when I search for "React mouse position" on StackOverflow, the first result suggests this solution, which was already outdated React a century ago:

```jsx
class ContextMenu extends React.Component {
  state = {
    visible: false,
  };

  render() {
    return (
      <canvas
        ref="canvas"
        className="DrawReflect"
        onMouseDown={this.startDrawing}
      />
    );
  }

  startDrawing(e) {
    console.log(
      e.clientX - e.target.offsetLeft,
      e.clientY - e.target.offsetTop
    );
  }

  drawPen(cursorX, cursorY) {
    // Just for showing drawing information in a label
    this.context.updateDrawInfo({
      cursorX: cursorX,
      cursorY: cursorY,
      drawingNow: true,
    });

    // Draw something
    const canvas = this.refs.canvas;
    const canvasContext = canvas.getContext("2d");
    canvasContext.beginPath();
    canvasContext.arc(
      cursorX,
      cursorY /* start position */,
      1 /* radius */,
      0 /* start angle */,
      2 * Math.PI /* end angle */
    );
    canvasContext.stroke();
  }
}
```

> Yuck

When I look for an npm package for a particular React feature, I mostly find abandoned packages with old, outdated syntax. Take [react-draggable](https://github.com/react-grid-layout/react-draggable) for instance. It's the de facto standard for implementing drag and drop with React. It has [many open issues](https://github.com/react-grid-layout/react-draggable/issues), and [low development activity](https://github.com/react-grid-layout/react-draggable/graphs/contributors). Perhaps it's because it's still class components based - it's hard to attract contributors when the codebase is so old.

As for your [official docs](https://reactjs.org/docs/state-and-lifecycle.html), they still recommend using `componentDidMount` and `componentWillUnmount` instead of `useEffect`. The core team has been working on a new version, called [Beta docs](https://beta.reactjs.org/), [for the last two years](https://github.com/reactjs/reactjs.org/issues/3308). They're still not ready for prime time.

All in all, the loooong migration to hooks is still not finished, and it has produced a notable fragmentation in the community. New developers struggle to find their way in the React ecosystem, and old developers strive to keep up with the latest developments.

## [Family Affair](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#family-affair)

At first, your father Facebook looked super cool. Facebook wanted to "Bring people closer together" - count me in! Whenever I visited your parents, I met new friends.

But then things got messy. Your parents enrolled in a [crowd manipulation scheme](https://en.wikipedia.org/wiki/Facebook%E2%80%93Cambridge_Analytica_data_scandal). They invented the concept of "Fake News". They started keeping files on everyone, without their consent. Visiting your parents became scary - to the point that I've [deleted my own Facebook account](https://www.facebook.com/help/delete_account) a few years ago.

I know - you can't hold children accountable for the actions of their parents. But you still live with them. They fund your development. They're your biggest users. **You depend on them**. If one day, they fall because of their behavior, you'll fall with them.

Other major JS frameworks have been able to break free from their parents. They became independent and joined a foundation called [The OpenJS Foundation](https://openjsf.org/). Node.js, Electron, webpack, lodash, eslint, and even Jest are now funded by a collective of companies and individuals. Since they can, you can, too. But you don't. You're stuck with your parents. Why?

## [It's Not Me, It's You](https://marmelab.com/blog/2022/09/20/react-i-love-you.html#its-not-me-its-you)

You and I have the same purpose in life: to help developers build better UIs. I'm doing it with [React-admin](https://marmelab.com/react-admin/). So I understand your challenges, and the tradeoffs you have to make. Your job is not an easy one, and you're probably solving tons of problems I even have no idea of.

---

# [Hacker News](https://news.ycombinator.com/item?id=32911492)

## BilalBudhani

I ditched React soon after they released hooks, mainly because I couldn't relate to the tradeoff React roadmap was taking from there. They went in a different direction from that point onwards, it seem like whatever code you write will become obsolete with the new set of best practices in the next release cycle.
More importantly, I realized React is trying to tame Facebook level of problems and hence their design decision steams from those data points. I develop small/medium type of frontend apps which doesn't need to apply solutions developed for such a scale.

These days I'm using Hotwire[^1] (Turbo + Stimulus) with fair amount of vanilla javascript libraries in my apps. Occasionally, when I need to develop a reactive piece of UI I reach out for Svelte[^2]

I'm quite happy after making the move. My apps complexity has reduced drastically and there is huge boost in my overall productivity.

[^1] https://hotwired.dev  
[^2] https://svelte.dev

### buscoquadnary

Step 1: The existing tooling is too clunky, big and a major PITA to work with, Developers spend most of their time fighting their framework and tooling to do simple things.  
Step 2: Someone gets fed up with this writes a framework that "does things right" and is designed for "simplicity"  
Step 3: People start loving the new tool because it is so much easier to work with.  
Step 4: People start to do things the tool wasn't designed to do. They start making "minor feature enhancements" to the tool so that it can fit more use cases.  
Alternative Step 4: Tool becomes "industry standard" so everyone starts using it because it is "the right way", regardless of whether or not it is a good fit.  
Step 5: The new tool becomes massive and bloated and overwhelmed with too many features, configurations, and options.  
Step 6: Return to step 1.

> The Wheel of Time turns, and Ages come and pass, leaving memories that become legend. Legend fades to myth, and even myth is long forgotten when the Age that gave it birth comes again. In one Age, called the Web 2.0 Age by some, an Age yet to come, an Age long past, a wind rose above the great mountainous island of FANNG. The wind was not the beginning. There are neither beginnings nor endings to the Wheel of Time. But it was a beginning.”

#### BilalBudhani

I don't agree with you.  
I have been doing Rails development for past 10 years now and I never faced a dilemma where the framework took a direction which isn't aligned with its core vision.  
I have been just trying to find a similar tool for frontend where I don't have to keep rewriting the entire codebase.

## gherkinnn

They absolutely do not have their place. Just about everything is worse with class components. I’ll take a dozen useEffects over a single class component any day.
That said, the hooks model is far from perfect. They give you a lot of rope to hang yourself with and were badly introduced. Within weeks the internet was ablaze with terrible advice.

When so many people get it wrong, the library is to blame. And I wish hooks were as robust as Solid.js’ signals model.

### mmis1000

I don't think hook themselves are a bad thing. But the way react implements hook probably is. The react team invented their hook format the suite themselves the most, but that probably isn't for other.
Vue 3 also has hook now. But none of these defects in the article exist.

In vue.

To use some value in a effect, you just use it and it is tracked.

If you need to clear up your code. You cut some code into a useXxx function, and your reusable utility is done. You can use it everywhere now. You don't really need to specify dependency of whatever by yourself.

If you must manipulate a dom, you just manipulate it. It will work as long as you revert the change before vue want to update it again.(And vue do provide a hook for you to attach a handler when these happen)

These restrictions are added by the way react implements hook, but not hook themselves. Hooks are just more user friendly services (by allow the hook to attach to component instance without all the glue codes(addListener or whatever))

#### KronisLV

> Vue 3 with the composition API looks fantastic on paper. (I haven’t used it in any meaningful way)

Recently worked on migrating a large codebase over from a legacy solution to Vue 3 with composition API, it was a pretty enjoyable experience, especially with Pinia!

Though I'd say that the problem was that most component libraries/frameworks out there actually don't support Vue 3 well enough. Last I checked, only the following were viable with Vue 3:

- Ant Design
- Element Plus
- PrimeVue (went with this, also has icons and a layout solution; also alternatives available for React and Angular)

Most of the other ones considered weren't quite there yet:

- Vuetify
- Quasar
- BootstrapVue
- Vue Material
- Buefy
- View UI
- Vuikit
- Chakra UI

I mean, is it really so hard to get a bunch of pre-built components for Vue 3 with Bootstrap, or Bulma? It feels a bit like the Python 2 to Python 3 migration in some respects.

#### mmis1000

I used it in a few project. And it reduces the code by a lot.
For example. To make a mutex to prevent duplicate submit of form. You use need to declare a instance field and wraps the code that do the submit. That alone is 3 lines of code but don't even include error handling.

But now I sealed it into a one line hook

```js
const wrap = useMutex()
const submit = wrap(async () = { … })
```

And then the submit can't run in parallel now.

# throwaway284534

As a developer who’s been working with React since the beta, I can confidently say that the author is speaking the truth. Especially so near the end of the article where they can’t seem to quit React.  
For all the annoyances of Hooks, they really are a godsend when it comes to composing state. And refs do indeed suck, but they sucked even more with class based components. I can’t tell you how many times I was able to solve a complex DOM state issue with custom hooks wrapped around refs.

Newer tools like Svelte and Solid do look promising as far as removing boilerplate, but they personally feel a step too far off the path of “it’s just JavaScript.”

Has anyone else here successfully left for greener JS pastures?

## nophunphil

I’m also a developer and tech lead who’s been working with React since the beta. Agreed with all your points about React. I’m not sure I would say Svelte and Solid are a farther step off the “just JavaScript” path than React given JSX though.

I haven’t tried Solid, but Svelte has already paid considerable dividends for our team. Frontend feature development pace is faster, the code is generally leaner, and the developers love working with it.

### egeozcan

I'm also a TL (which makes me a teaspoon here in Germany, which I like more than the tech lead title). I understand how the development can be faster with Svelte, but ecosystem argument really hits home. You'd get to 80% with Svelte perhaps much faster than React, but that missing library for, say, drag-and-drop makes that last 20% itself plus "hey let's develop our own drag-and-drop library in-house which should be easy and opinionated and maybe it gets open-sourced" (it will be hard, with crazy high budget, as it will try to cover many use-cases you will never have and it still won't be open-sourced because now it's your "core competency" and five months later someone will realize your component has terrible a11y and etc. and one million bug fixes later it is a monster code-base that none wants to touch and maybe rewrite? oh here we go again).

## fabian2k

The part about Redux and Context seems to be a complete misinterpretation of what Context is meant for. It was never meant to replace Redux, and as far as I know nobody from the React team has ever claimed something like that. State management in React is a topic discussed to death, there are plenty of options if you have specific tastes or requirements but plain old React state works perfectly fine as well (especially when coupled to server-side state libraries like React Query). But Context is not about state management, it does not seem useful to complain that it doesn't do a job well it was never meant to do.

The part about the Inspector component and the rules of hooks I don't understand. I would have put the visibility state outside the Inspector component, and then there is no need for any conditional calling of hooks.

## joshribakoff

Concurrent react actually makes your app less concurrent: https://github.com/facebook/react/issues/21668

5yrs in progress, it’s still not documented let alone fixed. I tried to look at the code, and they make giant PRs and are experimenting with priority queues and bitmasks, which seemed pretty off in the weeds to me.

## sergiotapia

Since quitting React I've been happier with my day to day. Phoenix Liveview came in clutch and showed me I don't have to put up with these kinds of self-inflicted problems.

If you're tired of React and the npm lunacy, I recommend you take a dip into Elixir and Phoenix Liveview. Take it for a spin, see how much better it is for you and your users. It's _sane_. You don't have to "split the context" anymore. xD

### azemetre

What are some resources (book or courses or videos or blogs) you'd recommend for learning Elixir and Phoenix?

#### jnsaff2

I can recommend this book currently in beta, that has been pretty good at keeping up to date with most developments in LiveView.
https://pragprog.com/titles/liveview/programming-phoenix-liveview/

#### krnsi

Better be fast: https://www.humblebundle.com/books/elixir-programming-pragmatic-programmers-books

#### sergiotapia

Easily these three courses: https://pragmaticstudio.com/
Phoenix Liveview, Elixir & OTP, and Full-stack Graphql with Phoenix.

Best way to learn Liveview.
