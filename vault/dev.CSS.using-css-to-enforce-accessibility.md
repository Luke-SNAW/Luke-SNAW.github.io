---
id: mk6v96zs2dgv83tuysal6hk
title: Using CSS to Enforce Accessibility
desc: ""
updated: 1666678731771
created: 1666678551871
---

> https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html

I am a big proponent of the [First Rule of ARIA](https://www.w3.org/TR/using-aria/#rule1) (don’t use ARIA). But ARIA brings a lot to the table that HTML does not, such as complex widgets and state information that HTML does not have natively.

A lot of that information can be hidden to the average developer unless they are checking the accessibility inspectors across browsers or testing with a suite of screen readers. This is one of the reasons I always advocate for making your styles lean on structure and attributes from the DOM, to make it easier to spot when something is amiss.

It is also, in my opinion, a way to reduce the surface area for accessibility bugs. If your sort icon orientation is keyed to the ARIA property that conveys that state programmatically, then getting that ARIA property wrong will have two effects — a broken interface and a weird icon. Addressing the accessibility issue will fix the visual style.

## [CSS as Accessibility Detector](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Detector)

None of this is new. Others have talked, written, and coded about it. I have taken it for granted since attribute selector support became widespread in the first decade of the 21st century. But I regularly work with folks who do not come at CSS from the same place I do.

Instead of preaching concepts, let me toss some examples out. Each of these links to a blog post where I explain the styles, how the selector is keying off the HTML, what WCAG Success Criteria they help support, and if there are any gotchas. Please read at least the linked sections of those posts for more detail.

### [Keyboard](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Keyboard)

In my post [Under-Engineered Responsive Tables](https://adrianroselli.com/2020/11/under-engineered-responsive-tables.html#CSS) I use the following CSS to ensure content is not clipped unless it will be accessible to keyboard users, _without_ creating a confusing mess for screen reader users:

```css
[role="region"][aria-labelledby][tabindex] {
  overflow: auto;
}

[role="region"][aria-labelledby][tabindex]:focus {
  outline: 0.1em solid rgba(0, 0, 0, 0.1);
}
```

### [Hidden](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Hidden)

In [Disclosure Widgets](https://adrianroselli.com/2020/05/disclosure-widgets.html#CSS), the following CSS only hides content when the programmatic state of the trigger (assuming it is the previous sibling) has been correctly set to convey the content it controls is hidden:

```css
button[aria-expanded="false"] + * {
  display: none;
}

button[aria-expanded] + * {
  /* Don't need anything here. */
}
```

I use a similar approach in my post [Under-Engineered Dependency Questions](https://adrianroselli.com/2021/12/under-engineered-dependency-questions.html). Choosing a radio button for “Other” in a set of options shows a text box, provided your HTML structure is simple. An ID selector with a couple pseudo-classes and a general sibling combinator can go a long way:

```css
#p5:not(:checked) ~ div {
  display: none;
}
```

_Added, 25 July 2022_: With support for `:has()` finally coming to browsers, I can point to this example I use in the [accordion](https://adrianroselli.com/2020/05/disclosure-widgets.html#Accordion) for my [Disclosure Widgets](https://adrianroselli.com/2020/05/disclosure-widgets.html#CSS) post:

```css
h2:has(> button[aria-expanded="false"]) + div {
  display: none;
}
```

Essentially the container that follows the heading goes away when the button in the heading says it is not expanded.

### [Sort](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Sort)

When writing about [Sortable Table Columns](https://adrianroselli.com/2021/04/sortable-table-columns.html#State), I do not go into detail in the CSS but the selectors are pretty clear in their reliance on the sort property:

```css
[aria-sort="ascending"] > button svg.asc {
  stroke: var(--col-header-color);
  fill: var(--col-header-color);
}

[aria-sort="descending"] > button svg.des {
  stroke: var(--col-header-color);
  fill: var(--col-header-color);
}
```

### [Error](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Error)

My [Under-Engineered Text Boxen](https://adrianroselli.com/2019/09/under-engineered-text-boxen.html#Errored) lean on native HTML attributes along with ARIA properties, such as when the state of a control is invalid:

```css
textarea[aria-invalid="true"],
textarea[aria-invalid="spelling"],
textarea[aria-invalid="grammar"],
input:not([type="checkbox"]):not([type="file"]):not([type="image"]):not([type="radio"]):not([type="range"])[aria-invalid] {
  background: linear-gradient(
    135deg,
    rgba(255, 0, 0, 1) 0,
    rgba(255, 0, 0, 1) 0.4em,
    rgba(255, 255, 255, 1) 0.4em
  );
}
```

### [Current](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Current)

Of course I cover the most common one, showing the current page in a set of navigation links, in [Link + Disclosure Widget Navigation](https://adrianroselli.com/2019/06/link-disclosure-widget-navigation.html#Links):

```css
a[aria-current="page"] {
  background-color: #187aba;
  border-color: #187aba;
}
```

### [Busy](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Busy)

For a twist, [More Accessible Skeletons](https://adrianroselli.com/2020/11/more-accessible-skeletons.html#CSS) uses CSS to spackle over a gap in ARIA support:

```css
*[aria-busy="true"],
.skeleton[aria-hidden="true"] {
  display: none;
}
```

## [What if I Use an Abstraction?](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Abstraction)

The challenge I run into again and again is with developers who do not know CSS, either at all or very well. Whether they rely on a CSS-in-JS approach, or a class-driven model like Tailwind or BEM, I find they struggle with first understanding the concept of using CSS as I outlined, but then with how to write the syntax in their tooling to make it work.

I am not making fun of Tailwind or BEM (though [I may have done that](https://twitter.com/aardrian/status/1405965407719235589) in [the past](https://twitter.com/aardrian/status/1164956147499053056)). I do not know either syntax (nor do I know SCSS, SMACSS, SASS, SFPD, and so on) and am not motivated to since my CSS knowledge is older and works everywhere.

I have no answers here, but I decided to [ask on Twitter](https://twitter.com/aardrian/status/1408124998389317644).

I encourage you to read the responses. Much of what I propose above will not work with Tailwind’s structure. Much of the feedback came down to either serving a static CSS file (while watching for layout conflicts) or integrating these styles with an [`@layer` directive](https://tailwindcss.com/docs/functions-and-directives#layer) to drop it into the place in the generated Tailwind file where you want it.

Phil Wolstenholme started [offering feedback immediately](https://twitter.com/philw_/status/1408125911023636484) and then wrote a post directly after with Tailwind-specific feedback: [Tying Tailwind styling to ARIA attributes](https://dev.to/philw_/tying-tailwind-styling-to-aria-attributes-502f).

If you use Tailwind, I encourage you to read it (and then maybe leave a comment there or here with feedback). If you do not use Tailwind, maybe some of those concepts can apply in your tools of choice.

Based on the overall responses, and my own digging into BEM, it looks like the selectors I outline above are well outside the scope of what these tools offer. For other tooling, I encourage you to offer your own experience in the comments.

## [Takeaway](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Takeaway)

Look, I can’t keep giving you free code. Some day I will be dead.

### [CSS](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#CSS)

Many of the [global ARIA states](https://www.w3.org/TR/wai-aria-1.1/#global_states) (but not properties) are great as styling hooks. Getting familiar with [all ARIA states and properties](https://www.w3.org/TR/wai-aria-1.1/#state_prop_def) that are available across widgets and other uses can be handy as well.

Every time you come up with a style that reflects a state or property of something (open, closed, expanded, collapsed, on, off, checked, disabled, busy, locked, selected, sobbing uncontrollably), do not use a class. At least not at first. Look at the programmatic change that happens to the underlying HTML that makes that thing happen.

Try to use that as your styling hook instead. Write it in a way where if that change does not happen, neither does your style.

### [Tools](https://adrianroselli.com/2021/06/using-css-to-enforce-accessibility.html#Tools)

Just as every problem looks like a nail when you are equipped with only a hammer, every layout or styling or widget challenge looks like something you solve with a `class` when you choose some self-described utility-first CSS tooling. Or JavaScript.

If you use these tools, you still need to know CSS. On top of that, you may need to know the tools’ syntax in order to incorporate any CSS that goes beyond what they offer.

If you have a hand in building these tools, please consider how you can use CSS that promotes and reinforces good and accessible underlying HTML syntax.

If you are building these kinds of tools because you only know how to style things with classes, then maybe go back and learn CSS first. And HTML. And ARIA. And WCAG. And accessibility. And maybe throw in some microdata formats too. _Then_ take that experience into the tool you want to build.

---

As an aside, I have a built-in bias against Tailwind. Not because of the technology; I see this stuff emerge over and over again and they all have a limited shelf life. My issue is with how its creator chooses to [engage with people online](https://twitter.com/adamwathan/status/1390663794985250816) who are not even critics, while [crapping on](https://twitter.com/cassiecodes/status/1390678296346697730) other approaches [on its home page](https://tailwindcss.com/#:~:text=%E2%80%9CBest%20practices%E2%80%9D%20don%E2%80%99t%20actually%C2%A0work.). [Like a boss](https://twitter.com/aardrian/status/886739140171239425).

A lot of people like the tooling, and a lot do not. I have no interest in that fight. If you are offended someone does not like your tooling, then you need to maybe choose to define your self-worth by something else. Maybe a sports franchise instead (like we do in Buffalo).
