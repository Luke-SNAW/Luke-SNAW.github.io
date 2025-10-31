
https://daverupert.com/2022/04/7-web-component-tricks/

# 1. You can manipulate props right on a Lit element

This may be something only I would do, but if you make an element with Lit that exposes its properties, you can edit those props externally using `querySelector`.

```html
<my-counter counter="3"></my-counter>

<script>
  const myCounter = document.querySelector("my-counter");
  myCounter.counter = 10;
</script>
```

# 2. :host-context let’s you style an element based on its parent

You can use `:host-context()` to style an element based on its parent. Your HTML may look like this:

```html
<my-element></my-element>
<div class="card"><my-element></my-element></div>
```

In your CSS inside the Web Component, you have something like this:

```css
:host-context(.card) {
  background: pink;
}
:host-context(.card)::after {
  content: "I’m in a card";
}
```

[See Example](https://codepen.io/davatron5000/pen/jOYKKPN)

# 3. Declarative ShadowDOM

```html
<my-element>
  <template shadowroot="open">
    <p>I'm a spooky skeleton screen 💀</p>
  </template>
</my-element>
```

Declarative Shadow DOM enables server-side rendering of Web Components, but one thing that’s not clear is your inlined template and the components actual template can be totally different.

[See Example](https://codepen.io/davatron5000/pen/PoEBezm)

# 4. Open WC has a project starter

If you’re looking for a `create-react-app` for Web Components, the folks at Open WC have you covered.

```html
npm init @open-wc
```

You get so much from this (local server, testing configs, a storybook, production rollup config, etc) but my favorite bit is from the sample component’s test file: it runs an [accessibility audit](https://open-wc.org/docs/testing/chai-a11y-axe/) on your Shadow DOM!

```jsx
it("passes the a11y audit", async () => {
  const el = await fixture(html`<custom-element></custom-element>`);

  await expect(el).shadowDom.to.be.accessible();
});
```

Accessibility out of the box! Nice.

# 5. You can “rebrand” other people’s components.

Want to mix and match components from different design systems but keep a consistent naming structure in your company? You can import a component and “rebrand” it or even add functionality.

```jsx
import { CoolButton } from 'cool-design-system'

class OurButton extends CoolButton {
	constructor { super() }
}

customElements.define('our-button', OurButton)
```

# 6. The Open WC Publishing Guides are cool

The OpenWC group also has some nice [community guidelines for publishing Web Components](https://open-wc.org/guides/developing-components/publishing/).

> ✅ Do publish latest standard EcmaScript  
> ✅ Do publish standard es modules  
> ✅ Do include `"main": "index.js"` and `"module": "index.js"` in your `package.json`  
> ✅ Do export element classes  
> ✅ Do export side effects separately  
> ✅ Do import 3rd party node modules with “bare” import specifiers  
> ✅ Do include file extensions in import specifiers
>
> ❌ Do not optimize  
> ❌ Do not bundle  
> ❌ Do not minify  
> ❌ Do not use `.mjs` file extensions  
> ❌ Do not import polyfills

That’s helpful and hopefully provides a consistent experience, allowing for a consistent bundling story, and preventing weird footguns that might occur when trying to use other people’s Web Components in your project.

# 7. You don’t need build tools until the very, very end.

If you want to write Web Components, you can write vanilla web components and use ES Modules to join them together. You can use a web component library like Lit with an `import` statement pointed at `skypack.dev` or `unpkg.com`. It’s super handy to get started with zero tooling.

If you want to install packages off of `npm` … you could try [Import Maps](https://github.com/WICG/import-maps) … but otherwise you’ll need a local dev server (`vite` or `@web/dev-server`) that supports “bare import specifiers”.

It’s only when going to production that you need tooling specific to your site’s needs. TypeScript is optional, bundling is optional, minifying code is optional. From a Web Component perspective, these are all considered “application-level concerns” that happen at deployment time.

[Rollup build script examples](https://open-wc.org/docs/building/rollup/) are out there, but Web Components don’t prescribe how to build your application, they don’t hitch you to an architecture. It could be a whole tree-shaken SPA (single page app), but Web Components also work well in a MPA (multi-page app) architecture. It’s up to you and your application to figure out what fits best.
