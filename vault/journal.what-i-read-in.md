---
id: t9eilmx27nd8ytoelbm5v10
title: "\U0001F453 What I read in"
desc: ""
updated: 1708405319365
created: 1667632965028
---

## Week 08, 2024

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
