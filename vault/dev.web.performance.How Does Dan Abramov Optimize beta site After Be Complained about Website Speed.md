---
id: xq0inpktt8bl1tp0vuqd7gi
title: "How Does Dan Abramov Optimize beta.reactjs.org After Be Complained about Website Speed?"
desc: ""
updated: 1655855318894
created: 1655855263863
---

An interesting thing happened in the open-source community a few days ago, it was about React maintainer Dan Abramov and Vue creator Evan You.

With the official release of React18, the React team has also created a new documentation website.

[

## React Docs Beta

### We are rewriting the React documentation with a few differences: All explanations are written using Hooks rather than…

beta.reactjs.org

](https://beta.reactjs.org/)

Then there are users who say that the user experience of the new website is great:

But Evan You expressed a different opinion. After performing performance tests, Evan believes that Vue’s official website performs better than React.

![](https://miro.medium.com/max/946/1*54qqOPTYoXnoVmOIHyEuWQ.jpeg)

![](https://miro.medium.com/max/946/1*9GNaZxVxu598RiVhVfPq9Q.jpeg)

←React vs Vue→

Then Dan responded: it is only a beta website.

Well, although Dan didn’t refute much in his mouth, he showed his importance to this matter with practical actions. After all, this is a question from Evan 😏 😏. React and Vue has been vying for the honor of being the best front-end framework for years.

In the next 3 days, Dan submitted many commits in a row and optimized the new website from various aspects.

![](https://miro.medium.com/max/700/1*O9sN6c5nAgMnxRMoW6LiWg.png)

Here let us learn how to improve the performance of a website from Dan’s commits.

# Website Optimization

There are two main aspects of Dan’s optimization:

- In the compilation, reduce the size of the packaged code.
- In the runtime, lazy-load if the code is not necessary for the First Contentful Paint(FCP).

> The First Contentful Paint (FCP) metric measures the time from when the page starts loading to when any part of the page’s content is rendered on the screen. For this metric, “content” refers to text, images (including background images), `<svg>` elements, or non-white `<canvas>` elements.

## Only import code you truly need

The previous code would import a file called `utils`. But not every function in `utils` will be used in the FCP, so Dan decided to split this file into different files and import them as needed, which can reduce the size of the bundle file.

![](https://miro.medium.com/max/700/1*7rn6x_u83IjlT4CU7pqutA.png)

![](https://miro.medium.com/max/700/1*JYu2SgDq9oIvodJRAIdhdQ.png)

## Build for modern browsers

This website uses the Nextjs framework under the hood, which is not optimized for modern browsers by default.

And we know that in order to be compatible with old browsers, frameworks such as Nextjs will perform a lot of polyfills, which will increase the size of the packaged files.

The audience of React’s documentation is all front-end developers, and they basically don’t use old browsers. So we can let Nextjs turn on optimizations for modern browsers.

Dan enabled this feature with this configuration:

![](https://miro.medium.com/max/700/1*Kenb9o7TRGZ8sKPKBY8hAA.png)

legacyBrowsers: false,

browsersListForSwc: true,

## Lazy loading of non-essential resources

The new documentation embeds a lot of code examples from `codesandboxes` that rely on the `CodeMirror linter`, but this is not essential for FCP.

So Dan lazy-loads this part of the resource:

![](https://miro.medium.com/max/700/1*8zuPNErMLhnB8AK9iugRQg.png)

# Result

After these optimizations, beta.reactjs.org is faster.

![](https://miro.medium.com/max/1990/1*DlxFSpojYN-TwFjeXAPYbQ.jpeg)

![](https://miro.medium.com/max/2016/1*bFCIJDknxch9YkDYrxI7MA.jpeg)

←React vs Vue→
