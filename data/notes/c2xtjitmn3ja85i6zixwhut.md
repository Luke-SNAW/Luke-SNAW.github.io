
> https://apiumhub.com/tech-blog-barcelona/inverted-triangle-architecture-for-css-itcss/

The concept of modular CSS started to emerge years ago. All of us developers who have worked with CSS have had to deal with the difficulty of making our styles scalable and maintainable when our projects start to grow and, in addition, several people collaborate. That is why numerous methodologies have emerged to make our work easier. These methodologies are not found in any library or technology, they are more of a guide to help organise our CSS.

The best known are OOCSS (object Oriented CSS), SMACSS (Scalable and Modular Architecture for CSS), BEM (Block, Element, Modifier) and ITCSS (Inverted Triangle CSS).

The concept of CSS architecture arises with the emergence of CSS preprocessors such as SASS or LESS, which allow us to import different files, use variables and functions among other functionalities. In this article I am going to focus on the ITCSS architecture and the advantages it can offer when implemented in a project.

## What is ITCSS?

It was developed by Harry Robers with the idea of organising our CSS code in an optimal way. Its name comes from Inverted Triangle architecture for CSS because of the way in which the files are organised in layers according to the level of specificity and importance.

#### Robers himself defines ITCSS as follows:

- It is a **scalable and manageable architecture**.
- It is a philosophy, **not a library**.
- It is **preprocessor-independent** (although it is really best served by using one).
- It is a **meta framework**, a framework for frameworks. That is, it serves as a base to be used with other frameworks.

The main objective of its emergence is to help organise the CSS files of our projects and thus solve the problems caused by the cascade and the specificity of the selectors. If we look at the following graph, we can get an idea of how CSS projects that do not follow a correct methodology end up:

[Inverted Triangle architecture for CSS (ITCSS) 1](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/vSiy5k4IvdOiPRA-Xtss49Il5M9FidzLTs4DCo1xHG4xgjX7TiaouuAZfSsEy545BL0jVNRnFxK1jDRwKjDPWa0YJSY-rTXlGn-NTeU84Dk26jPeWTRkOu49BYMEhWgKdl0RxX1Q)

If we look at all the rules of our project in a single CSS file, the left of the X axis of the graph would be the beginning and the right would be the end. We see how we have rules that are at the beginning prevail over rules that are at the end, while others that are in the middle are the most important. In short: we have a code that is complicated to maintain and where the new rules we add are in direct conflict with the specificity.

The goal with ITCSS is that, by organising the CSS files in layers, we achieve a bottom-up specificity.

[Inverted Triangle architecture for CSS (ITCSS) 2](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/oNZDM44OEcrHbQTau-fiOMkHqgXATGWsw-EkdJfP_g1uCzwRepPDRcF_fMh1w3ZjrbVQk7KAyAGTcw4YyuJCq50_Z9HZ19bzQYKDifrvcWcnbJILJ5qVHybvDNiSb18tXHVpTC7I)

It is true that the rules of specificity and cascading are very clear, but when we work on real projects we find that the mix of using id, !important and nesting means that applying a new rule is a problem and our applications end up being unmaintainable.

Therefore, we find that each piece of CSS needs to be aware of which one precedes it and which one is next. In other words: dependencies are created. In the end, CSS is a giant tree of dependencies.

To solve all these problems, in summary we need::

- A healthy and accessible environment for many people.
- To be able to control and tame the order of the code and the cascade.
- Create a place for the old and the new to coexist.
- Reduce redundancy.
- End the war on specificity.

And these are the principles on which ITCSS was born. Now let’s look at an example of how this is achieved.

## Structure

The code defined in the upper layers has a greater impact than the code defined in the lower layers. Thus the upper layers affect the lower layers, but never the other way around. The lower layers will inherit the styles of their superiors.

[Manage large CSS projects with ITCSS](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/444COS9a2NkcThrLfpZ1kPQIrNmpx45qKBDTTkuoe1zMv_ARAc7nOpfmLVMHQvHYa_9qrXEU4E1imJLOO2FhoVWFFowURADr6dsj6vc717Aqm_RvVRgeCEIZG4xTW04_itnj5pD9 "Inverted Triangle architecture for CSS (ITCSS) 3")

– **Settings.** This is where variables are defined when using a preprocessor. It does not generate CSS.

```css
$main-color: #6834cb;
```

– **Tools.** If preprocessor is used, functions and mixins are defined in this layer. Like the previous one, it does not generate CSS.

```css
@function sum($numbers...) {
  $sum: 0;
  @each $number in $numbers {
    $sum: $sum + $number;
  }
  @return $sum;
}
```

– **Generic.** This refers to generic code, that which serves to reset or standardise the base styles of browsers. For example a reset css or a normalize would go here.

```css
* {
  padding: 0;
  margin: 0;
}
```

**– Elements.** Rules affecting HTML tags.

```css
h1 {
  color: $main-color;
  font-size: 24px;
}
```

– **Objects.** Objects, i.e. those generic classes that are reusable throughout the project. For example the container.

```css
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto;
}
```

– **Components.** Components, unlike objects, are specific parts of the interface. An example of a component would be a search bar or the header of our application. The styles we define for a component will only affect that component.

```css
.search-bar {
  background-color: $pearl;
  color: $light-grey;
  font-size: 22px;
}
```

**– Trumps.** This layer, also called **Utilities**, encompasses all those rules that override any other rules defined in the previous layers. It is the only layer where !important is allowed. An example would be to have a class that allows us to hide elements using a display: none.

```css
.d-none {
  display: none !important;
}
```

## Structure within a project

Let’s assume that we use SASS as a CSS preprocessor to structure our project, so it would look like this:

[Inverted Triangle architecture for CSS (ITCSS) 4](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/n2ZxeiTQDF15L2gE9jhwy6eAVroJOg_BrL5ZdhIKYEgUR6JC4zogUDErJeD5RtuA0Vx8aUtla3uje5UJAjHJaeMSMxX5r74-F4PSVaeebfUNl2IOkbafeVCPBpwt0fos-aHD-NAX)

– A folder with the imports. This is something I like to use to have better organized the files for each ITCSS layer, especially when several people work, so we can better locate our code and where to add the new files to import. However, if you prefer, you can omit this folder and add the imports directly in the main file.

[Inverted Triangle architecture for CSS (ITCSS) 5](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/uCpv7dDnDFJuA-ZbymjE2Lgmf8E_ATJllkJirbqj7M0bL1HmA4vMXJJIORr56vHdN_hz-ltguVzChC5YWUrAupPCUIirp6VXsrzGRqLIEKNFHO8pQaW3pClLdCwxdkbDxy2Qs-0D "Inverted Triangle architecture for CSS (ITCSS) 5")

– **Main file** with all the imports that will be the one that will end up compiled in a single CSS that our application will use. As we have done the imports by layers in the imports folder, this is much lighter and cleaner and we don’t have to worry about adding any more files here.

[Inverted Triangle architecture for CSS (ITCSS) 6](https://cdn-cgbdj.nitrocdn.com/RbczMDpxKIrQLdqnZdHDBvZTsISICJjh/assets/desktop/optimized/rev-924eb12/W3zG6V6q6nL0kV6MrFBgN4_S3K2R9R2dK1kh7lj6tJbkRhexMCGZl2qTUCwbJmc48rvev8Dl8_GEdyEwX4deuKltJ_UCQncJRU86OFPzfAQ0K5ZsqKSWqi3Uyl7Gt5J12soq3Xdp)

The names of files that are only to be used in imported form in another file begin with an underscore to make them easier to distinguish.

## Conclusion

And this is how the structure of a project following the ITCSS architecture would look like. It is clear that for a small project made in Vue or React, you may not see much use in its implementation, but for those projects that are large, have several people working on them and need to be scalable, ITCSS offers a fairly consistent framework. It is also very useful if we want to create our own library that will be common to several projects, thus having a unified architecture.

Finally, I would like to mention again that ITCSS is inclusive with other frameworks, and even BEMIT has emerged, which is the joint use of BEM with ITCSS and enhances the benefits of both. But this is a topic for another article.

#### Interesting Links

Talk by Harry Roberts explaining ITCSS in depth: [https://vimeo.com/114965689](https://vimeo.com/114965689)
