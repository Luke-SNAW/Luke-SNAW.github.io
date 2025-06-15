
> https://medium.com/codex/i-bet-you-didnt-know-about-these-15-html-features-9b0824dba28f

## **Content Editable**

`contenteditable` is an attribute that can be set on an element to make the content editable. It works with elements like DIV, P, UL, etc. You have to specify it like, `<element contenteditable=”true|false”>`.

```html
<h2>Earth 616 superheroes</h2>
<ul class="content-editable" contenteditable="true">
  <li>1. Iron Man</li>
  <li>2. Captain America</li>
  <li>3. Black Panther</li>
</ul>
```

## **Datalist**

The `<datalist>` tag specifies a list of pre-defined options and provides an autocomplete feature.

```html
<label for="”superhero”"
  >In case of emergency, which superhero would you call?:</label
>
<input list="”superheroes”" name="”superhero”" id="”superhero”" />
<datalist id="”superheroes”">
  <option value="”Iron" Man”></option>
  <option value="”Captain" America”></option>
  <option value="”Black" Panther”></option>
  <option value="”Thor”"></option>
  <option value="”Spider" Man”></option>
</datalist>
```

## **Range**

The `range` input type behaves like a slider range selector.

```html
<head>
  <script>
    function changeValue(event) {
      let value = event.target.value;
      let output = document.getElementById("output");
      output.value = value;
    }
  </script>
</head>
<body>
  <form method="post">
    <input
      type="range"
      name="range"
      min="0"
      max="100"
      step="1"
      value=""
      onchange="changeValue(event)"
    />
  </form>
  <div class="range">
    <output id="output" name="result"> </output>
  </div>
</body>
```

## **Meter**

The `<meter>` tag defines a scalar measurement within a defined range or a fractional value.

```html
<label for="home">Cloud storage</label> <meter id="home" value="0.4">40%</meter
><br /><label for="root">Internal storage</label>
<meter id="root" value="0.6">60%</meter><br />
```

## **Color picker**

A simple color picker.

```html
<p id="colorPicker">Color Picker!</p>
<input type="color" onchange="showColor(event)" />
```

## **Mark content**

Use the `<mark>` tag to highlight any text content.

```html
<p>Did you know that <mark>not all heroes wear capes.</mark></p>
```

## **Blockquote & Cite**

If you’re including content from a different source, you should absolutely cite that source.

```html
<figure>
  <blockquote>
    <p>It's an imperfect world, but its the only one we've got.</p>
  </blockquote>
  <figcaption>--TONY STARK, <cite>IRON MAN</cite></figcaption>
</figure>
```

## **Abbreviation**

“abbr” is short for abbreviation! The idea here is that if you use a title (e.g. “Mr.”) or acronym (e.g. “SHIELD”), the abbr tag indicates exactly what that abbreviation means.

```html
<p>
  Agent Phil Coulson leads a team of highly skilled agents from the global
  law-enforcement organisation known as
  <abbr
    title="Strategic Homeland Intervention, Enforcement, and Logistics Division"
    >SHIELD</abbr
  >.
</p>
```

## **<del> and <ins>**

There is actually a tag for a text that is struck-through and another that indicates the replacement text.

```html
<p>
  <del>Iron Man</del> <ins>Captain America</ins> is ehmmm.. yea the captain!
</p>
```

## **Output**

The `<output>` tag represents the result of a calculation. Typically this element defines an area that will be used to display text output from some calculation.

```html
<form oninput="x.value=parseInt(a.value) \* parseInt(b.value)">
  <input type="number" id="a" value="0" /> \*
  <input type="number" id="b" value="0" /> =
  <output name="x" for="a b"></output>
</form>
```

## **Hidden**

When it comes to hiding elements, we all tried different approaches such as using `opacity:0`, `visibility:hidden`, `height:0; width:0`, `display:none` in our CSS file. Each one has its own use cases and works on different layouts. Another option similar to them is the [hidden](https://developer.mozilla.org/en/docs/Web/HTML/Global_attributes/hidden) HTML attribute. If an element has `hidden` specified on it, it’ll be hidden. It happened to me to have hidden inputs for storing values, so don't be surprised if you will need it too!

```html
<div hidden>...</div>
```

## **Time**

The `<time>` tag defines a specific time (or datetime).

The `datetime` attribute of this element is used to translate the time into a machine-readable format so that browsers can offer to add date reminders through the user's calendar, and search engines can produce smarter search results.

```html
<p>
  The next assemble meeting is postponed on
  <time datetime="2022-12-01">2022-12-01</time>.
</p>
```

## **Audio**

The `<audio>` tag will define a sound and there are three supported files which the tag can be used with. These are MP3, WAV, and OGG. A browser will then select the first one it supports.

```html
<audio controls>
  <source src=”introduction.ogg” type=”audio/ogg”> <source
  src=”introduction.mp3” type=”audio/mpeg”> Your browser does not support this
  audio
</audio>
```
