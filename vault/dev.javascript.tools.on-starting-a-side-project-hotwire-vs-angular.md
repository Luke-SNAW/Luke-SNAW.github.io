---
id: q8rxb4e1rjfzkmqpe8t03c7
title: 'On Starting A Side-Project: Hotwire vs. Angular'
desc: ''
updated: 1683704885185
created: 1683704804487
---

> https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm

For the last few months, [I've been digging into the Hotwire framework](https://www.bennadel.com/blog/4396-setting-up-my-coldfusion-hotwire-demos-playground.htm "Read article: Setting Up My ColdFusion + Hotwire Demos Playground"). I was initially drawn to Hotwire on its promise of allowing me to build a SPA (Single-Page Application)-like experience using an MPA (Multi-Page Application); and, to do so with _less effort_. After several months of creating demos and migrating this ColdFusion blog over to using Hotwire, I feel like I have a much better sense of how Turbo Drive, Turbo Streams, and Stimulus work. But, I'm not quite sure that I want to use Hotwire when I start my next side-project.

**CAUTION**: This blog post is very much me _talking to myself_, trying to figure some things out.

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#im-happy-that-i-updated-my-blog-to-use-hotwire "Link directly to this section: I'm Happy That I Updated My Blog to Use Hotwire")I'm Happy That I Updated My Blog to Use Hotwire

I used this blog as a laboratory for learning about Hotwire. Prior to this, I had _no framework at all_. Sure, I had jQuery, which I eventually [replaced with Umbrella JS](https://www.bennadel.com/blog/4184-replacing-jquery-110kb-with-umbrella-js-8kb.htm "Read article: Replacing jQuery (110kb) With Umbrella JS (8kb)"); but, there was nothing really tying everything together. As such, moving to Hotwire somewhat forced me to organize my code better.

Plus, I do love the fact that Hotwire creates a _persistent process_, which reduces the amount of work each _subsequent navigation event_ has to incur. Of course, this is a "blog" where the number of pages viewed is "1" in the vast majority of cases; so, the relevance of a "subsequent navigation event" is a matter of much debate.

I'm also thankful that Hotwire encouraged me to think about **progressive enhancement** and creating an experience that would still work if the JavaScript failed to load. I do believe that this is a _critical ingredient_ for any _public facing_ site. And, it has certainly made this site more resilient.

In the end, if I were to build another public facing "content" site, **I do believe that I would choose Hotwire**. I also believe that I might choose it for any "simple" back-end administrative system.

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#hotwire-doesnt-address-some-important-problems "Link directly to this section: Hotwire Doesn't Address Some Important Problems")Hotwire Doesn't Address Some Important Problems

I understand that a lot of the uphill battle with Hotwire - with _anything new_ - is lack of experience. I've been building-up a completely new mental model, and it's not always obvious how things are supposed to be done. But, after a few months of experience, I'm beginning to see that Hotwire doesn't really address a certain set of problems. Here are some things that still seem fuzzy and unanswered in my mind:

- **Scoping of Names**: Hotwire uses the DOM (Document Object Model) as the source of truth; and, maps DOM attributes to Stimulus Controllers. As such, every controller has to be uniquely named. As an application grows and evolves, I suspect that Controller names will have to get longer and more complex in order to remain unique. And, since controller names are included in every "action", "param", and "target" target as well, the DOM is going to get wordy!
  > **ASIDE**: I've see this with other Dependency-Injection (DI) frameworks as well. In fact, in my AngularJS 1.x apps, I've started to prefix my Component tag-names with `m{x}` where `x` is a globally-unique counter. Example `<m44-team-members>` and `<m97-email-recipients>`. This way, I can avoid naming collisions without having to create artificially complex names.
- **Scoping of CSS**: Most of the Hotwire examples on the web seem to use Tailwind CSS. And, I suspect that some of the impetus behind this is a lack of any native CSS scoping. Since there's no inherent compilation step in a Hotwire application, there's no hook that allows Hotwire to inject template modifications that enable scoping.
- **Encapsulated Interfaces**: While reusing templates for rendering is a core part of the Hotwire way, this doesn't directly address the need to encapsulate complex interfaces. Ruby on Rails has some helpers for this; but, if you're not using Rails, you're on your own.
- **Layered Routing**: If your application is "flat," in that a URL route only ever maps to a single page, Hotwire "just works". But, if you want to start using "auxiliary routes" to represent page state - such as making a modal window deep-linkable from _anywhere_ in the application - there's no a great _native way_ to do this. You can use Turbo Frames with an `advance` action to change the URL; but, this doesn't really address the page-refresh issue; or, the need to simply close the modal window and revert back to the previous URL.
- **Error Handling**: Whether it be a `401 Unauthorized` error or a `500 Server Error`, handling failures in Hotwire is non-obvious. You can hook into _events_ and _override rendering_; however, since Hotwire is doing all the fetching _for you_, there's no clear place to put this kind of logic. And, since Turbo Frames and top-level requests seem to fail in _different ways_, handling errors is all the more complex.

Now, again, I have to stress that I only have a _few months_ experience with Hotwire; so, **take this all with some healthy apprehension**. Plus, the Basecamp team has built Basecamp and HEY, both of which are highly dynamic, interactive applications. So, if you really know what you're doing, it's clear that Hotwire gives you the tools to get it done.

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#is-hotwire-really-less-work "Link directly to this section: Is Hotwire Really Less Work?")Is Hotwire Really Less Work?

Part of the Hotwire messaging is that building an application is going to be less work. But, I'm not sure it actually works-out that way. I believe that, more than anything, aspects of the control-flow just live in different places. But, I don't believe that there's actually _less stuff_ to build.

Consider a "Contact" form. With a Contact form I need:

- A controller action to render the form.
- The form HTML itself.
- A controller action to receive the submission.
- The business logic to process the submission.
- A controller action to render the Thank you.
- The Thank you HTML itself.

With Hotwire, that's all done server-side. _Without Hotwire_, some of that is server-side and some of that is client-side. Furthermore, the server-side parts are likely spread out across page-controllers and API-controllers. But, there's nothing here that I would _remove_ when using Hotwire; nor is there anything that I would _add_ when using a single-page application. It's the same stuff, it's just in different places.

Of course, if you're using Hotwire because you get to use the server-side technology more often, then it's _not the volume_ of "stuff" that matters, it's the _implementation of the stuff_ that makes the difference for you.

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#hotwires-back-button-is-fundamentally-better "Link directly to this section: Hotwire's "Back Button" is Fundamentally Better")Hotwire's "Back Button" is Fundamentally Better

One thing that Hotwire _clearly gets right_ is the **Back Button**. When you hit the back button in a Hotwire application, Turbo Drive just pulls the page out of the cache and renders it instantly. This is something that **no Single-Page Application can really do quite as well** (or so it seems).

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#hotwire-leads-to-more-reusable-widgets "Link directly to this section: Hotwire Leads to More Reusable Widgets")Hotwire Leads to More Reusable Widgets

If I were to choose Angular for my next side-project, then all the widgets I built would end up working in an Angular-only context. Which means, if I had something special - like a "Fancy Select Box" - I couldn't use it on any View outside of the Angular app.

With Hotwire, on the other hand, since everything is based on server-side partial reuse, any widget can be used anywhere (as long as you're loading Hotwire). Well, I mean, sort of - it depends on whether that widget was built to work via progressive enhancement.

## [](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm#its-all-about-trade-offs "Link directly to this section: It's All About Trade-Offs")It's All About Trade-Offs

There's no clear-cut winner here. The reason I'm even writing this post is because **I'm conflicted**; and, the writing helps me think-through the problem. I think there are some things that Hotwire does really well; and, I think there are some points of friction. The question then becomes, are the benefits worth the drawbacks?

If I needed the site to work _without JavaScript_, it would be a non-issue - Hotwire all the way. Its "progressive enhancement" approach is a true winner.

But, if I'm creating a site that has decided to rely on JavaScript, are the drawbacks of Hotwire "less bad" than the drawbacks of something like Angular? Angular has added complexity, no doubt. But, it also brings a ton of value to the table. If I'm going to buy into JavaScript, then the value-add of Angular is well worth it.

Much to consider!

---

## Comments

The other _relatively large drawback_ to using Hotwire is that it [doesn't working with `.cfm` file extensions natively](https://www.bennadel.com/blog/4381-hotwire-turbo-drive-doesnt-work-with-cfm-page-extensions.htm "Read article: Hotwire Turbo Drive Doesn't Work With .cfm Page Extensions"). Which means, any site that uses Hotwire will _also have to use_ some sort of **URL-rewriting** that maps all `.htm` requests to `.cfm` requests. This isn't a huge deal; but, it does add another layer of complexity where I have to define route-definitions. If I use Angular, it doesn't matter what the URLs look like.
