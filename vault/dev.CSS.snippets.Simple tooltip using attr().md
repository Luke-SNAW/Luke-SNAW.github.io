---
id: db1iy80kfrgwmlb2ggnwf8p
title: Simple tooltip using attr()
desc: ""
updated: 1647761571115
created: 1647761506377
---

https://stackdiary.com/useful-css-tricks/

The attr() property is one of my favorite recent discoveries. I wanted to add a tooltip function to my WordPress blog, but doing so would require using a plugin that adds unnecessary bloat to my site. Thankfully, that can be circumvented using attr().

The way it works is quite simple, let me explain the code below:

- We use the tooltip class to specify which element is going to be the tooltip. You can style this however you like, but for sake of the demo we use a dotted border-bottom.
- Next we create a :before pseudo-element which will contain a content attr() function and its specification. In this case, we call it tooltip-data.
- And finally we create a :hover pseudo-class which will set the opacity to 1 whenever someone hovers over the tooltip itself.

Additionally, you have to include custom styling. Depending on your tooltip data, you might need to adjust the width but also the margin. And once you do set it all up, you can reuse the tooltip-data attr() class in any part of your design.

```html
<h1>HTML/CSS tooltip</h1>
<p>
  Hover <span class="tooltip" tooltip-data="Tooltip Content">Here</span> to see
  the tooltip.
</p>
<p>
  You can also hover
  <span class="tooltip" tooltip-data="This is another Tooltip Content"
    >here</span
  >
  to see another example.
</p>
```

```css
.tooltip {
  position: relative;
  border-bottom: 1px dotted black;
}

.tooltip:before {
  content: attr(tooltip-data);
  position: absolute;
  width: 250px;
  background-color: #efba93;
  color: #fff;
  text-align: center;
  padding: 15px;
  line-height: 1.1;
  border-radius: 5px;
  z-index: 1;
  opacity: 0;
  transition: opacity 0.5s;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  font-size: 0.7em;
  visibility: hidden;
}

.tooltip:after {
  content: "";
  position: absolute;
  bottom: 75%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  opacity: 0;
  transition: opacity 0.5s;
  border-color: #000 transparent transparent transparent;
  visibility: hidden;
}

.tooltip:hover:before,
.tooltip:hover:after {
  opacity: 1;
  visibility: visible;
}
```
