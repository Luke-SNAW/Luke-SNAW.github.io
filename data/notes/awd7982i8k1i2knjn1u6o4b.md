
https://meyerweb.com/eric/thoughts/2022/04/26/flexibly-centering-an-element-with-side-aligned-content/

https://jsfiddle.net/oduska/va4djs9o/

```html
<ol>
  <li>Foreword</li>
  <li>Chapter 1: The Day I Was Born</li>
  <li>Chapter 2: Childhood</li>
  <li>Chapter 3: Teachers I Admired</li>
  <li>Chapter 4: Teenage Dreaming</li>
  <li>Chapter 5: Look Out World</li>
  <li>Chapter 6: The World Strikes Back</li>
  <li>Chapter 7: Righting My Ship</li>
  <li>Chapter 8: In Hindsight</li>
  <li>Afterword</li>
</ol>
```

```css
ol {
  max-inline-size: max-content;
  margin-inline: auto;
}
```

You can also achieve this with:

```css
ol {
  display: table;
  margin: auto;
}
```
