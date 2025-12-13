---
id: 78dfzzy16rxii38x2wnzh3n
title: tailwind-is-an-anti-pattern
desc: ''
updated: 1658217095034
created: 1658216990738
---

> https://javascript.plainenglish.io/tailwind-is-an-anti-pattern-ed3f64f565f0

_Let us open Schrödinger’s Box to see what’s inside. Spoiler: It’s a dead cat._

Many people like Tailwind’s so-called “utility-first” approach, and I understand why. However, you should know that this technique is nothing new. As a matter of fact, there were small CSS snippets that existed way before Bootstrap that came with classes like `.p-8`. They were not considered a library or framework; they were merely snippets copied from project to project. Nevertheless, the technique itself is _not new_. With the rise of Bootstrap, however, we stopped doing that. One reason — of course — is that Bootstrap came with its own utility classes, but there’s another reason, and you should be aware of that before starting to use Tailwind in every project.

## What does Tailwind do?

Since I couldn’t find any better way to insult Tailwind than using their own examples, let’s stick to that. Note that I have a TailwindUI account, as some of my customers insist on using that. So, I don’t just blame the free examples, but you literally pay for broken code. But let us stick to the free “Hero Section” example so that everybody can access it and follow my thoughts ([https://tailwindui.com/components/marketing/sections/heroes](https://tailwindui.com/components/marketing/sections/heroes)).

**Problem one, bloated HTML:**

Just look at the button:

```html
<button
  type="button"
  **class="bg-white rounded-md p-2 inline-flex items-center justify-center text-gray-400 hover:text-gray-500 hover:bg-gray-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500"
  **
  aria-expanded="false"
>
  <span class="sr-only">Open main menu</span>

  <!-- Heroicon name: outline/menu -->
  <svg
    class="h-6 w-6"
    xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)"
    fill="none"
    viewBox="0 0 24 24"
    stroke-width="2"
    stroke="currentColor"
    aria-hidden="true"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="M4 6h16M4 12h16M4 18h16"
    />
  </svg>
</button>
```

Holy smokes, what a list of classes. What does it look like? What does the button do? Well, it’s hard to figure out. Here’s the same example without Tailwind:

```html
<button type="button" **class="button-menu-toggle" ** aria-expanded="false">
  <span class="sr-only">Open main menu</span>

  <!-- Heroicon name: outline/menu -->
  <svg
    class="h-6 w-6"
    xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)"
    fill="none"
    viewBox="0 0 24 24"
    stroke-width="2"
    stroke="currentColor"
    aria-hidden="true"
  >
    <path
      stroke-linecap="round"
      stroke-linejoin="round"
      d="M4 6h16M4 12h16M4 18h16"
    />
  </svg>
</button>
```

At first glance, we know this is the button responsible for toggling the menu (note that I don’t use BEM, which is an Anti-Pattern, too). Code is read much more often than it is written; consider that when thinking about Tailwind.

Now, every time I bring this up, there’s at least one developer who blames me for not knowing about `@apply`. Trust me, I know. But it defeats Tailwind’s own purpose as you will then just write regular CSS. Of course, you may mix both techniques, but then again, you have two ways of writing CSS. If you’re also inlining some CSS, then it’s even three. `@apply` makes everything worse.

**Problem two, naming things**

Tailwind claims

> You have to think up class names all the time — nothing will slow you down or drain your energy like coming up with a class name for something that doesn’t deserve to be named. — [https://tailwindcss.com/docs/reusing-styles](https://tailwindcss.com/docs/reusing-styles)

“Something that doesn’t deserve to be named” also doesn’t deserve utility classes. As a matter of fact, CSS got you covered. Take a look at another snippet of the Hero Section:

```html
<div **class="hidden md:block md:ml-10 md:pr-4 md:space-x-8" **\>
  <a href="#" **class="font-medium text-gray-500 hover:text-gray-900" **\
    >Product</a
  >
  <a href="#" **class="font-medium text-gray-500 hover:text-gray-900" **\
    >Features</a
  >
  <a href="#" **class="font-medium text-gray-500 hover:text-gray-900" **\
    >Marketplace</a
  >
  <a href="#" **class="font-medium text-gray-500 hover:text-gray-900" **\
    >Company</a
  >
  <a href="#" **class="font-medium text-indigo-600 hover:text-indigo-500" **\
    >Log in</a
  >
</div>
```

Here’s how to do it with CSS:

```html
<div
  **class="navigation-desktop"
  **
  role="navigation"
  aria-label="Main Navigation"
>
  <a href="#">Product</a>
  <a href="#">Features</a>
  <a href="#">Marketplace</a>
  <a href="#">Company</a>
  <a href="#">Log in</a>
</div>
```

It shows the marketing gibberish they push on you to make you buy their rubbish. Of course, the CSS would be in its own stylesheet, cut the CSS in JS (which is also an Anti-Pattern).

```css
.navigation-desktop {
  display: none;
}
.navigation-desktop > a {
  font-weight: 500;
  color: rgb(107 114 128);
}
.navigation-desktop > a:hover {
  color: rgb(17 24 39);
}
[@media](http://twitter.com/media) (min-width: 768px)
{
  .navigation-desktop {
    display: block;
    margin-left: 2.5rem;
    padding-right: 1rem;
  }

  .navigation-desktop > \* + \* {
    margin-left: 2rem;
  }
}
```

I didn’t have to come up with a class name for my anchor tags; everybody knows from the parent element that this is supposed to be the desktop nav (why they are using a div is beyond me, but I am not going to fix their broken markup now). Looking at the Tailwind code, you will just be overwhelmed and surrender to your fate. And you know another great thing about my solution: It works in any project; it doesn’t depend on any library.

Most vital for you as a developer: The HTML markup stays readable and is not bloated. It’s the first thing you ship to your users, after all.

**Problem three, jumping around files**

Tailwind claims

> You have to jump between multiple files to make changes — which is a way bigger workflow killer than you’d think before co-locating everything together. — [https://tailwindcss.com/docs/reusing-styles](https://tailwindcss.com/docs/reusing-styles)

This defeats the whole purpose of having CSS in the first place. Before Tailwind, we could have also just inlined every style. However, separating styles from markup is an important feature. Without Tailwind, you can learn to write much more usable code since Tailwind tightly couples your CSS to its markup. Again, I am aware of @apply, but then I could just stick to common CSS and throw the whole Tailwind toolchain right out the window — where it belongs.

**Problem four, changing CSS is scary**

Tailwind claims

> Changing styles is scarier — CSS is global, are you _sure_ you can change the min-width value in that class without breaking something in another part of the site? — [https://tailwindcss.com/docs/reusing-styles](https://tailwindcss.com/docs/reusing-styles)

CSS is not necessarily global. With ShadowDOM and CSS Modules, we have two strong tools at our disposal that take care of CSS classes that would otherwise be problematic. We don’t have to come up with crazy names anymore (which makes BEM obsolete, too). Also, is 30 different classes slapped into an HTML element’s class attribute supposed to be any better? How so? Offical example incoming:

```html
<button
  type="button"
  **class="inline-flex items-center px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
  **\
>
  _<!-- Heroicon name: solid/check -->_
  <svg
    class="-ml-1 mr-2 h-5 w-5"
    xmlns="http://www.w3.org/2000/svg"
    viewBox="0 0 20 20"
    fill="currentColor"
    aria-hidden="true"
  >
    <path
      fill-rule="evenodd"
      d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
      clip-rule="evenodd"
    />
  </svg>
  Publish
</button>
```

The above gibberish will render this button:

![](https://miro.medium.com/max/189/1*TX_F7o3Mq5DwP438FsGYnA.png)

[https://tailwindui.com/components/application-ui/headings/page-headings](https://tailwindui.com/components/application-ui/headings/page-headings)

First, note the `<button type="button"` which is redundant since this button is outside of a form element. Other than that, it’s an awful lot of classes to render a simple purple button. It probably wouldn’t be as problematic if the HTML file only contained this one button, but every element looks like that in Tailwind. Behold the TailwindUI source code:

![](https://miro.medium.com/max/700/1*B_-tu67LyUD9r08_5Z-J_Q.png)

Why? [https://tailwindui.com/](https://tailwindui.com/) source…

Don’t repeat yourself (DRY)? I’d say, You Ain’t Gonna Need It. I find this one scarier than having a `.button-action` class where _I know_ what happens. It’s _not scary_ to change it because it’s my architecture, and _I can rely on it_. I also don’t have to write something like `scale-[calc(204/299)]`I would be scared to change it, though. Magic numbers, anyone? THAT code smells.

**Problem five, big bundles**

Tailwind claims

> Your CSS bundle will be bigger — oof. — [https://tailwindcss.com/docs/reusing-styles](https://tailwindcss.com/docs/reusing-styles)

That’s a straight-up lie. Tailwind doesn’t magically reduce your bundle size. You just shift part of the size to your HTML file. Also, you might declare redundant properties in classes, which would ultimately increase bundle size. But you don’t have to ship all the properties that you’re using in your project. In Tailwind, you do. The toolchain scans your project, then creates the Tailwind bundle. This bundle contains any property that you’re using throughout the project. Even if the user never visits any site with that specific property. An issue you don’t have with CSS Modules or Web Components. Tailwind removes one problem and replaces it with another—nothing more, nothing less.

The landing page of tailwindui.com uses about 20% of the CSS it initially ships to your browser.

![](https://miro.medium.com/max/700/1*OsgBkHEj_NJij4qWr2sEtQ.png)

Unfortunately, that’s nothing quite unusual. Most websites ship a lot of unused CSS — Tailwind or not. We as developers should work on it, but Tailwind certainly won’t help solve it. It’s also a matter of protecting our scarce resources: Saving bytes ultimately means saving power. Every effort — and be it so little — counts.

CSS has improved since the dark ages of Bootstrap and the likes. Because we have native variables, grids, and CSS Modules at our disposal, there’s little to no reason to use SCSS, Bootstrap, or Tailwind.

Another issue is that you’re not learning CSS patterns by using Tailwind. E.g., what does `space-x-8` do? It will translate to `.your-element > * + * { margin-left: 2rem; }` which is a typical design pattern in CSS. Do you know what it does? It is so common that you should be able to recognize this pattern at first glance!

If you’re a beginner in CSS, Tailwind is the safest way that you will remain a beginner. And even more than that, adapting their broken HTML semantics leaves you with a website that doesn’t live up to modern standards—even the ones you pay for at TailwindUI. They’re using divs where they’re supposed to be using more semantic tags; also, they don’t always add aria-roles needed to provide an accessible website. Examples? Random h2, h3, h4 tags, hilarious ul/li footer navigations without any role or semantic tags, unequal font sizes for headlines of the same level, using spans for subheadlines, … And they charge an awful lot of money for that. Unfortunately, I cannot hand you the code for the examples, as you have to **pay** for them.

Yes, there’s a lot of personal pain and a lot of personal opinions. I am aware of that. Separation of concerns and skipping to learn important CSS patterns remain problematic, though. Where are you gonna go when Tailwind is obsolete? CSS is here to stay. I can use both. I am forced to use Tailwind for some clients because it’s simply part of their toolchain. And who am I to change their decisions as an external developer? I still find it problematic.

The problems outlined were also the reason why we ditched that “utility classes” approach in the first place. It’s not flexible enough. When there are new CSS features, will you wait until Tailwind implements them? Your projects will end up having several escape hatches: Using `@apply`, creating custom classes because you cannot remember the `background-image` syntax of Tailwind, or even overriding Tailwind classes instead of extending the configuration file — because it’s CSS, so why not, right?

That’s all, folks!

Consider leaving a like or follow so I know which kind of articles you like to read more. Thank you so much for reading.

**Disclaimer:** No cats have been harmed during the writing of this article.
