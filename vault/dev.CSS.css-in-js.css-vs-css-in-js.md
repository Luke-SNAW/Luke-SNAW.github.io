---
id: mvc57qhjuvlcihsoz9i94e5
title: "CSS vs. CSS-in-JS: How and why to use each"
desc: ""
updated: 1669177163730
created: 1669177021595
---

> https://blog.logrocket.com/css-vs-css-in-js/

## Pros of CSS-in-JS

A JavaScript developer may prefer to style things with CSS-in-JS rather than going through CSS classes. The biggest problem the CSS-in-JS approach solves is the global scope. It also has some other advantages that make a lot of sense if you are a JavaScript developer.

Let’s explore some of these benefits now.

### No scoping and specificity problems

Since styles are available in a local scope, they are not prone to clashing with the styles of other components. You don’t even have to worry about naming things strictly to avoid style clashes.

Styles are written exclusively for one component without prepending child selectors, so specificity issues are rare.

### Dynamic styling

Conditional CSS is another highlight of CSS-in-JS. As the button example above demonstrates, checking for prop values and adding suitable styles is way cooler than writing separate CSS styles for each variation.

### Less CSS specificity

CSS-in-JS helps you keep the specificity of CSS declarations to the lowest, as the only thing you style with it is the element itself. The same applies to creating component variations, where you can check for prop object values and add dynamic styling when required.

### Easy theming

[Theming apps with custom CSS properties](https://blog.logrocket.com/a-guide-to-theming-in-css/) makes sense. In the end, you will have to move to the JavaScript side and write the logic to switch and remember the theme based on user input.

CSS-in-JS allows you to write theming logic entirely in JavaScript. With the styled-components `ThemeProvider` wrapper, you can quickly color-code themes for components. Take a look at [this CodePen example](https://codepen.io/_rahul/pen/qBKXevo) to see component theming with styled-components in action:

### Painless maintenance

Considering the features and advantages CSS-in-JS offers, a JavaScript developer may find CSS-in-JS more convenient than managing hundreds of CSS files.

The fact remains, however, that one must have a good understanding of both JavaScript and CSS to effectively manage and maintain huge projects powered by CSS-in-JS.

## Cons of CSS-in-JS

CSS-in-JS does solve the scoping problem very well. But as we discussed initially, we have much bigger challenges — like render-blocking — that directly affect the user experience. Along with that, there are some other issues that the concept of CSS-in-JS still has to address.

### Delayed rendering

CSS-in-JS will execute JavaScript to parse CSS from JavaScript components, and then inject these parsed styles into the DOM. The more components more will be the more time taken by the browser for the first paint.

### Caching problem

CSS caching is often used to improve successive page load times. Since no CSS files are involved when using CSS-in-JS, caching is a big problem. Also, dynamically generated CSS class names make this issue even more complicated.

### No CSS preprocessor support

With the regular componentized CSS approach, it’s easy to add support for [preprocessors like SASS](https://blog.logrocket.com/how-to-write-reusable-css-with-sass/), Less, PostCSS, and others. The same is not possible with CSS-in-JS.

### Messy DOM

CSS-in-JS is based on the idea of parsing all style definitions from JavaScript into vanilla CSS and then injecting the styles into the DOM using style blocks.

For each component styled with CSS-in-JS, there could be 100 style blocks that must be parsed first, then injected. Simply put, there will be more overhead costs.

### Library dependency

As we already know, we can add CSS-in-JS functionality with an external library. A lot of JavaScript will be included and run before actual CSS parsing, as parsing styles from JavaScript to CSS styles depends on a library like styled-components.

### Learning curve

A lot of native CSS and SCSS features are missing with CSS-in-JS. It may be very challenging for developers who are used to CSS and SCSS to adapt to CSS-in-JS.

### No extensive support

Most of the UI and component libraries don’t support the CSS-in-JS approach right now, as it still has a lot of issues to address.

The problems discussed above may collectively contribute to a low-performant, hard-to-maintain product with several UI and UX inconsistencies.

## Recommendations for where to use CSS-in-JS

The CSS-in-JS solution is ideal when you are dealing with a smaller application for which performance is a lower priority. It may not be ideal when dealing with a performance-critical application with a huge design system.

As an app grows bigger, using CSS-in-JS can get complicated easily, considering all the drawbacks of this concept. A lot of work goes into converting a design system into CSS-in-JS, and in my opinion, no JavaScript developer would want to deal with that.

## Pros of CSS Module

The most significant benefit that CSS Module offers is removing the reliance on CSS-in-JS to fix the scoping and specificity problems. If we can fix the scoping and specificity problems by keeping CSS as traditional as possible, CSS-in-JS will be more work than necessary.

### No scoping and specificity issues

As demonstrated in the example above, CSS Module successfully solves the scoping problem we have with traditional, old-style CSS. As the rules are loosely written in CSS Module files, it’s rare to observe any specificity problems.

### Organized code

Keeping separate CSS files may appear to be a limitation. However, this method actually promotes better organization. For example, here’s how I organize components by separating them into their own folders:

```
- Project
  - src
    - components
      - Button
          - Button.jsx
          - Button.modules.css
      - Carousel
          - Carousel.jsx
          - Carousel.modules.css
```

### Caching possibilities

The minified CSS files generated with the final build can be cached by the browser to improve the successive page load times.

### CSS preprocessing

It’s easy to add support for [CSS preprocessors like PostCSS](https://blog.logrocket.com/using-postcss-media-queries-level4/), SASS, Less, and others. However, you have to rely on additional packages to do so.

### Zero learning curve

If you know how CSS works, you can use CSS Module without learning anything new besides the few points that we discussed above in the intro segment.

### Great support

You won’t need to add additional packages to use CSS Modules. All major frameworks and libraries provide inbuilt support.

## Cons of CSS Module

While CSS Module offers many benefits, it’s not a perfect solution. Below are some considerations to keep in mind.

### The nonstandard `:global` property

When targeting selectors in the global scope, you must use the `:global` rule. This not a part of CSS specifications but is used by JavaScript to label global styles.

### No dynamic styles

With CSS Module, all the declarations go into separate CSS files. It’s therefore impossible to implement dynamic styles like CSS-in-JS, as we can’t implement any JavaScript in CSS files.

### External CSS files

You can’t omit the usage of CSS files with CSS modules in your components. The only possible way to use CSS modules is to maintain and import external CSS files.

### TypeScript limitation

To use CSS Modules with TypeScript, you have to add module definitions in the `index.d.ts` file or [use a webpack loader](https://blog.logrocket.com/how-to-configure-css-modules-webpack/):

```ts
/** index.d.ts **/
declare module "*.module.css" // TS module for CSS Module files
declare module "*.module.scss" // TS module for CSS Module files in SCSS format
```

## Recommendations for where to use CSS Module

Using CSS Module is a good choice if you have a performance-critical application with a large UI. Since everything offered by CSS Module is ultimately based on traditional, non-experimental usage, this method makes it easier to monitor and fix performance.

The CSS Module files are simple to adapt code from any CSS framework of your choice since all you’re dealing with is CSS. Some basic knowledge of CSS is sufficient for this task, as discussed previously.
