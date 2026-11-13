
https://betterprogramming.pub/10-css-tricks-that-greatly-improve-user-experience-5ee52886ca4b

# Clickable area

```css
#btn::before {
  content: "";
  position: absolute;
  top: -20px;
  right: -20px;
  bottom: -20px;
  left: -20px;
}
```

# Smooth Scroll

# Select all text

just use this CSS style: `user-select: all`.  
If you want to add some extra styles after the text is selected, you can use `::selection`.

# Cursor

# Image

```css
img {
  width: 128px;
  height: 128px;
  object-fit: cover;
}
```

# No image

```html
<img
  src="https://miro.medium.com/xxx.jpg"
  alt="fireworks picture"
  onerror="this.classList.add('error');"
/>
```

```css
img.error {
  display: inline-block;
  transform: scale(1);
  content: "";
  color: transparent;
}
img.error::before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: #f5f5f5
    url("https://cdn-images-1.medium.com/max/1600/1*we8wfyztsdo12e2Cww6oVA.jpeg")
    no-repeat center / 100% 100%;
}
```

# Color Contrast

The WCAG AA specification states that all the important content needs to have a color contrast ratio of `4.5:1` or more.

Here is a tool for [Contrast Checker](https://webaim.org/resources/contrastchecker/).
