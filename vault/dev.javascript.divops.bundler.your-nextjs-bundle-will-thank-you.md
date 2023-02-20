---
id: 9ju4drok0fv1fml7977iyba
title: Your Nextjs Bundle Will Thank You
desc: ''
updated: 1667882410996
created: 1667881389948
tags:
  - performance
  - divops
  - bundler
---

> https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you

## Initial Check

I did some checking, ran a couple of Lighthouse reports, and ended up with an average performance score of **35 points** on both mobile and desktop. Effectively they were not wrong, some problems were there. After a quick check of the report, I moved on to another type of testing, launching a production build to check the beautiful report that Next provides us. The result made me **jump out of my chair**.

## [Analyzing Problems](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#analyzing-problems)

### [JS Shared By All Files](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#js-shared-by-all-files)

### [CSS is Not Included in the Calculation](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#css-is-not-included-in-the-calculation)

## The Magic Madness of Barrel Files

Just to be clear, what is a Barrel File? Well, do you know when you put all your exports into an index.js file to have easier import paths? This is a Barrel File. (Did you know that the Node.js creator [has regrets about having created it](https://youtu.be/M3BM9TB-8yA?t=883)?)

...

If you notice inside the components folder, there is a seemingly harmless file that has never been mentioned so far the index.js:

```js
export * from "./auth-form"
export * from "./button"
export * from "./movie-autocomplete"
export * from "./navbar"
export * from "./phone-input"
export * from "./random-table"
export * from "./side-menu"
```

Think for a second about what is going on in this file, this file is responsible for exporting all the components within the components folder, to make them usable with a lighter import syntax. I will paste here the differences between the two import versions:

```js
import { Navbar } from "../components" // Version 1
import { Navbar } from "../components/navbar" // Version 2
```

So yes, we save a subdirectory, but what is the consequence then? It will be enough to import even one tiny module from this index.js to cause a massive import of all other components within the page bundle.

## Why is this happening?

So far we have discovered and solved the problem of having all pages with a giant bundle composed of unused dependencies, and we saw that the cause of this was an import from an index.js file, now I would like to explain why this thing causes this problem.

Normally, on a production build, JavaScript code undergoes several operations including removing unused modules, this specific phenomenon is called **Tree Shaking**. And you can imagine it this way: there’s a nice tree in your garden, that tree is your app source code, the green, and healthy leaves are the modules that your app uses, instead the brown and almost dead leaves are the unused modules.

## The Alternative Solution

> Yes, all is very nice, but isn’t there a way to have the same result by keeping index.js?

Actually, there is, (most of the time) an alternative solution for you.

As you just read, Terser is doing a nice job, but sometimes it’s not perfect. To make it work better, we can give webpack a nice hint called sideEffects. This value can be put into a package.json and accepts RegEx, Strings, and Boolean as values. **But what exactly a side effect is**?

Well, official documentation can help us:

> A “side effect” is defined as code that performs a special behavior when imported, other than exposing one or more exports. An example of this are polyfills, which affect the global scope and usually do not provide an export.

For example in our case we don’t use any side effects, so we can set directly false, helping webpack pruning the unused modules:

```json
{
  "sideEffects": false
}
```

### A Smart Question

Do you remember when we removed the AuthForm and the Navbar component from the signin.js page? We initially solved the problem, but am I mistaken, or was there still an imported dependency present?

```js
import { Box } from “@mui/material
```

Why did this dependency not continue to cause the problem of the other two? Yet here again a [barrel file](https://github.com/mui/material-ui/blob/master/packages/mui-material/src/index.js#L51) is used to export all the components, and well, the answer again can be [found here](https://github.com/mui/material-ui/blob/master/packages/mui-material/package.json#L76). And if you are wondering, [ChakraUI](https://github.com/chakra-ui/chakra-ui/blob/main/packages/components/accordion/package.json#L27) is using the same on all the components, and [MantineUI](https://github.com/mantinedev/mantine/blob/master/src/mantine-core/package.json#L10) is using it too, even [Lodash](https://github.com/lodash/lodash/blob/master/package.json#L10) (in the ESM version) takes advantage of this technique.

## [Common Tips to Enhance Tree Shaking](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#common-tips-to-enhance-tree-shaking)

### [Use Tree Shakeable Library](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#use-tree-shakeable-library)

Again, it can be a cliché but is very common to see projects with tons of non-tree-shakeable dependencies, how can you know if one of them is tree-shakeable or not? Using tools like [BundlePhobia](https://bundlephobia.com/).

### [Avoid Transpiling to CommonJS](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#avoid-transpiling-to-commonjs)

You should configure your bundler to leave intact all your ESM instead of transpiling it into CJS, otherwise, the tree-shaking will be much more difficult to be applied from the bundler. You can make this for example with Babel using this piece of code:

```json
export default {
  presets: [
    [
      "@babel/preset-env",
      {
        modules: false,
      },
    ],
  ],
};
```

### [Avoid Star Imports](https://renatopozzi.me/articles/your-nextjs-bundle-will-thank-you#avoid-star-imports)

You should import only the modules you need, avoid importing \* from a module, otherwise everything will be included in your code chunk, even if it’s unused!
