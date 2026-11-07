
> https://hackernoon.com/a-quick-guide-on-how-to-create-accessible-buttons-in-html

Accessibility was always important, but lately, it has gained even more traction, and if you don’t know how to create accessible websites, you can’t really call yourself a [good front-end developer](https://hackernoon.com/how-to-create-effective-frontend-design-documents?ref=hackernoon.com).

That’s a bold statement, I know, but it’s true. Just deal with it.

Today we’ll look at one of the most basic elements of any website: a button. How do I make it accessible? Without further ado, let’s just jump into it.

First and foremost, use a `button` tag. You might ask, why not a `div` for example?

Here you have a few reasons `button` tag is the better choice:

1. **It’s semantically correct.** Semantic HTML is really important. It helps with code readability and also helps web crawlers better understand our website.
2. **It’s focusable and clickable by default.** You don’t need to implement those behaviors (but if you use some CSS frameworks that reset styles for every element - remember to implement `hover` and `focus` states)
3. **It’s recognizable by screen readers.** When you use any of the screen readers, it will announce the `button` tag as, well, a button.

Is that it? That would be great, wouldn’t it be? But no, the next thing we need to talk about is button content. Here we can go three ways:

1. Text
2. Icon + text
3. Only Icon

### Text Buttons

In this case, the best thing we can do is to just use the text that is self-explanatory. We don’t need to put any additional attributes to make this kind of button accessible. There can be occasions where you’d be tempted to use `aria-label` to “overwrite” the text on the button. I strongly recommend you not to do it - it is against one of the WCAG principles.

**NOTE**: You can check all the code that I use in this article here: [Codepen](https://codepen.io/hwlkdev/pen/zYLbJJK?ref=hackernoon.com)

```html
<html lang="en">
  <body>
    <button>This is a test button</button>

    <!-- incorrect -->
    <button aria-label="This is a different button">
      This is another button
    </button>
  </body>
</html>
```

### Icon with Text Buttons

The second case - icon with text is also quite simple. We can actually use the same technique as for the simple text, but with one additional thing - we’ll need to add `aria-hidden=true` attribute for the `svg` icon. This way, screen readers will ignore the icon and read only the text.

One thing also worth doing is to add `focusable=false` attribute as some of the old browsers focus on `svg` for some reason.

```html
<button>
  <svg
    class="svg-icon"
    viewBox="0 0 20 20"
    aria-hidden="true"
    focusable="false"
  >
    <title>The icon</title>
    <path
      d="M9.719,17.073l-6.562-6.51c-0.27-0.268-0.504-0.567-0.696-0.888C1.385,7.89,1.67,5.613,3.155,4.14c0.864-0.856,2.012-1.329,3.233-1.329c1.924,0,3.115,1.12,3.612,1.752c0.499-0.634,1.689-1.752,3.612-1.752c1.221,0,2.369,0.472,3.233,1.329c1.484,1.473,1.771,3.75,0.693,5.537c-0.19,0.32-0.425,0.618-0.695,0.887l-6.562,6.51C10.125,17.229,9.875,17.229,9.719,17.073 M6.388,3.61C5.379,3.61,4.431,4,3.717,4.707C2.495,5.92,2.259,7.794,3.145,9.265c0.158,0.265,0.351,0.51,0.574,0.731L10,16.228l6.281-6.232c0.224-0.221,0.416-0.466,0.573-0.729c0.887-1.472,0.651-3.346-0.571-4.56C15.57,4,14.621,3.61,13.612,3.61c-1.43,0-2.639,0.786-3.268,1.863c-0.154,0.264-0.536,0.264-0.69,0C9.029,4.397,7.82,3.61,6.388,3.61"
    ></path>
  </svg>
  Button with icon
</button>
```

### Icon Buttons

The third case - icon only button is also pretty straightforward. We can just use `aria-label` on the `button` tag, and the screen readers will ignore everything that’s inside the button (so, in this case, an icon). We don’t even need to add `aria-hidden=true` on the icon.

```html
<button aria-label="Like">
  <svg class="svg-icon" viewBox="0 0 20 20" focusable="false" width="40px">
    <title>The icon</title>
    <path
      d="M9.719,17.073l-6.562-6.51c-0.27-0.268-0.504-0.567-0.696-0.888C1.385,7.89,1.67,5.613,3.155,4.14c0.864-0.856,2.012-1.329,3.233-1.329c1.924,0,3.115,1.12,3.612,1.752c0.499-0.634,1.689-1.752,3.612-1.752c1.221,0,2.369,0.472,3.233,1.329c1.484,1.473,1.771,3.75,0.693,5.537c-0.19,0.32-0.425,0.618-0.695,0.887l-6.562,6.51C10.125,17.229,9.875,17.229,9.719,17.073 M6.388,3.61C5.379,3.61,4.431,4,3.717,4.707C2.495,5.92,2.259,7.794,3.145,9.265c0.158,0.265,0.351,0.51,0.574,0.731L10,16.228l6.281-6.232c0.224-0.221,0.416-0.466,0.573-0.729c0.887-1.472,0.651-3.346-0.571-4.56C15.57,4,14.621,3.61,13.612,3.61c-1.43,0-2.639,0.786-3.268,1.863c-0.154,0.264-0.536,0.264-0.69,0C9.029,4.397,7.82,3.61,6.388,3.61"
    ></path>
  </svg>
</button>
```

This is definitely the simplest and most supported solution. But what are the alternatives?

The first one would be creating a `sr-only` or `visuallyhidden` class in your CSS and then using it to create an “invisible” label.

TailwindCSS defines `sr-only` class as follows:

```css
.sr-only {
  **position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border-width: 0;
}
```

When you have this class in place, you can then use it like this:

```html
<button>
  <svg
    class="svg-icon"
    viewBox="0 0 20 20"
    aria-hidden="true"
    focusable="false"
    width="40px"
  >
    <title>The icon</title>
    <path
      d="M9.719,17.073l-6.562-6.51c-0.27-0.268-0.504-0.567-0.696-0.888C1.385,7.89,1.67,5.613,3.155,4.14c0.864-0.856,2.012-1.329,3.233-1.329c1.924,0,3.115,1.12,3.612,1.752c0.499-0.634,1.689-1.752,3.612-1.752c1.221,0,2.369,0.472,3.233,1.329c1.484,1.473,1.771,3.75,0.693,5.537c-0.19,0.32-0.425,0.618-0.695,0.887l-6.562,6.51C10.125,17.229,9.875,17.229,9.719,17.073 M6.388,3.61C5.379,3.61,4.431,4,3.717,4.707C2.495,5.92,2.259,7.794,3.145,9.265c0.158,0.265,0.351,0.51,0.574,0.731L10,16.228l6.281-6.232c0.224-0.221,0.416-0.466,0.573-0.729c0.887-1.472,0.651-3.346-0.571-4.56C15.57,4,14.621,3.61,13.612,3.61c-1.43,0-2.639,0.786-3.268,1.863c-0.154,0.264-0.536,0.264-0.69,0C9.029,4.397,7.82,3.61,6.388,3.61"
    ></path>
  </svg>
  <span class="sr-only">Like</span>
</button>
```

And as you can see and hear, it works as expected (I strongly recommend you to try focusing on the buttons with VoiceOver turned on - it really helps in understanding the things that we are doing here).

Another solution is a little bit more complicated. We need to use `aria-labelledby` on the button and then provide a `hidden` label inside. Be aware that even though the label will be hidden, `labelledby` attribute will still be able to access it.

It would look like this:

```html
<button aria-labelledby="likeBtn">
  <svg
    class="svg-icon"
    viewBox="0 0 20 20"
    aria-hidden="true"
    focusable="false"
    width="40px"
  >
    <title>The icon</title>
    <path
      d="M9.719,17.073l-6.562-6.51c-0.27-0.268-0.504-0.567-0.696-0.888C1.385,7.89,1.67,5.613,3.155,4.14c0.864-0.856,2.012-1.329,3.233-1.329c1.924,0,3.115,1.12,3.612,1.752c0.499-0.634,1.689-1.752,3.612-1.752c1.221,0,2.369,0.472,3.233,1.329c1.484,1.473,1.771,3.75,0.693,5.537c-0.19,0.32-0.425,0.618-0.695,0.887l-6.562,6.51C10.125,17.229,9.875,17.229,9.719,17.073 M6.388,3.61C5.379,3.61,4.431,4,3.717,4.707C2.495,5.92,2.259,7.794,3.145,9.265c0.158,0.265,0.351,0.51,0.574,0.731L10,16.228l6.281-6.232c0.224-0.221,0.416-0.466,0.573-0.729c0.887-1.472,0.651-3.346-0.571-4.56C15.57,4,14.621,3.61,13.612,3.61c-1.43,0-2.639,0.786-3.268,1.863c-0.154,0.264-0.536,0.264-0.69,0C9.029,4.397,7.82,3.61,6.388,3.61"
    ></path>
  </svg>
  <span id="likeBtn" hidden> Like </span>
</button>
```

Setting the `id` on the `span` is important because that’s how we can access the label from the `labelledby` attribute.

All three solutions work the same. That’s why my favorite is just setting the `aria-label`, it is the simplest solution.

These were the most important accessibility adjustments you can make to ensure your buttons work well with screen readers. But what about people with visual impairments that do not use screen readers? Here we have two additional things to take care of, and we’ll be all set.

### Sizing

First, let’s talk about sizing. In the WCAG guidelines, there is a criterion 2.5.5 - Target Size. It’s described as follows:

> The size of the target for pointer inputs is at least 44 by 44 CSS pixels.

There are a few exceptions, and you can see those on the screen now. They are not relevant in this specific case.

[A11Y](https://hackernoon.imgix.net/images/HWFAWxGBOGhZROldCWk4gX3WWFs1-2023-07-05T12:20:23.445Z-z9lgcu119tkw464bimu1njz9?w=1200&q=75&auto=format)

So let’s ensure that our buttons are, in fact, big enough. I’m not a fan of using pixels; I’d much rather go with `rems` or `ems`. This will also help if the user changes his base font size - the button will still be sized properly.

```css
button {
  min-height: 3rem;
  min-width: 3rem;
}
```

I used `3rem` as usually the root font size is `16px`, so `3rem` gives us `48px`. But if the user zooms in to, let’s say, `24px`, the button will be larger.

Ok, with that out of the way - let’s handle the last thing I want to talk about today - contrast.

### Contrast

WCAG guidelines say:

> The visual presentation of text and images of text has a contrast ratio of at least 4.5:1 - for AA success criterion, and 7:1 for AAA criterion.

The best tool to use here is the contrast checker by WebAIM [https://webaim.org/resources/contrastchecker/](https://webaim.org/resources/contrastchecker/?ref=hackernoon.com)

You can just put your button color there, and you’ll get the text color and vice versa. A simple yet great tool. In the case of my examples, let’s say I wanted a green button.

[Contrast Checker](https://hackernoon.imgix.net/images/HWFAWxGBOGhZROldCWk4gX3WWFs1-2023-07-05T12:20:23.473Z-kirouycgk4vim0mbr1mn4reu?w=1200&q=75&auto=format)

As you can see, white text fails all of the criteria, but black should be OK. As you can see, while I’m scrolling through the colors, the contrast ratio changes, and also different criteria are passing.

With straight black, we get a contrast of over 10 to 1. So that’s going to work!

And that’s it! Those are the things that you can do to make your buttons accessible. I hope you like it. If you did, consider following me on Twitter, [Dev.to](http://dev.to/?ref=hackernoon.com), and LinkedIn. More front-end and accessibility-related content are on the way.
