
https://ishadeed.com/article/flexbox-separator/

```html
<section class="section">
  <div class="section__item section__item--start">
    <!-- Content -->
  </div>

  <div class="section__item section__item--end">
    <!-- Content -->
  </div>
</section>
```

I want to center the two items vertically, so I will use align-items on the parent.

```css
.section {
  display: flex;
  align-items: center;
  gap: 1rem;
  /* other styles */
}

.section__item {
  flex: 1;
}
```

# Adding The Separator

# Why The Separator Looks Like A Square?

Since we added align-items: center to center the child items vertically, we removed the default behavior of flexbox stretching child items (stretching vertically, in this case).

To fix that, we need to reset the alignment of the pseudo-element to stretch.

```css
.section:before {
  content: "";
  border: 0.5px solid #d3d3d3;
  align-self: stretch;
}
```

Next, I need to reorder the flex items to make the divider appears between them.

```css
.section__item--start {
  order: -1;
}
```

# Another Way Of Doing It

```css
/* On small sizes */
.section:before {
  content: "";
  height: 2px;
  background-color: lightgrey;
}

@media (min-width: 700px) {
  .section:before {
    width: 2px;
    height: 150px;
  }
}
```
