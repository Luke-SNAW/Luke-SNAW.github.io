---
id: fhqiguqk4tmhvgqwol1sgku
title: Checklist in pure CSS
desc: ""
updated: 1647761652838
created: 1647761603748
---

https://stackdiary.com/useful-css-tricks/

As I mentioned at the beginning of the article, CSS is maturing at a steady pace. And this demo of a dynamic checklist is a prime example of that.

The way it works is that we use the `checkbox` input type together with the `:checked` pseudo-class. And use the `transform` property to change the state whenever the `:checked` specification returns true.

You can achieve various things with this approach. E.g. Toggle hidden content when a user clicks on a specific checkbox. It works with input types such as radio and checkbox, but can also be applied to `<option>` and `<select>` elements.

```html
<div class="checklist">
  <h2>Item Checklist with CSS</h2>
  <label>
    <input type="checkbox" name="" id="" />
    <i></i>
    <span>Item #1</span>
  </label>
  <label>
    <input type="checkbox" name="" id="" />
    <i></i>
    <span>Item #2</span>
  </label>
  <label>
    <input type="checkbox" name="" id="" />
    <i></i>
    <span>Item #3</span>
  </label>
</div>
```

```css
.checklist {
  padding: 50px;
  position: relative;
  background: #043b3e;
  border-top: 50px solid #03a2f4;
}
.checklist h2 {
  color: #f3f3f3;
  font-size: 25px;
  padding: 10px 0;
  margin-left: 10px;
  display: inline-block;
  border-bottom: 4px solid #f3f3f3;
}
.checklist label {
  position: relative;
  display: block;
  margin: 40px 0;
  color: #fff;
  font-size: 24px;
  cursor: pointer;
}
.checklist input[type="checkbox"] {
  -webkit-appearance: none;
}
.checklist i {
  position: absolute;
  top: 2px;
  display: inline-block;
  width: 25px;
  height: 25px;
  border: 2px solid #fff;
}
.checklist input[type="checkbox"]:checked ~ i {
  top: 1px;
  height: 15px;
  width: 25px;
  border-top: none;
  border-right: none;
  transform: rotate(-45deg);
}
.checklist span {
  position: relative;
  left: 40px;
  transition: 0.5s;
}
.checklist span:before {
  content: "";
  position: absolute;
  top: 50%;
  left: 0;
  width: 100%;
  height: 1px;
  background: #fff;
  transform: translateY(-50%) scaleX(0);
  transform-origin: left;
  transition: transform 0.5s;
}
.checklist input[type="checkbox"]:checked ~ span:before {
  transform: translateY(-50%) scaleX(1);
  transform-origin: right;
  transition: transform 0.5s;
}
.checklist input[type="checkbox"]:checked ~ span {
  color: #154e6b;
}
```
