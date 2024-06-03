---
id: t9eilmx27nd8ytoelbm5v10
title: "\U0001F453 What I read in"
desc: ""
updated: 1717395880085
created: 1667632965028
---

## Week 23, 2024

- [LLMs Aren’t Just “Trained On the Internet” Anymore](https://allenpike.com/2024/llms-trained-on-internet)
- [Stealing everything you’ve ever typed or viewed on your own Windows PC is now possible with two lines of code — inside the Copilot+ Recall disaster.](https://doublepulsar.com/recall-stealing-everything-youve-ever-typed-or-viewed-on-your-own-windows-pc-is-now-possible-da3e12e9465e)

## Week 22, 2024

- [Polyfill.io, 중국 CDN 기업에 인수된 후 보안 및 안정성 문제 발생](https://x.com/hmartapp/status/1796729141309673554)
  - [polyfill.io now available on cdnjs: reduce your supply chain risk](https://blog.cloudflare.com/polyfill-io-now-available-on-cdnjs-reduce-your-supply-chain-risk)
- [Why, after 6 years, I’m over GraphQL](https://bessey.dev/blog/2024/05/24/why-im-over-graphql/)
- [Three Laws of Software Complexity](https://maheshba.bitbucket.io/blog/2024/05/08/2024-ThreeLaws.html)
  1. A well-designed system will degrade into a badly designed system over time.
  2. Complexity is a Moat (filled by Leaky Abstractions).
  3. There is no fundamental upper limit on Software Complexity.
- [An Anonymous Source Shared Thousands of Leaked Google Search API Documents with Me; Everyone in SEO Should See Them](https://sparktoro.com/blog/an-anonymous-source-shared-thousands-of-leaked-google-search-api-documents-with-me-everyone-in-seo-should-see-them/)
- [Your API Shouldn't Redirect HTTP to HTTPS](https://jviide.iki.fi/http-redirects)
  - Redirection can lead to sensitive data being transmitted in plaintext before the encrypted connection is established.
- [Terminal Text Effects](https://github.com/ChrisBuilds/terminaltexteffects)
- [Doing is normally distributed, learning is log-normal](https://hiandrewquinn.github.io/til-site/posts/doing-is-normally-distributed-learning-is-log-normal/)
  - Software estimation is challenging because it fails to recognize that learning is non-normally distributed.
- [Bubble.ai](https://www.profgalloway.com/bubble-ai/)
- [Google scrambles to manually remove weird AI answers in search](https://www.theverge.com/2024/5/24/24164119/google-ai-overview-mistakes-search-race-openai)

## Week 21, 2024

- [iTerm2 and AI hype overload](https://xeiaso.net/notes/2024/ai-hype/)
  > A terminal emulator is probably one of the most privileged programs.
  > It deals with all the secrets in the world, and the threat that it could be used to upload them all to a third party is great enough that people are willing to switch away from it sight unseen.
  >
  > not letting you use local models
- [Leaked OpenAI documents reveal aggressive tactics toward former employees](https://www.vox.com/future-perfect/351132/openai-vested-equity-nda-sam-altman-documents-employees)
- [Improvements to the Speculation Rules API](https://developer.chrome.com/blog/speculation-rules-improvements?hl=en) which allows websites to prefetch or prerender future navigations to improve performance.
- [QPick.app](https://qpick.app/) website for making random choices easy and fun!
  - https://qpick.app/burger,pizza,chicken
- [Rethinking Text Resizing on Web](https://medium.com/airbnb-engineering/rethinking-text-resizing-on-web-1047b12d2881)
  - Airbnb has made improving web accessibility a priority, focusing on the WCAG 1.4.4 Resize Text guideline. This guideline is important for users with low vision, as it requires web content to be maintained when text is scaled 200%.
- [New alternatives to innerHTML](https://fullystacked.net/innerhtml-alternatives/)
  - `setHTML`
  - `setHTMLUnsafe` does not perform input sanitization. The setHTMLUnsafe method is particularly useful for working with declarative shadow DOM, where the contents of a `<template>` element with the shadowrootmode attribute need to be rendered as shadow DOM. The setHTML method would remove the template element entirely, whereas setHTMLUnsafe preserves it.
- [A Brief Note on Highlighted Text](https://adrianroselli.com/2024/05/a-brief-note-on-highlighted-text.html)
  > If you plan to style text highlighted by the browser, you must give it sufficient contrast — 3:1 for the highlight block against its background and (probably) 4.5:1 for the text within that highlighted block against that background.
- [Target=\_blank implies rel=noopener](https://www.stefanjudis.com/today-i-learned/target-blank-implies-rel-noopener/)
- [Thinking out loud about 2nd-gen Email](https://gabrielsieben.tech/2024/05/17/thinking-out-loud-2nd-gen-email/)
- [Files](https://github.com/files-community/Files) - Building the best file manager for Windows

## Week 20, 2024

- [A Front-End Engineer's Take on LLMs](https://alexkondov.com/a-frontend-engineers-take-on-llms/)
  > the indeterminism and unreliable behavior of LLMs, which is unlike the deterministic nature of typical software development.
  > The author thinks prompt engineering will go the way testing is going. - be a skill rather than a discipline
- [The Times You Need A Custom @property Instead Of A CSS Variable](https://www.smashingmagazine.com/2024/05/times-need-custom-property-instead-css-variable/)
  > CSS custom properties allow developers to specify the syntax, initial value, and inheritance behavior of CSS variables.
  > This provides more control over how variables are used, enabling advanced animations that were previously only possible with JavaScript.
- [Edit PDFs for free with Firefox PDF Editor](https://www.mozilla.org/en-GB/firefox/features/pdf-editor/)
- [URLhaus](https://urlhaus.abuse.ch/) is a project from abuse.ch with the goal of sharing malicious URLs that are being used for malware distribution.
- [State of HTML 2023](https://2023.stateofhtml.com/)
- [Not an iPad Pro Review: Why iPadOS Still Doesn’t Get the Basics Right](https://www.macstories.net/stories/not-an-ipad-pro-review/)
  - [Missing Apps](https://www.macstories.net/stories/not-an-ipad-pro-review/#missing-apps)
  - [Not-So-Desktop-Class Apps](https://www.macstories.net/stories/not-an-ipad-pro-review/#not-so-desktop-class-apps)
  - [Files: A Slow, Unreliable File Manager](https://www.macstories.net/stories/not-an-ipad-pro-review/#files-a-slow-unreliable-file-manager)
  - [Audio Limitations](https://www.macstories.net/stories/not-an-ipad-pro-review/#audio-limitations)
  - [Multitasking: A Fractured Mess](https://www.macstories.net/stories/not-an-ipad-pro-review/#multitasking-a-fractured-mess)
  - [Spotlight](https://www.macstories.net/stories/not-an-ipad-pro-review/#spotlight)
  - [Lack of Background Processes and System-Wide Utilities](https://www.macstories.net/stories/not-an-ipad-pro-review/#lack-of-background-processes-and-system-wide-utilities)
    - [To Be Fixed Later This Year, But Only for Some](https://www.macstories.net/stories/not-an-ipad-pro-review/#to-be-fixed-later-this-year-but-only-for-some)
  - [Inefficiency by a Thousand Cuts](https://www.macstories.net/stories/not-an-ipad-pro-review/#inefficiency-by-a-thousand-cuts)
  - [The Need for Change](https://www.macstories.net/stories/not-an-ipad-pro-review/#the-need-for-change)
- [100k Stars](https://stars.chromeexperiments.com/)
- [PeaZip](https://github.com/peazip/PeaZip/) Free Archiver
- [Humanoid agent robot](https://www.unitree.com/g1/)
- [Avoid blundering: 80% of a winning strategy](https://longform.asmartbear.com/avoid-blundering/)
  - https://news.ycombinator.com/item?id=39902854
  - https://news.hada.io/topic?id=14789

## Week 19, 2024

- [Latency numbers every frontend developer should know](https://vercel.com/blog/latency-numbers-every-web-developer-should-know)
- [It’s always TCP_NODELAY. Every damn time.](https://brooker.co.za/blog/2024/05/09/nagle.html) argues that in modern distributed systems, Nagle's algorithm may no longer be necessary. The author recommends that for latency-sensitive distributed systems, TCP_NODELAY should be the default setting, as it provides better performance.
- [Deaf girl is cured in world first gene therapy trial](https://www.independent.co.uk/news/health/deaf-cure-girl-gene-therapy-b2541735.html)
- [Homebrew vs. MacPorts, A Systems Software Engineer's Perspective](https://dede.dev/posts/homebrew-vs-macPorts/)
  > In practice, many engineers use both package managers to combine the strengths of each. For instance, use Homebrew for common software and MacPorts for specialized projects.
- [chezmoi](https://github.com/twpayne/chezmoi) - Manage your dotfiles across multiple diverse machines, securely.
- [Distribution is King](https://every.to/napkin-math/distribution-is-king) - What video games can teach us about building billion-dollar companies
  - https://news.hada.io/topic?id=14677
- [Your 14-Day Free Trial Ain't Gonna Cut It](https://keygen.sh/blog/your-14-day-free-trial-aint-gonna-cut-it/)
  > For Keygen, p50 TTC(Time-to-Convert) is 41 days. My p90, 130 days; p95, 198; p99, 290.
- [JSONata](https://github.com/jsonata-js/jsonata) JSON query and transformation language
- [‘I will never go back’: Ontario family doctor says new AI notetaking saved her job](https://globalnews.ca/news/10463535/ontario-family-doctor-artificial-intelligence-notes/)

## Week 18, 2024

- [You receive a call on your phone. The caller says they're from your bank](https://mastodon.social/@Edent/112372412442888807)
- [I Reviewed 1,000s of GraphQL vs. REST perspectives](https://konfigthis.com/blog/graphql-vs-rest/)
- [I Reviewed 1,000s of Opinions on HTMX](https://konfigthis.com/blog/htmx/)
- [jsDelivr May outage postmortem](https://www.jsdelivr.com/blog/jsdelivr-may-outage-postmortem/)
- [Locality of Behavior in React Components](https://alexkondov.com/locality-of-behavior-react/)
  > Abstractions are not an enemy of locality. You don’t need to inline everything in a single file. In the context of a React component, the invocation of the function is more important than what it actually does.
- [Forms 101: More tags useful in forms](https://thevalleyofcode.com/forms/5-more-tags-useful-in-forms) - `<fieldset>`, `<legend>`
- [Form fields: File input fields](https://thevalleyofcode.com/form-fields/5-file-input-fields)
- [Form fields: Autocompleting form fields](https://thevalleyofcode.com/form-fields/8-autocompleting-form-fields)
- [Google Made Me Ruin A Perfectly Good Website: A Case Study On The AI-Generated Internet](https://theluddite.org/#!post/google-ads)
  > Google's AdSense program rejected the site, claiming it lacked unique content. To get approved, the author resorted to generating low-quality, AI-written content like recipes, poems, and blog posts about their fictional obsession with congressional apportionment. After creating this deranged additional content, Google eventually approved the site for ads. The passage is a critique of how Google's policies are leading to the proliferation of low-quality, SEO-driven content on the internet.
- [SVG Viewer](https://www.svgviewer.dev/) – View, edit, and optimize SVGs
- [What can LLMs never do?](https://www.strangeloopcanon.com/p/what-can-llms-never-do)
  > inability to perform certain tasks that seem simple for humans, like playing Wordle or predicting the output of cellular automata.
- [World Wide Web (1991)](https://info.cern.ch/hypertext/WWW/TheProject.html)
- [Leaving Rust gamedev after 3 years](https://loglog.games/blog/leaving-rust-gamedev/)
  > Rust's strengths do not always align well with the needs of practical game development.
- [Passkeys: A Shattered Dream](https://fy.blackhats.net.au/blog/2024-04-26-passkeys-a-shattered-dream/)
  > The technology has become increasingly controlled by major tech companies like Google and Apple with problems about device compatibility, data loss, and vendor lock-in. Password managers may provide a better user experience for most consumers.

## Week 17, 2024

- [CSS: Specificity](https://thevalleyofcode.com/css/4-specificity)
- [TDD's Missing Skill: Behavioral Composition](https://tidyfirst.substack.com/p/tdds-missing-skill-behavioral-composition)
- [The Man Who Killed Google Search](https://www.wheresyoured.at/the-men-who-killed-google/)
- [Cognition Labs: "Today we're excited to introduce Devin, the first AI software engineer.](https://www.cognition-labs.com/introducing-devin)
  - [They actually dont do ANYTHING themselfs](https://old.reddit.com/r/cscareerquestions/comments/1bd12gc/relevant_news_cognition_labs_today_were_excited/kujyidr/) - Analytics: Hotjar, Website: NextJS, Login: Clerk, Jobs: Ashby, Waitlist: Google docs (ROFL), Learn more about their funding: A link to twitter
- [Programming Is Mostly Thinking](https://agileotter.blogspot.com/2014/09/programming-is-mostly-thinking.html)
- [Coroutines and effects](https://without.boats/blog/coroutines-and-effects/)

## Week 16, 2024

- [Why you need a "WTF Notebook"](https://www.simplermachines.com/why-you-need-a-wtf-notebook/)
- [The invisible seafaring industry that keeps the internet afloat.](https://www.theverge.com/c/24070570/internet-cables-undersea-deep-repair-ships)
- [NEVER sacrifice your life for an artificial deadline.](https://news.ycombinator.com/user?id=nine_zeros)
  - How to determine if something is an artificial deadline? Because if it were a real deadline with significance to the business, they'd pull more hands on deck, remove roadblocks relentlessly day after day, and even offer to take portions of your work on themselves so that the deadlines can be met.
- [HTMX Is So Cool I Rolled My Own!](https://dbushell.com/2024/04/16/htmx-and-modern-javascript/)
- [The Wax and the Wane of the Web](https://alistapart.com/article/the-wax-and-the-wane-of-the-web/)
- [My favourite animation trick: exponential smoothing](https://lisyarus.github.io/blog/programming/2023/02/21/exponential-smoothing.html) avoids issues like jittering or overshooting that can occur with other methods.
- [DevTools Tips & Tricks](https://frontendmasters.com/blog/devtools-tips-tricks/)
  - [Inspect Popups on Hover](https://frontendmasters.com/blog/devtools-tips-tricks/#1-inspect-popups-on-hover)
  - [Use logpoints](https://frontendmasters.com/blog/devtools-tips-tricks/#2-use-logpoints)
  - [Emulate foldable devices](https://frontendmasters.com/blog/devtools-tips-tricks/#3-emulate-foldable-devices)
  - [Inspect Event streams](https://frontendmasters.com/blog/devtools-tips-tricks/#7-inspect-event-streams)
  - [Live expressions](https://frontendmasters.com/blog/devtools-tips-tricks/#9-live-expressions)
- [Gap is the new Margin](https://frontendmasters.com/blog/gap-is-the-new-margin/)
  > > [Margin breaks component encapsulation.](https://mxstbr.com/thoughts/margin/) A well-built component should not affect anything outside itself.  
  > > [Prediction](https://dev.to/argyleink/5-css-predictions-for-2020-pl3): margins in stylesheets will decline as gap in stylesheets climb
- [Hardest Problem in Computer Science: Centering Things](https://tonsky.me/blog/centering/)
  > STOP. USING. FONTS. FOR. ICONS.
- https://ios404.com/ - missing web features in iOS
- [Hono](https://hono.dev/) is a small, simple, and ultrafast web framework for the Edges. It works on any JavaScript runtime: Cloudflare Workers, Fastly Compute, Deno, Bun, Vercel, AWS Lambda, Lambda@Edge, and Node.js.
- [Old CSS, new CSS](https://eev.ee/blog/2020/02/01/old-css-new-css/)
  > > `<H1><FONT COLOR=red>...</FONT></H1>` …every single goddamn time.
  >
  > is in fashion again! Only now it’s called class="text-red-500" [:o)](https://news.ycombinator.com/item?id=40029373)

## Week 15, 2024

- [QCon London: How Duolingo Sent 4 Million Push Notifications in 6 Seconds During the Super Bowl Break](https://www.infoq.com/news/2024/04/qcon-london-duolingo-super-bowl/)
- [QWANJI](https://byronicalpatrick.github.io/qwanji/)
- [The Power of :has() in CSS](https://css-tricks.com/the-power-of-has-in-css/)
  ```css
  h1:has(+ h2) {
    color: blue;
  }
  ```
- [How to Kill the Cascade](https://robinrendle.com/the-cascade/017-how-to-kill-the-cascade/)
- [In-app browsers are still a privacy, security, and choice problem](https://www.theregister.com/2024/03/27/inapp_browsers/)
- [How to think about HTML responsive images](https://danburzo.ro/responsive-images-html/)
  ```html
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="macos-dark.png" />
    <source media="print" srcset="macos-contrast.png" />
    <img src="macos-light.png" alt="…" />
  </picture>
  ```
- [The 37signals Guide to Internal Communication](https://37signals.com/how-we-communicate)

## Week 14, 2024

- [An Interactive Guide to CSS Container Queries](https://ishadeed.com/article/css-container-query-guide)

  ```css
  /* Try to add more items and see what happens. */
  .timelineWrapper {
    container: timeline / inline-size;
    --force-vertical: false;

    &:has(.c-timeline__item:nth-last-child(n + 5)) {
      --force-vertical: true;
    }
  }
  ```

  ```css
  @container timeline (inline-size > 430px) and style(--force-vertical: false) {
    /* Apply the full variation. */
  }
  ```

- [Reddit Migrates Media Metadata from S3 and Other Systems into AWS Aurora Postgres](https://www.infoq.com/news/2024/03/reddit-metadata-s3-postgres/)
- [Chill Scroll Snapping: Article Headers](https://frontendmasters.com/blog/chill-scroll-snapping-article-headers/)
- [JavaScript Visualized: Promise Execution](https://www.lydiahallie.com/blog/promise-execution)
  > Long story short, Promises are just objects with some additional functionality to change their internal state.
  >
  > The cool thing about Promises is that this can trigger an asynchronous action if a handler is attached by either then or catch. Since the handlers are pushed to the Microtask Queue, you can handle the eventual result in a non-blocking way. This makes it easier to handle errors, chain multiple operations together, and keep your code more readable and maintainable!
- [Happy 404 Day. Whats your favorite 404 error page?](https://news.ycombinator.com/item?id=39928950)
  - [Financial Times 404](https://www.ft.com/404)
- [Kobold Letters](https://lutrasecurity.com/en/articles/kobold-letters/) - Why HTML emails are a risk to your organization
- [Spicing up text with text-emphasis in CSS](https://www.amitmerchant.com/spicing-up-text-with-text-emphasis-in-css/)
  ```css
  .text-emphasis-dollar {
    text-emphasis: "$" lime;
    text-emphasis-position: under;
  }
  ```
- [CSS scoping from What You Need to Know about Modern CSS (Spring 2024 Edition)](https://frontendmasters.com/blog/what-you-need-to-know-about-modern-css-spring-2024-edition/#scoping)
- [CSS Button Styles You Might Not Know](https://dbushell.com/2024/03/10/css-button-styles-you-might-not-know/)
  > The manipulation value disables gestures like ‘double-tap to zoom’. Other gestures like ‘panning’ and ‘pinch to zoom’ are unaffected. An extra benefit is that the browser no longer needs to delay the click event waiting for a second tap.
  ```css
  .button,::file-selector-button {
    inline-size: fit-content;
    touch-action: manipulation;
    user-select: none;
  }
  *:focus-visible {
      outline: 2px solid magenta;
      outline-offset: 2px;
    }
  }
  ```
- [BIG DATA IS DEAD](https://motherduck.com/blog/big-data-is-dead/)
  > The author suggests that the real problem is often data hoarding rather than true "Big Data" challenges. Overall, the passage contends that the Big Data hype has passed and organizations should focus on using their data effectively rather than worrying about sheer data volume.
- [What’s the Difference Between OLAP and OLTP?](https://aws.amazon.com/compare/the-difference-between-olap-and-oltp/)
- [Postgres is eating the database world](https://medium.com/@fengruohang/postgres-is-eating-the-database-world-157c204dcfc4)
  > PostgreSQL is emerging as a dominant database platform that is capable of handling a wide range of use cases, from OLTP to OLAP workloads. Its extensibility through a thriving ecosystem of add-ons and integrations allows it to compete with specialized databases across various domains like time-series, geospatial, and vector data. The rise of analytical extensions like ParadeDB and DuckDB have further bolstered PostgreSQL's capabilities, making it a viable alternative to dedicated data warehousing solutions. As hardware advancements have addressed performance and scalability concerns, the need for separate OLTP and OLAP systems is diminishing, leading to a convergence where PostgreSQL can serve as a unified, multi-model database. The author argues that the real competitive frontier now lies in leveraging PostgreSQL's extensibility through integrated distributions and services, rather than focusing on the core database kernel.
- [The power of CSS Variables 💪: A flexible solution for spacing utilities](https://dev.to/karsten_biedermann/the-power-of-css-variables-a-flexible-solution-for-spacing-utilities-4bch)

  ```html
  <div style="--space-top: 30px; --space-bottom: 100px;"></div>
  ```

  ```css
  @media (min-width: 992px) {
    [style*="--space-bottom"] {
      margin-bottom: var(--space-bottom);
    }
    [style*="--space-top"] {
      margin-top: var(--space-top);
    }
  }
  ```

- [What is safe alignment in CSS?](https://frontendmasters.com/blog/what-is-safe-alignment-in-css/)
  ```css
  .flex {
    display: flex;
    align-items: safe center;
  }
  ```
- [LiveView is best with Svelte](https://blog.sequin.io/liveview-is-best-with-svelte/)
  > LiveView is a unique approach to building web applications that combines the benefits of server-rendered and client-side frameworks. While LiveView offers many advantages, the authors found some limitations around handling complex client-side interactions and the blurry line between client and server state. To address these challenges, the authors describe using LiveView together with the Svelte frontend framework, which they found to be a powerful and productive combination. The LiveView backend handles data fetching, validation, and state management, while the Svelte frontend focuses on rendering and simple event handling. This "LiveSvelte" approach eliminates the need for a separate frontend microservice and allows for a clean separation of concerns between the client and server.
  >
  > > One possible solution which I didn't investigate, but should work, is to write all game logic in gleam ([https://gleam.run/](https://gleam.run/)). Gleam is compatible with Elixir, AND it also can compile to js, so you could in theory run the same code on the server and the client. — [POiNTx](https://news.ycombinator.com/item?id=39919223)
- [HTTP Speed](https://kitsonkelly.com/posts/http-speed) - Deno, Bun, Node.js
- [Optimizing Javascript for fun and for profit](https://romgrk.com/posts/optimizing-javascript)
  - [Avoid different shapes](https://romgrk.com/posts/optimizing-javascript#2-avoid-different-shapes)
- [Runtime compatibility across JavaScript runtimes](https://runtime-compat.unjs.io/)
  - https://node.green/
- [Alpine Ajax - Comparisons between Alpine AJAX and other similar libraries](https://alpine-ajax.js.org/comparisons/)
- [WebSockets vs Server-Sent-Events vs Long-Polling vs WebRTC vs WebTransport](https://rxdb.info/articles/websockets-sse-polling-webrtc-webtransport.html)

## Week 13, 2024

- [You Want border-color: transparent, Not border: none](https://frontendmasters.com/blog/you-want-border-color-transparent-not-border-none/)
  - `@media (forced-colors: active)`
- [There is no EU cookie banner law](https://www.bitecode.dev/p/there-is-no-eu-cookie-banner-law)
- [Why choose async/await over threads in Rust?](https://notgull.net/why-not-threads/) explains how async/await allows for more composable and flexible concurrency compared to threads, which can be difficult to synchronize. The author argues that the benefits of async/await, such as its ability to easily add timeouts and other functionality, are not always well-communicated.
  - [Futex congestion collapse. Starvation of unfair mutexes.](https://news.ycombinator.com/item?id=39813525)
- [Game of Life, simulating itself, infinitely zoomable](https://oimo.io/works/life/)
- https://www.libhunt.com/css

## Week 11, 2024

- [mise-en-place](https://github.com/jdx/mise) - dev tools, env vars, task runner
- [Flox](https://github.com/flox/flox/) is a virtual environment and package manager all in one.
- [You should separate your billing from entitlements](https://arnon.dk/why-you-should-separate-your-billing-from-entitlement/)
- [5 things I learned while developing a billing system](https://arnon.dk/5-things-i-learned-developing-billing-system/)
- [Devin: AI Software Engineer - comments](https://news.ycombinator.com/item?id=39679787)
- [Designing better target sizes](https://ishadeed.com/article/target-size/)
- [Techniques to Break Words](https://adrianroselli.com/2024/02/techniques-to-break-words.html)
  - Probably don’t add `&shy;` without guidance from a copywriter.
  - Probably don’t add `&shy;` to foreign words without a localization expert or at least a native speaker.
  - Probably don’t add `&shy;` to URLs, email addresses, code blocks, and so on.
  - Probably restrict `<wbr>` to URLs, email addresses, code blocks, and similar words where technical accuracy is paramount.
  - Probably restrict `<wbr>` to _before_ periods and dashes and maybe slashes in URLs and emails so it doesn’t look like the sentence or address has ended.
- [Getting Started with Style Queries](https://developer.chrome.com/docs/css-ui/style-queries?hl=en)
  - Can't you do it with attributes?
- [Bruno](https://github.com/usebruno/bruno) - Fast and Git-friendly open-source API client (Postman alternative)

## Week 10, 2024

- [CSS :has() Interactive Guide](https://ishadeed.com/article/css-has-guide)
- [A practical guide to using shadow DOM](https://www.mayank.co/blog/declarative-shadow-dom-guide/)
- [Aristotle — How to live a good life](https://ralphammer.com/aristotle-how-to-live-a-good-life/) - Ralph Ammer
  > Happiness is not a feeling of pleasure. **Happiness is the pursuit of excellence**.
- [CSS for printing to paper](https://voussoir.net/writing/css_for_printing)

## Week 09, 2024

- [Blur radius comparison](https://bjango.com/articles/blurradiuscomparison/)
  > the three Sketch blur types, scaled to the equivelent CSS box-shadow value. They now all match!
- [WebPerf Snippets](https://webperf-snippets.nucliweb.net/)
- [So, what exactly did Apple break in the EU?](https://blog.tomayac.com/2024/02/28/so-what-exactly-did-apple-break-in-the-eu/)
- [Youtube video embedding harm reduction](https://dustri.org/b/youtube-video-embedding-harm-reduction.html)
  ```html
  <iframe
    credentialless
    allowfullscreen
    referrerpolicy="no-referrer"
    sandbox="allow-scripts allow-same-origin"
    allow="accelerometer 'none'; ambient-light-sensor 'none'; autoplay 'none'; battery 'none'; browsing-topics 'none'; camera 'none'; display-capture 'none'; domain-agent 'none'; document-domain 'none'; encrypted-media 'none'; execution-while-not-rendered 'none'; execution-while-out-of-viewport ''; gamepad 'none'; geolocation 'none'; gyroscope 'none'; hid 'none'; identity-credentials-get 'none'; idle-detection 'none'; local-fonts 'none'; magnetometer 'none'; microphone 'none'; midi 'none'; otp-credentials 'none'; payment 'none'; picture-in-picture 'none'; publickey-credentials-create 'none'; publickey-credentials-get 'none'; screen-wake-lock 'none'; serial 'none'; speaker-selection 'none'; usb 'none'; window-management 'none'; xr-spatial-tracking 'none'"
    ,
    csp="sandbox allow-scripts allow-same-origin;"
    width="560"
    height="315"
    src="https://www.youtube-nocookie.com/embed/jfKfPfyJRdk"
    title="lofi hip hop radio 📚 - beats to relax/study to"
    frameborder="0"
    loading="lazy"
  ></iframe>
  ```
- [Netlify just sent me a $104K bill for a simple static site](https://old.reddit.com/r/webdev/comments/1b14bty/netlify_just_sent_me_a_104k_bill_for_a_simple/)
- [Four Steps to Achieving Operational Flow and Improving Quality in Tech Teams](https://www.infoq.com/articles/achieve-flow-improve-quality/)
  - Take on fewer things; focus on doing a complete job.
  - Dependencies destroy flow. Break down and remove dependencies in order to improve your team(s)'s ability to get things done.
  - Shift your focus toward keeping work moving and away from keeping people busy.
  - Work creates ROI only when a customer can use it. That means that completing work is more important than being busy.
  - It's more important for a team to be able to keep work moving than it is to keep the team small. Get work moving first, then think about how to reduce team size without compromising flow.
- [Dear Developer, the Web Isn’t About You](https://www.youtube.com/watch?v=WYXSck7TyVM)
  - The web was originally simple, robust and accessible to all due to technologies like HTML working together in a layered manner.
  - Performance and accessibility are major issues for many users but not priorities for most developers.
  - Simple, progressive techniques like serving HTML first make sites robust and usable for all.
  - The goal is caring for all people who use the web, not prioritizing new technologies.
- [SaaS Payment vs. SaaS Billing - What Those Terms Mean and What the Differences Are](https://www.wingback.com/blog/saas-payment-vs-saas-billing)
- [🦑 The 14 pains of building your own billing system](https://arnon.dk/the-14-pains-of-billing/)
- [Decoding Apple's Ploy To Scuttle Progressive Web Apps](https://infrequently.org/2024/02/home-screen-advantage/)
- [What is a non-capturing group in regular expressions?](https://stackoverflow.com/a/3513858/5163033)
- [console.delight](https://frontendmasters.com/blog/console-delight/)
- [Quality is a hard sell in big tech](https://www.pcloadletter.dev/blog/big-tech-quality/)

## Week 08, 2024

- [JavaScript Bloat in 2024](https://tonsky.me/blog/js-bloat/)
- [Scroll-Driven Animations: You want overflow: clip, not overflow: hidden](https://www.bram.us/2024/02/14/scroll-driven-animations-you-want-overflow-clip-not-overflow-hidden/)
- [Introducing SafeTest by Netflix: A Novel Approach to Front End Testing](https://netflixtechblog.com/introducing-safetest-a-novel-approach-to-front-end-testing-37f9f88c152d)
- [🔒Securing Web: A Deep Dive into Content Security Policy (CSP)](https://dev.to/vashnavichauhan18/securing-web-a-deep-dive-into-content-security-policy-csp-2nna)
- [Using localStorage in Modern Applications: A Comprehensive Guide](https://rxdb.info/articles/localstorage.html)
- [Using abbreviations for long CSS properties in VS Code](https://www.amitmerchant.com/using-abbreviations-for-long-css-properties-in-vs-code/)
- https://www.perfectmemory.ai/
  - https://www.rewind.ai/
- [If Architects had to work like Programmers](http://www.gksoft.com/a/fun/architects.html)
- [Bloom Filters](https://samwho.dev/bloom-filters/)
  - Bloom filters return true it doesn't mean "yes", it means "maybe", false-positive.
  - If you're happy to accept being wrong 0.0001% of the time (1 in a million), you could use a bloom filter which can store the same data in 82% reduction in size.
- [In Defense of Simple Architectures](https://danluu.com/simple-architectures/)
  - [Microservices aren't a performance strategy. They are a POTENTIAL cost saving strategy against performance. And an engineering coordination strategy.](https://news.ycombinator.com/item?id=39441508)
  - [Towards Modern Development of Cloud Applications](https://dl.acm.org/doi/pdf/10.1145/3593856.3595909)
- [The Case Against Caffeine](https://zantafakari.substack.com/p/the-case-against-caffeine)
  - But it gets worse, especially if you drink lots of caffeine throughout the day. In that case, you never give your body the chance to clear it out. So the base concentration in your blood slowly creeps up. - https://zantafakari.substack.com/i/141012714/the-science-of-sleep
- [htmz](https://github.com/Kalabasa/htmz) is a minimalist HTML microframework that gives you the power to create dynamic web user interfaces with the familiar simplicity of plain HTML.
  ```html
  <iframe
    hidden
    name="htmz"
    onload="setTimeout(()=>document.querySelector(this.contentWindow.location.hash||null)?.replaceWith(...this.contentDocument.body.childNodes))"
  ></iframe>
  ```

## Week 07, 2024

- [LLRT (**L**ow **L**atency **R**un**t**ime)](https://github.com/awslabs/llrt) is a lightweight JavaScript runtime designed to address the growing demand for fast and efficient Serverless applications. LLRT offers up to over **10x** faster startup and up to **2x** overall lower cost compared to other JavaScript runtimes running on **AWS Lambda**
- [A Guide To Designing For Older Adults](https://www.smashingmagazine.com/2024/02/guide-designing-older-adults/)
  > Today, one billion people are 60 years or older. That’s 12% of the entire world population, and the age group is growing faster than any other group. Yet, online, the needs of older adults are often overlooked or omitted.
- [How to make external links accessible](https://blog.pope.tech/2024/01/02/how-to-make-external-links-accessible/)
  - [Why external links should open in the same tab](https://blog.pope.tech/2024/01/02/how-to-make-external-links-accessible/#why)
    - giving users the choice
  - [When external links should open in a new tab](https://blog.pope.tech/2024/01/02/how-to-make-external-links-accessible/#when)
    - Lose form progress
    - An alternative solution
    - Terminate login
    - User needs information on both pages
  - [Accessible design and code for external links opening in a new tab](https://blog.pope.tech/2024/01/02/how-to-make-external-links-accessible/#design)
    - give users a warning that it opens in a new tab.
- [:focus vs :focus-visible](https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible#focus_vs_focus-visible)
  > The `:focus-visible` pseudo-class also matches the focused element, but only if the user needs to be informed where the focus currently is.
  - https://daverupert.com/2024/01/focus-visible-love/
- [The psychology of site speed and human happiness](https://www.speedcurve.com/blog/psychology-site-speed/)
- [Apple has not fixed the macOS audio left/right balance bug for nearly 10 years](https://twitter.com/ffaebi/status/1757669861377949930)
  - https://news.ycombinator.com/item?id=39367460
- [I designed a cube that balances itself on a corner](https://willempennings.nl/balancing-cube/)
- [How to Study](https://cse.buffalo.edu/~rapaport/howtostudy.html)
- [(Almost) Every infrastructure decision I endorse or regret after 4 years running infrastructure at a startup](https://cep.dev/posts/every-infrastructure-decision-i-endorse-or-regret-after-4-years-running-infrastructure-at-a-startup/)
- [Classless CSS](https://github.com/dbohdan/classless-css)
- [Drop-in switcher for previewing minimal CSS frameworks](https://dohliam.github.io/dropin-minimal-css/)

## Week 06, 2024

- [SQL for the Weary](https://gvwilson.github.io/sql-tutorial/)
- [Command Line Interface Guidelines](https://clig.dev/)
- [Simplify: move code into database functions](https://sive.rs/pg)
  - Databases outlive the applications that access them.
  - the database is actually [quite smart](https://www.postgresql.org/docs/current/server-programming.html).
  - examples: [constraints](https://www.postgresql.org/docs/current/ddl-constraints.html), [triggers](https://www.postgresql.org/docs/current/trigger-definition.html), functions, [create JSON directly](https://www.postgresql.org/docs/current/functions-json.html#FUNCTIONS-JSON-CREATION-TABLE).
  - If you like JavaScript, check out the promising [plv8](https://plv8.github.io/).
  - **branching? source code history(Migrations)?**
    - [How to work with stored procedures and not die trying](https://github.com/kblok/tech-posts/blob/master/working-with-stored-procedures.md)?
    - [You can use a DDL trigger to keep all revisions in a table in a separate database (and of course back up that database frequently).](https://dba.stackexchange.com/a/33544) - [SQL Server DDL Triggers to Track All Database Changes](http://www.mssqltips.com/sqlservertip/2085/sql-server-ddl-triggers-to-track-all-database-changes/)
- [It's Time To Get Over That Stored Procedure Aversion You Have](https://bigmachine.io/databases/its-time-to-get-over-that-stored-procedure-aversion-you-have/)
- [Postgresql is enough](https://gist.github.com/cpursley/c8fb81fe8a7e5df038158bdfe0f06dbb)
  > - [As an application grows in complexity, you start to realize _why_ there's a stack, rather than just a single technology to rule them all. Trying to cram everything into Postgres (or lambdas, or S3, or firebase, or whatever other tech you're trying to consolidate on) starts to get really uncomfortable.](https://news.ycombinator.com/item?id=39274174)
  > - [... both worked: the PG queue was never grown out of, and generally SQS was easy to work with & reliable. But what I've also seen is "Let's introduce bespoke tech that nobody on the team, including the person introducing it, has experience in, for a queue that isn't even the main focus of what we're building" — this I'm less fine with.](https://news.ycombinator.com/item?id=39274805)
- [People will never be motivated to go the extra mile by a standardized, bureaucratized process.](https://news.ycombinator.com/item?id=39271692)
  - https://news.ycombinator.com/item?id=39272190
- [Companies embracing SMS for account logins should be blamed for SIM-swap attacks](https://keydiscussions.com/2024/02/05/sim-swap-attacks-can-be-blamed-on-companies-embracing-sms-based-password-resets/)
- [Write code for the web](https://mrmr.io/apple)
  > - Apple doesn’t care for me as a developer
  > - The best approach is to write code for the web, where no single company has control.
  > - https://news.ycombinator.com/item?id=39250406
- [tints.dev](https://www.tints.dev/) - Palette Generator + API for Tailwind CSS
- [The undercover generalist](https://ochagavia.nl/blog/the-undercover-generalist/)
  > - Needing to look like a specialist
  > - Telling people what they want to hear
- [Lazy Hydration and Server Components in Nuxt – Vue.js 3 Performance](https://vueschool.io/articles/vuejs-tutorials/lazy-hydration-and-server-components-in-nuxt-vue-js-3-performance/)
  > Most of the components don’t need to be eagerly hydrated
- [How to align the text of the last paragraph line](https://www.stefanjudis.com/today-i-learned/how-to-align-the-text-of-the-last-paragraph-line/)
  > `text-align-last`
- [Benchmarks of JavaScript Package Managers(daily updated)](https://pnpm.io/benchmarks)

## Week 05, 2024

- [Generally speaking, you’ll want to use `text-wrap: balance` for headings and `text-wrap: pretty` for body text.](https://codersblock.com/blog/nicer-text-wrapping-with-css-text-wrap/)
- [Portable Network Graphics (PNG, pronounced "ping")](https://www.w3.org/TR/2003/REC-PNG-20031110/#1Scope)
- [Variable Fonts](https://v-fonts.com/)

## Week 04, 2024

- [A Single Small Map Is Enough For A Lifetime](https://www.noemamag.com/a-single-small-map-is-enough-for-a-lifetime/)
- [iPhone Apps Secretly Harvest Data When They Send You Notifications, Researchers Find](https://gizmodo.com/iphone-apps-can-harvest-data-from-notifications-1851194537)
- [npm malware (@npm_malware) on X](https://twitter.com/npm_malware)
- [The problem with disabled buttons and what to do instead](https://adamsilver.io/blog/the-problem-with-disabled-buttons-and-what-to-do-instead/)
- [When to use CSS text-wrap: balance; vs text-wrap: pretty;](https://blog.stephaniestimac.com/posts/2023/10/css-text-wrap/)
  > Use text-wrap: balance; on headings and subheadings. And use text-wrap: pretty; on paragraphs of text to get rid of orphans on the last line. Despite the Chromium-only support, these would be a good candidate for progressive enhancement.
- [A Practical Introduction to Scroll-Driven Animations with CSS scroll() and view()](https://tympanus.net/codrops/2024/01/17/a-practical-introduction-to-scroll-driven-animations-with-css-scroll-and-view/) - At the time of writing this, it is Chromium only.
- [12 Modern CSS One-Line Upgrades](https://moderncss.dev/12-modern-css-one-line-upgrades/)
  - Stable Enhancements: `accent-color`, `scroll-margin-top/bottom` - `[id]`
  - progressive enhancement: `overscroll-behavior: contain`, `scrollbar-gutter`
  - https://news.ycombinator.com/item?id=39176717
- [Should I Open Source my Company?](https://supabase.com/blog/should-i-open-source-my-company)
- [What Is Nightshade?](https://nightshade.cs.uchicago.edu/whatis.html) - An offensive tool for artists against AI art generators

## Week 03, 2024

- [PIDs: Creating Stable Control in Games](https://azeemba.com/posts/pids-creating-stable-control-in-games.html)
- [U.S. Developers Can Now Offer Non-App Store Purchasing Option, But Apple Will Still Collect Commissions](https://forums.macrumors.com/threads/u-s-developers-can-now-offer-non-app-store-purchasing-option-but-apple-will-still-collect-commissions.2416540/)
- [Teach Yourself Programming in Ten Years](https://norvig.com/21-days.html) - Why is everyone in such a rush?
- [Slashing Data Transfer Costs in AWS by 99%](https://www.bitsand.cloud/posts/slashing-data-transfer-costs/)
  > AWS replicates S3 data between availability zones
  >
  > - https://news.ycombinator.com/item?id=38999902 - https://news.ycombinator.com/item?id=38999947
- [Preventing HTTPS Downgrade Attacks](https://auth0.com/blog/preventing-https-downgrade-attacks/)
  > - configuring servers to redirect all HTTP traffic to HTTPS and setting the HTTP Content-Security-Policy and Strict-Transport-Security headers to enforce HTTPS-only browsing
  > - The HSTS preload directive further strengthens security by ensuring browsers always use HTTPS for a domain

## Week 02, 2024

- [Use cases of soft delete](https://rahulraj.io/a-better-deletion-approach-than-soft-delete/)
  > - You want to delete records, but also want to retain them for n number of days, just for a safer side against accidental deletion.
  > - You want to exclude some records (permanent retain) under explicit requirements, even if they match the criteria of an eligible record to be deleted.
  > - You don't want to delete the actual resource before returning the resource back. Basically, deletion before returning the value is not desired.
  > - You don't want to modify existing table schema(s) to accommodate soft delete key.
  > - You want the tables as loosely coupled as possible without having to worry about deletion logic.
- [All JavaScript and TypeScript Features of the last 3 years](https://betterprogramming.pub/all-javascript-and-typescript-features-of-the-last-3-years-629c57e73e42)
- [Using the CSS contain property: A deep dive](https://blog.logrocket.com/using-css-contain-property-deep-dive/)
  > to decrease the burden on browsers for layout calculations, paints, repaints, and reflows.
- [One YouTube Embed weighs almost 1.2 MB](https://www.zachleat.com/web/youtube-embeds/)
  > https://github.com/paulirish/lite-youtube-embed
- [Correctly Configure (Pre) Connections](https://csswizardry.com/2023/12/correctly-configure-preconnections/)
- [atuin](https://github.com/atuinsh/atuin) - ✨ Magical shell history
- [Prevent unnecessary network requests with the HTTP Cache](https://web.dev/articles/http-cache?hl=en)
- [Understanding SVG Paths](https://www.nan.fyi/svg-paths)
- [6 CSS snippets every front-end developer should know in 2023](https://web.dev/articles/6-css-snippets-every-front-end-developer-should-know-in-2023?hl=en)
- [Chrome enables desktop mode by default on premium tablets](https://developer.chrome.com/blog/desktop-mode?hl=en)
- [Zendesk Moves from DynamoDB to MySQL and S3 to Save over 80% in Costs](https://www.infoq.com/news/2023/12/zendesk-dynamodb-mysql-s3-cost/)
- [Why LinkedIn chose gRPC+Protobuf over REST+JSON: Q&A with Karthik Ramgopal and Min Chen](https://www.infoq.com/news/2023/12/linkedin-grpc-protobuf-rest-json/)
- [CSS Scroll Snapping Aligned With Global Page Layout: A Full-Width Slider Case Study](https://www.smashingmagazine.com/2023/12/css-scroll-snapping-aligned-global-page-layout-case-study/)
- [What is Token-Based Authentication?](https://www.permit.io/blog/what-is-token-based-authentication/)

## Week 01, 2024

- [LLMs and Programming in the first days of 2024](http://antirez.com/news/140)
  > The author discusses their extensive use of large language models for programming tasks over the past year. They find LLMs most helpful for writing disposable code, learning new frameworks quickly, and accelerating documentation searches. While useful, LLMs still struggle with system programming problems requiring complex reasoning. The author believes LLMs have begun to show rudimentary reasoning abilities through their interpolation of concepts, but their capabilities are still limited. Overall, they argue LLMs are a valuable tool for programmers that can help focus time on more important problems and skills.
- [Why asking your customers what they want doesn't work](https://techbooks.substack.com/p/why-asking-your-customers-what-they)
  > A fast food chain failed to increase milkshake sales despite adding requested elements, but succeeded by observing what "jobs" customers hired milkshakes for, such as a boring commute.
  > [Don‘t listen to your customer. Watch your customer.](https://news.ycombinator.com/item?id=38823091)
- [Best-Practices for API Authorization](https://www.permit.io/blog/)
- [It's not microservice or monolith; it's cognitive load you need to understand first](https://fernandovillalba.substack.com/p/its-not-microservice-or-monolith)
- [Cold-blooded software](https://dubroy.com/blog/cold-blooded-software/)
- [Heynote](https://github.com/heyman/heynote/) is a dedicated scratchpad for developers

## [[2023|journal.what-i-read-in.2023]]

## [[2022|journal.what-i-read-in.2022]]
