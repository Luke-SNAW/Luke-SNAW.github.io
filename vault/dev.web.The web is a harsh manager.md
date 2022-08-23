---
id: nr06lu1kv2b3mr7yaf1178q
title: The web is a harsh manager
desc: ""
updated: 1661241105359
created: 1661241069395
---

> https://daverupert.com/2022/08/web-is-a-harsh-manager/  
> https://news.ycombinator.com/item?id=32518211

Addressing the increasing demands of the front-end

August 17, 2022

The responsibilities of the front-end web are ever increasing.

- The person responsible for knowing the 3,000 programmable property-value pairs to make the site look like the design comp… is the same person in charge of understanding the language and ecosystem required to query the data layer.
- The person who must understand a thousand page compendium of making your website accessible for every person to avoid legal peril… is also the person who copy-pastes a script tag so invasive marketing can track users across the entire web.
- The person who configures the metadata for social media cards and Google search results… is the same person who oversees the quality and security of thousands of third-party packages.
- The person who animates elements on the page as you scroll… is also the person in charge of creating images with math-based vectors using data sources resulting in impactful charts and graphs of infinite combinations.
- The person who writes asynchronous workers to control the way a browser paints a box with a code-based canvas drawing application… is the same person responsible for wiring up interactive form controls and client-side error messages.
- The person who creates a high-level system of serialized design tokens and components defined to meet specific user stories consumed by all internal and external web properties… is the same person responsible for controlling client side cache mechanisms.

All these jobs are the same person! In some ways the front-end web is like a bad manager; the scope keeps growing over time. I don’t have anything other than anecdotal evidence, but I’d wager this is a problem that leads to burnout due to context switching among front-end people. Learning new skills is admirable, but the unending list of topics to learn and the vast swings of urgent demands puts you in a state of constant stress and reinvention. “Full-stack”, [as](https://dev.to/entrptaher/fullstack-developer-is-a-scam-term-3bl2) [many](https://medium.com/swlh/the-full-stack-developer-is-a-myth-4e3fb9c25867) [have](https://www.andyshora.com/full-stack-developers.html) [noted](https://bradfrost.com/blog/post/full-stack-developers/) [before](https://www.atlanticbt.com/insights/myth-full-stack-unicorn-developer/) [me](https://medium.com/@alexkatrompas/the-hard-truth-about-the-full-stack-developer-myths-and-lies-945ffadeeb8c), exacerbates this situation.

Years ago, Chris Coyier summed this struggle up in his post [The Great Divide](https://css-tricks.com/the-great-divide/). That post was informed by a series we did on ShopTalk called “[How to think like a Front-End Developer](https://shoptalkshow.com/series/how-to-think-like-a-front-end-developer/)”. In that series, [Brad Frost](https://shoptalkshow.com/334/) divined two sides of the divide as “front of the front” and “back of the front” and it still resonates with me today. We could probably split the front-end a few ways and still have plenty of jobs to do. Some are proposing bridge roles…

Natalya Shelburne expresses this idea as a bridge role she calls [Design Engineering](https://shoptalkshow.com/434/). This is someone who acts as a bridge between design and engineering. Together with Adekunle Oduye, Kim Williams, and Eddie Lou she wrote the [Design Engineering Handbook](https://www.designbetter.co/design-engineering-handbook/introducing-design-engineering) which outlines all the roles and responsibilities of a Design Engineer saying it “involves setting up individual workflows and organizational structures that facilitate collaboration and communication across the intersection of design and engineering, as well as across product, marketing, and stakeholders.” If you’re paying money for good design, this makes sense; protect your investment to make sure the designs get engineered well.

Alex Sexton proposed a [Front-end Ops](https://www.smashingmagazine.com/2013/06/front-end-ops/) role as a “bridge between an application’s intent and an application’s reality”, managing builds and deployments, performance and error monitoring, and updating dependencies. Even at a modest scale this feels like enough work for a full time job. These are all critical operations that go sideways if not prioritized.

And there are other bridge roles we haven’t discovered yet. I personally see the need for new specializations as well. I’d argue for a “CSS Engineer” title, someone who knows the ins-and-outs of good CSS architecture that can save your app thousands of lines of code. But that title probably wouldn’t pay enough, so it’d need to be more official sounding like “Render Optimization Engineer Level 6” or something. Now that’ll get the Amazon bucks.

I don’t have answers, only questions as I find myself traversing the spectrum of different jobs a “front-end” person can do this week. It’s hard to be an expert at the front-end. And I’m not sure I like the conclusion of “You need 12 people just to make a website (or else you get yelled at on Twitter)” either. That’s a lot of money, frankly, and would lead to less websites. What’s one change we could make to eliminate 80% of the work?
