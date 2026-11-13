
> https://quii.dev/HTMX_is_the_Future

## The costs of SPA

SPAs have allowed engineers to create some great web applications, but they come with a cost:

- Hugely increased complexity both in terms of architecture and developer experience. You have to spend considerable time learning about frameworks.

  - Tooling is an ever-shifting landscape in terms of building and packaging code.
  - Managing state on both the client and server
  - Frameworks, on top of libraries, on top of other libraries, on top of polyfills. [React even recommend using a framework on top of their tech](https://react.dev/):
    > React is a library. It lets you put components together, but it doesn’t prescribe how to do routing and data fetching. To build an entire app with React, we recommend a full-stack React framework.

- By their nature, a fat client requires the client to execute a lot of JavaScript. If you have modern hardware, this is fine, but these applications will be unusable & slow for those on older hardware or in locations with slow and unreliable internet connections.
  - It is very easy to make an SPA incorrectly, where you need to use the right approach with hooks to avoid ending up with abysmal client-side performance.
- Some SPA implementations of SPA throw away progressive enhancement (a notable and noble exception is [Remix](https://remix.run/)). Therefore, you _must_ have JavaScript turned on for most SPAs.
- If you wish to use something other than JavaScript or TypeScript, you must traverse the treacherous road of transpilation.
- It has created backend and frontend silos in many companies, carrying high coordination costs.

Before SPAs, you'd choose your preferred language and deliver HTML to a user's browser in response to HTTP requests. This is _fine_, but it offers little interactivity and, in some cases, could make an annoying-to-use UI, especially regarding having the page fully reload on every interaction. To get around this, you'd typically sprinkle varying amounts of JS to grease the UX wheels.

Whilst this approach can feel old-fashioned to some, this approach is what inspired the [original paper of **REST**](http://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm), especially concerning **hypermedia**. The hypermedia approach of building websites led to the world-wide-web being an incredible success.

### Hypermedia?

The following is a response from a data API, not hypermedia.

```json
{
  "sort": "12-34-56",
  "number": "87654321",
  "balance": "123.45"
}
```

To make this data useful in an SPA, the client code must understand the structure and decide what to render and what controls to make available.

REST describes the use of hypermedia. Hypermedia is where your responses are not just raw data but are instead a payload describing the media (think HTML tags like `<p>`, headers, etc.) _and_ how to manipulate it (like `form`, `input`).

A server returning HTML describing a bank account, with some form of controls to work with the resource, is an example of hypermedia. The server is now responsible for deciding how to render the data (with the slight caveat of CSS) and _what_ controls should be displayed.

```html
<dl>
  <dt>Sort</dt>
  <dd>12-34-56</dd>
  <dt>Number</dt>
  <dd>87654321</dd>
  <dt>Balance</dt>
  <dd>£123.45</dd>
</dl>
<form method="POST" action="/transfer-funds">
  <label>Amount <input type="text" /></label>
  <!-- etc -->
  <input type="submit" value="Do transfer" />
</form>
```

The approach means you have one universal client, the web browser; it understands how to display the hypermedia responses and lets the user work with the "controls" to do whatever they need.

[Carson Gross on The Go Time podcast](https://changelog.com/gotime/266)

> ...when browsers first came out, this idea of one universal network client that could talk to any application over this crazy hypermedia technology was really, really novel. And it still is.
>
> If you told someone in 1980, “You know what - you’re gonna be using the same piece of software to access your news, your bank, your calendar, this stuff called email, and all this stuff”, they would have looked at you cross-eyed, they wouldn't know what you were talking about, unless they happened to be in one of the small research groups that was looking into this sort of stuff.

Before the World Wide Web, before web browsers, the prevailing patterns of apps were bespoke, and often "thick", clients.

Whilst ostensibly, people building SPAs talk about using "RESTful" APIs to provide data exchange to their client-side code, the approach is not RESTful in the purist sense because it does not use hypermedia.

Instead of one universal client, _scores of developers create bespoke clients_, which have to understand the raw data they fetch from web servers and then render controls according to the data. With this approach, the browser is more of a JavaScript, HTML and CSS runtime.

By definition, a fatter client will carry more effort and cost than a thin one. However, the "original" hypermedia approach arguably is not good enough for all of today's needs; the controls that the browser can work with and the way it requires a full page refresh to use them mean the user experience isn't good enough for many types of web-app we need to make.

### HTMX and hypermedia

Unlike SPAs, HTMX **doesn't throw away the architectural approach of REST**; it _augments the browser_, **improving its hypermedia capabilities** and making it simpler to deliver a rich client experience without having to write much JavaScript if any at all.

You can use **whatever programming language you like** to deliver HTML, just like we used to. This means you can use battle-tested, mature tooling, using a "true RESTful" approach, resulting in a far more straightforward development approach with less accidental complexity.

HTMX allows you to design pages that fetch **fragments of HTML** from your server to update the user's page as needed without the annoying full-page load refresh.

## Clojure HTMX TODO

...

## Embracing the web

There's more to HTMX, but this is the crux of the approach, which is the same as the approach that most websites were made before SPAs became popular.

- The user goes to a `URL`
- The server returns hypermedia (HTML), which is content with controls.
- Browser renders hypermedia
- Users can use the controls to do work, which results in an HTTP request sent from the browser to the server.
- The server does business logic, and then returns new hypermedia for the user to work with

All HTMX does, is make the browser **better** at hypermedia by giving us more options regarding **what can trigger an HTTP request** and **allowing us to update a part of the page rather than a full page reload**.

By embracing the hypermedia and not viewing the browser as merely a JavaScript runtime, we get a lot of simplicity benefits:

- We can use any programming language on the server side.
- We don't need lots of libraries and other cruft to maintain what were basic benefits of web development.
  - Caching
  - SEO-friendliness
  - The back button working as you'd expect
  - etc.
- It is very easy to support users who do not wish to, or cannot use JavaScript

This final point is crucial to me and to my current employer. I work for a company that works on products used worldwide, and our content and tools must be as usable by as many people as possible. It is unacceptable for us to exclude people through poor technical choices.

This is why we adopt the approach of [**progressive enhancement**](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement).

> **Progressive enhancement** is a design philosophy that provides a baseline of essential content and functionality to as many users as possible, while delivering the best possible experience only to users of the most modern browsers that can run all the required code.

### How it supports non-JavaScript

...

## Why is it _The Future_ ?

Obviously, I cannot predict the future, but I do believe HTMX (or something like it) will become an increasingly popular approach for making web applications in the following years.

Recently, [HTMX was announced as one of 20 projects in the GitHub Accelerator](https://github.blog/2023-04-12-github-accelerator-our-first-cohort-and-whats-next/)

### It makes "the frontend" more accessible.

Learning React is an industry in itself. It moves quickly and changes, and there are tons to learn. I sympathise with developers who _used_ to make fully-fledged applications being put off by modern frontend development and instead were happy to be pigeonholed into being a "backend" dev.

I've made reasonably complex systems in React, and whilst some of it was pretty fun, **the amount you have to learn to be effective is unreasonable for most applications**. React has its place, but it's overkill for many web applications.

The hypermedia approach with HTMX is not hard to grasp, especially if you have some REST fundamentals (which many "backend" devs should have). It opens up making rich websites to a broader group of people who don't want to learn how to use a framework and then keep up with its constantly shifting landscape.

### Less churn

Even after over 10 years of React being around, it still doesn't feel settled and mature. A few years ago, hooks were the new-fangled thing that everyone had to learn and re-write all their components with. In the last six months, my Twitter feed has been awash with debates and tutorials about this new-fangled "RSC" - react server components. Joy emoji.

Working with HTMX has allowed me to leverage things I learned 15-20 years ago **that still work**, [like my website](https://quii.dev/How_my_website_works). The approach is also well-understood and documented, and the best practices are independent of programming languages and frameworks.

I have made the example app in Go _and_ Clojure with no trouble at all, and I am a complete Clojure novice. Once you've figured out the basic syntax of a language and learned how to respond to HTTP requests with hypermedia, you have enough to get going; and you can re-use the architectural and design best practices without having to learn a new approach over and over again.

How much of your skills would be transferable from React if you had to work with Angular? Is it easy to switch from one react framework to another? How did you feel when class components became "bad", and everyone wanted you to use hooks instead?

### Cheaper

It's just less effort!

[Hotwire](https://hotwired.dev/) is a library with similar goals to HTMX, driven by the Ruby on Rails world. DHH tweeted the following.

> [Hotwiring Rails expresses the desire to gift a lone full-stack developer all the tools they need to build the next Basecamp, GitHub, or Shopify. Not what a team of dozens or hundreds can do if they have millions in VC to buy specialists. Renaissance tech for renaissance people.](https://twitter.com/dhh/status/1341758748717510659)
>
> That's why it's so depressing to hear the term "full stack" be used as a derogative. Or an impossible mission. That we HAVE to be a scattered band of frontend vs backend vs services vs whatever group of specialists to do cool shit. Absolutely fucking not.

Without the cognitive overload of understanding a vast framework from the SPA world and the inherent complexities of making a fat client, you can realistically create rich web applications with far fewer engineers.

### More resilient

As described earlier, using the hypermedia approach, making a web application that works without JavaScript is relatively simple.

It's also important to remember that the browser is an **untrusted environment**, so when you build a SPA, you have to work extremely defensively. You have to implement lots of business logic client side; but because of the architecture, this same logic needs to be replicated on the server too.

For instance, let's say we wanted a rule saying you cannot edit a to-do if it is marked as done. In an SPA world, I'd get raw JSON, and I'd have to have business logic to determine whether to render the edit button on the client code somewhere. However, if we wanted to ensure a user couldn't circumvent this, I'd have to have this same protection on the server. This sounds low-stakes and simple, but this complexity adds up, and the chance of misalignment increases.

With a hypermedia approach, the browser is "dumb" and doesn't need to worry about this. As a developer, I can capture this rule in one place, the server.

### Reduced coordination complexity

**The complexity of SPAs has created a shift into backend and frontend silos**, which carries a cost.

The typical backend/frontend team divide causes a lot of inefficiencies in terms of teamwork, with hand-offs and miscommunication, and **makes getting stuff done harder**. Many people mistake individual efficiencies as the most critical metric and use that as justification for these silos. They see lots of PRs being merged, and lots of heat being generated, but ignoring the coordination costs.

For example, let's assume you want to add a new piece of data to a page or add a new button. For many teams, that'll involve meetings between teams to discuss and agree on the new API, creating fakes for the frontend team to use and finally coordinating releases.

In the hypermedia approach, you **don't have this complexity at all**. If you wish to add a button to the page, you can add it, and you don't need to coordinate efforts. You don't have to worry so much about API design. You are free to change the markup and content as you please.

Teams exchanging data via JSON can be **extremely brittle** without care and always carries a coordination cost. Tools like consumer-driven contracts can help, but this is just _another_ tool, _another_ thing to understand and _another_ thing that goes wrong. The overheads, support and complexity of API versioning are **inherently not an issue** with a hypermedia approach, you are free to change the markup as you please.

This is not to say there is no room for specialisation. I've worked on teams where the engineers built the web application "end to end", but we had people who were experts on semantic, accessible markup who helped us make sure the work we did was of good quality. It is incredibly freeing not to have to negotiate APIs and hand off work to one another to build a website.

### More options

Rendering HTML on the server is a very well-trodden road. Many battle-tested and mature tools and libraries are available to generate HTML from the server in every mainstream programming language and most of the more niche ones.

## Further reading and listening

- The author of HTMX has written an excellent, [free book, explaining hypermedia](https://hypermedia.systems/). It's an easy read and will challenge your beliefs on how to build web applications. If you've only ever created SPAs, this is an essential read.
- [HTMX](https://htmx.org/). The examples section, in particular, is very good in showing you what's possible. The essays are also great.
- I was lucky enough to be invited onto [The GoTime podcast with the creator of HTMX, Carson Gross to discuss it](https://changelog.com/gotime/266)! Even though it's a Go podcast, the majority of the conversation was about the hypermedia approach.
- [The Go version](https://github.com/quii/todo) was my first adventure with HTMX, creating the same todo list app described in this post
- I worked on [The Clojure version](https://github.com/ndchorley/todo) with my colleague, Nicky
- [DHH on Hotwire](https://world.hey.com/dhh/the-time-is-right-for-hotwire-ecdb9b33)
- [Progressive enhancement](https://developer.mozilla.org/en-US/docs/Glossary/Progressive_Enhancement)
- Five years ago, I wrote [The Web I Want](https://quii.dev/The_Web_I_Want), where I bemoaned the spiralling costs of SPAs. It was originally prompted by watching my partner's 2-year-old ChromeBook grind to a halt on a popular website that really could've been static HTML. In the article, I discussed how I wished more of the web stuck to the basic hypermedia approach, rendering HTML on the server and using progressive enhancement to improve the experience. Reading back on this has made me very relieved the likes of HTMX have arrived.

---

## [obpe](https://news.ycombinator.com/item?id=35830823)

It's kinda funny to me that many of the "pros" of this approach are the exact reasons so many abandoned MPAs in the first place.
For instance, a major selling point of Node was running JS on both the client and server so you can write the code once. It's a pretty shitty client experience if you have to do a network request for each and every validation of user input.

Also, there was a push to move the shitty code from the server to the client to free up server resources and prevent your servers from ruining the experience for everyone.

We moved away for MPAs because they were bloated, slow and difficult to work with. SPAs have definitely become what they sought to replace.

But that isn't because of the technology, it's because all the devs writing shitty MPAs are now writing shitty SPAs. If this becomes popular, they will start writing shitty MPAs again. Nothing about this technology will stop that.

### [berkes](https://news.ycombinator.com/item?id=35834893)

Even worse: Client-side validation and server-side validation (and database integrity validation) are all their own domains! I call all of these "domain logic" or domain validation just to be sure.
Yes, they overlap. Sure, you'll need some repetition and maybe, indeed, some DSL or tooling to share some of the overlapping ones across the boundaries.

But no! They are not the same. A "this email is already in use" is serverside, (it depends on the case). A "this doesn't look like an email-address, did you mean gmail.com instead of gamil.com" is client side and a "unique-key-constraint: contactemail already used" is even more down.

My point is, that the more you sit down (with customers! domain experts!) and talk or think all this through, the less it's a technical problem that has to be solved with DSLs, SPAs, MPAs or "same language for backend and UI". And the more you (I) realize it really often hardly matters.

You quite probably don't even need that email-uniqueness validation at all. In any layer. If you just care to speak to the business.

## [brushfoot](https://news.ycombinator.com/item?id=35831051)

I use tech like HTMX because, as a team of one, I have no other choice.
I tried using Angular in 2019, and it nearly sank me. The dependency graph was so convoluted that updates were basically impossible. Having a separate API meant that I had to write everything twice. My productivity plummeted.

After that experience, I realized that what works for a front-end team may not work for me, and I went back to MPAs with JavaScript sprinkled in.

This year, I've looked at Node again now that frameworks like Next offer a middle ground with server-side rendering, but I'm still put off by the dependency graphs and tooling, which seems to be in a constant state of flux. It seems to offer great benefits for front-end teams that have the time to deal with it, but that's not me.

All this to say pick the right tool for the job. For me, and for teams going fuller stack as shops tighten their belts, that's tech like HTMX, sprinkled JavaScript, and sometimes lightweight frameworks like Alpine.
