---
id: h1Xiu9HcFfjIwSPhAZy3Z
title: "Switch vs if…else: A Comparison"
desc: ""
updated: 1669616858541
created: 1644825544998
---

> https://javascript.plainenglish.io/switch-vs-if-else-7f7617bfe8cb

```javascript
function recommendMovie(genre) {
  if (genre === "action" {
      console.log("Die Hard");
  } else if (genre === "comedy") {
      console.log("The Big Lebowski");
  } else if (genre === "horror") {
      console.log("Dawn of the Dead");
  } else if (genre === "drama") {
      console.log("The Shawshank Redemption");
  } else if (genre === "musical") {
      console.log("The Blues Brothers");
  } else if (genre === "sci-fi") {
      console.log("Blade Runner");
  } else {
      console.log("Genre not recognized. Choose between action, comedy, horror, drama, musical, or sci-fi.");
  }
}
```

```javascript
function recommendMovie(genre) {
  switch (genre) {
    case "action":
      console.log("Die Hard")
      break
    case "comedy":
      console.log("The Big Lebowski")
      break
    case "horror":
      console.log("Dawn of the Dead")
      break
    case "drama":
      console.log("The Shawshank Redemption")
      break
    case "musical":
      console.log("The Blues Brothers")
      break
    case "sci-fi":
      console.log("Blade Runner")
    default:
      console.log(
        "Genre not recognized. Choose between action, comedy, drama, musical, or sci-fi."
      )
  }
}
```

The switch statement is less cluttered, quicker to read, and easier to understand. It is also a little bit faster which gives it another advantage in cases with numerous conditions. The other area where switch statements shine is when multiple conditions execute the same outcome.

```javascript
function fruitOrVegetable(item) {
  if (
    item === "apple" ||
    item === "orange" ||
    item === "banana" ||
    item === "cherry"
  ) {
    console.log("Fruit")
  } else if (
    item === "broccoli" ||
    item === "lettuce" ||
    item === "carrot" ||
    item === "potato"
  ) {
    console.log("Vegetable")
  } else {
    console.log("Neither")
  }
}
```

```javascript
function fruitOrVegetable(item) {
  switch (item) {
    case "apple":
    case "orange":
    case "banana":
    case "cherry":
      console.log("Fruit")
      break
    case "broccoli":
    case "lettuce":
    case "carrot":
    case "potato":
      console.log("Vegetable")
      break
    default:
      console.log("Neither")
  }
}
```

This is a pretty big improvement. It’s much easier to read and understand.
