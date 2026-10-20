
## Collections

- [The Valley of Code](https://thevalleyofcode.com/)
- [Web Almanac - HTTP Archive’s annual state of the web report 2022](https://almanac.httparchive.org/en/2022/table-of-contents) - HTTP Archive’s annual **state of the web** report
- [Have Single-Page Apps Ruined the Web? | Transitional Apps with Rich Harris, NYTimes](https://youtu.be/860d8usGC0o)
- [Move over JavaScript: Back-end languages are coming to the front-end](https://github.com/readme/featured/server-side-languages-for-front-end): A NEW CROP OF SERVER-SIDE TOOLS IS MAKING IT POSSIBLE TO BUILD WEB UIS WITHOUT JAVASCRIPT.
- [Why Efficient Hydration in JavaScript Frameworks is so Challenging](https://dev.to/this-is-learning/why-efficient-hydration-in-javascript-frameworks-is-so-challenging-1ca3)
- [Web Quality Assurance: From User Requirements To Web Risk Management](https://www.smashingmagazine.com/2021/09/journey-into-web-quality-assurance/)
  - [The Web Quality Assurance Checklist](https://checklists.opquast.com/en/web-quality-assurance/): 240 rules to improve your sites and take better care of your users - Version 4 - 2020-2025
- [The Future Of The Web](https://www.hazem.cool/blog/the-future-of-the-web)
- [HTTP Status Dogs](https://httpstatusdogs.com/)
- [Safari isn't protecting the web, it's killing it](https://httptoolkit.tech/blog/safari-is-killing-the-web/)
- [Front-End System Design Guide. Web developer interview cheat sheet](https://javascript.plainenglish.io/front-end-system-design-guide-9a11381f5e81)
- [A Response To "Have Single-Page Apps Ruined the Web?"](https://htmx.org/essays/a-response-to-rich-harris/)
- [When Should You Use Hypermedia?](https://htmx.org/essays/when-to-use-hypermedia/)
- [HTTP/3 From A To Z: Core Concepts (Part 1)](https://www.smashingmagazine.com/2021/08/http3-core-concepts-part1/)
- [Web Incubator Community Group](https://wicg.io/) (WICG) is a community group of the [World Wide Web Consortium (W3C)](https://www.w3.org/) that incubates new web platform features.
- [View Transitions Break Incremental Rendering](https://ericportis.com/posts/2023/view-transitions-break-incremental-rendering/)
- [Why HTTP/3 is eating the world](https://blog.apnic.net/2023/09/25/why-http-3-is-eating-the-world/)
  > HTTP/3 has seen rapid adoption due to being used by major companies like Google and Meta. It uses the QUIC protocol, which improves on TCP by more extensively encrypting metadata and enabling faster connection setup. QUIC also enhances performance by eliminating issues like head-of-line blocking and improving network handling. While HTTP/3 was created to work over QUIC, the true innovation was QUIC itself, which updates TCP with security and efficiency improvements. QUIC encryption makes it easier to update features, since middleboxes cannot access metadata. Overall, QUIC and HTTP/3 enhance web performance and security by modernizing core Internet protocols.
- [Write code for the web](https://mrmr.io/apple)
  > - Apple doesn’t care for me as a developer
  > - The best approach is to write code for the web, where no single company has control.
  > - https://news.ycombinator.com/item?id=39250406
- [Dear Developer, the Web Isn’t About You](https://www.youtube.com/watch?v=WYXSck7TyVM)
  - The web was originally simple, robust and accessible to all due to technologies like HTML working together in a layered manner.
  - Over-engineering websites with complex JavaScript frameworks makes the web fragile and excludes many users.
  - Performance and accessibility are major issues for many users but not priorities for most developers.
  - "Moving fast and breaking things" prioritizes developers over users and can exclude people from the web.
  - Researching user needs upfront through UX instead of just coding could lead to more useful websites.
  - The web is heterogeneous, not a controlled platform, so it requires an approach that acknowledges its diversity.
  - Simple, progressive techniques like serving HTML first make sites robust and usable for all.
  - The goal is caring for all people who use the web, not prioritizing new technologies.
- [The Wax and the Wane of the Web](https://alistapart.com/article/the-wax-and-the-wane-of-the-web/)
- ["Web components" considered harmful](https://www.mayank.co/blog/web-components-considered-harmful/)
  > It's better to use the specific names (custom elements, shadow DOM, templates) instead of the umbrella term "web components" to avoid confusion and make these APIs more approachable.
- [HTTP Status Codes Glossary](https://www.webfx.com/web-development/glossary/http-status-codes/)

## SPA

> I swear if I see another "SEO" guy or some rando web dev who joined the workforce after Covid complaining about SPAs by misrepresenting it, I'm gonna explode.  
> As someone who's been developing web apps since the 2000s, let me tell you the origin of SPA has few things to do with the "false promise of SPAs" he listed, but largely due to companies in the late 2000/early 2010s wanting to go "mobile first". This usually meant they still had a desktop second somewhere, which implied they were architecting the entire system to completely separate the frontends and the backend.
>
> Before, what web devs meant by frontend was essentially server-side rendered HTML templates with perhaps a little bit of jQuery running on the client-side. Now, since mobile and desktop web apps are to share some business logic and the database somehow, people had to rediscover REST by reading Roy Fielding's Phd dissertation that inspired the original HTTP. This meant now every company was moving to service-oriented architecture and started exposing their backend APIs onto the open internet so their mobile apps and SPAs running in the browser can share the same APIs. This was a cost saving measure.
>
> This period also coincided with the steady decline of full-stack webapp frameworks like Ruby on Rails and Django because for a couple of years, these frameworks had no good ways to support an API only applications. Django hadn't even reached 1.0 back then. This was a time when NodeJS was really starting to pick up momentum. Once people had started being more comfortable with JS on the server-side, lots of people suddenly realized they could push a lot of business logic to increasing powerful desktop browsers and phones, application hosts people now call "edge devices".
>
> This is the true impetus of SPA. How is CSS going to kill this need? — [wyuenho](https://news.ycombinator.com/item?id=44690219)

## Webview Case

- [Inspecting Web Views in macOS](https://blog.jim-nielsen.com/2022/inspecting-web-views-in-macos/)

## Images

- [WebP is so great… except it’s not](https://eng.aurelienpierre.com/2021/10/webp-is-so-great-except-its-not/)
  > WebP was more prone to posterization and artifacts, especially on photos with smooth gradients.  
  > For similar visual quality on a portrait photo, WebP was actually 30-39% heavier than JPEG.  
  > WebP is not necessarily better than JPEG for all photographic use cases.

## [Double-keyed Caching: How Browser Cache Partitioning Changed the Web](https://addyosmani.com/blog/double-keyed-caching/)

### How Caching Used to Work (Pre-2020)

In the traditional model, browsers maintained a simple key-value store for cached resources:

```json
cache = {
  "https://cdn.example.com/jquery-3.6.0.min.js": resourceData,
  "https://fonts.googleapis.com/css?family=Roboto": resourceData
}
```

This meant that once a user visited any site loading jQuery from a public CDN, subsequent visits to other sites using the same CDN-hosted jQuery would get an instant cache hit. This model powered the “CDN-first” approach that dominated web development through the 2010s.

The advantages were compelling:

- Reduced bandwidth usage through cross-site resource sharing
- Better performance for users visiting multiple sites using common resources
- Lower hosting costs by leveraging public CDNs
- Faster page loads through cache hits

#### The Privacy Problem

While efficient, this model leaked information. Consider these attack vectors:

1. Cache probing: Site A could check if resources from Site B were in the cache, revealing browsing history
2. Timing attacks: Measuring resource load times exposed cache status
3. Cross-site tracking: Cached resources could be used as persistent identifiers

### The New Model: Double-Keyed Caching

Double-keyed caching introduces a fundamental change to how browsers store and retrieve resources. Instead of using just the resource URL as the cache key, browsers now use two pieces of information: the top-level site making the request and the resource’s URL. Let’s look at an example.

When site-a.com requests jQuery from a CDN, the browser creates a HTTP cache entry that combines both site-a.com (the requester) and the full resource URL. Later, when site-b.com requests that exact same jQuery file, instead of reusing the cached copy, the browser creates a completely new cache entry with site-b.com as part of the key. This is what modern cache entries look like:

```json
cache = {
  {
    topLevelSite: "site-a.com",
    resource: "https://cdn.example.com/jquery-3.6.0.min.js"
  }: resourceData,
  {
    topLevelSite: "site-b.com",
    resource: "https://cdn.example.com/jquery-3.6.0.min.js"
  }: resourceData
}
```

This means that even identical resources are cached separately for each site that requests them, effectively partitioning the cache by the requesting site’s origin. While this prevents cross-site tracking and other privacy issues, it also means we’re storing duplicate copies of the same resource - a trade-off between security and efficiency.

#### Performance Impact on Cache Hit Rates

According to Chrome’s [implementation data](https://developer.chrome.com/blog/http-cache-partitioning/?utm_source=chatgpt.com#what_is_the_impact_of_this_behavioral_change), double-keyed caching leads to approximately:

- 3.6% increase in overall cache miss rate
- 4% increase in bytes loaded from the network
- 0.3% impact on First Contentful Paint (FCP)

While these numbers might seem modest, their impact varies significantly based on resource type and usage patterns.

While double-keyed caching introduces some performance overhead, it’s important to understand that these impacts are accepted as a necessary trade-off for enhanced security and privacy protection. The mechanism helps prevent various security vulnerabilities:

- Protection against timing attacks that could expose user browsing history
- Prevention of cross-site tracking through cache-based fingerprinting
- Mitigation of side-channel attacks that exploit shared cache states
- Enhanced resistance to cross-site search attacks

These security benefits justify the performance costs, though understanding and optimizing around these impacts remains crucial.
