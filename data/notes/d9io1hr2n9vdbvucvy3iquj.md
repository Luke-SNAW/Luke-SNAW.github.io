
## Week 52, 2023

- [Stop using {} in Typescript](https://medium.com/@sukheja.varun/stop-using-in-typescript-ed24d3532d9e)
  - `Record<string, unkown>`
  - `{ [key:string]: unknown }`
- [Introducing four new international features in CSS](https://developer.chrome.com/blog/css-i18n-features?hl=en)
  - From Chrome 119: Japanese phrase line breaking with `word-break: auto-phrase`.
  - Behind a flag from Chrome 120: Inter-script spacing with the `text-autospace` property.
  - Under development: Chinese, Japanese, and Korean (CJK) punctuation kerning with the `text-spacing-trim` property.
  - Consistent minimum font size across languages.
- [Micro Frontend Synergy: Techniques for Effective Communication](https://medium.com/@rk-tech/micro-frontend-synergy-techniques-for-effective-communication-97df104931ed)
- [How Pinterest scaled to 11 million users with only 6 engineers](https://read.engineerscodex.com/p/how-pinterest-scaled-to-11-million)
  - Use known, proven technologies. Pinterest’s dive into newer technologies at the time led to issues like data corruption.
  - Keep it simple. (A recurring theme!)
  - Don’t get too creative. The team settled on an architecture where they could add more of the same nodes to scale.
  - Limit your options.
  - Sharding databases > clustering. It reduced data transfer across nodes, which was a good thing.
  - Have fun! New engineers would contribute code in their first week.
- [How Big is YouTube?](https://ethanzuckerman.com/2023/12/22/how-big-is-youtube/)
  > He details an experiment where he and others were able to collect over 10,000 truly random YouTube videos using an inefficient "drunk dialing" method to guess video URLs.
  > This allowed them to estimate that YouTube contains over 13 billion videos and that 4 billion were added just in 2023.
- [Google OAuth is broken (sort of)](https://trufflesecurity.com/blog/google-oauth-is-broken-sort-of/)
  > It is possible for former employees to retain access to workplace apps like Slack and Zoom after leaving a company by creating a Google account using a plus sign email address derived from their work email. (janedoe+oldjob@company.com)
- [Advice for new software devs who've read all those other advice essays](https://buttondown.email/hillelwayne/archive/advice-for-new-software-devs-whove-read-all-those/)

## Week 51, 2023

- [A Quick Guide on How to Create Accessible Buttons in HTML](https://hackernoon.com/a-quick-guide-on-how-to-create-accessible-buttons-in-html)
  - Icon with Text Buttons - `aria-hidden=true` attribute for the svg icon
  - Icon Buttons - `aria-label` on the button tag
  - ... the alternatives.
  - The size of the target for pointer inputs is at least 44 by 44 CSS pixels.
- [How to use Chrome's accessibility tree](https://blog.pope.tech/2023/11/27/how-to-use-chromes-accessibility-tree/)
- [Lost in Translation: Tips for Multilingual Web Accessibility](https://benmyers.dev/blog/multilingual-web-accessibility/)
- [WebP is so great… except it’s not](https://eng.aurelienpierre.com/2021/10/webp-is-so-great-except-its-not/)
  > WebP was more prone to bad posterization and artifacts, especially on photos with smooth gradients.  
  > For similar visual quality on a portrait photo, WebP was actually 30-39% heavier than JPEG.  
  > WebP is not necessarily better than JPEG for all photographic use cases.

## Week 50, 2023

- [How to Use Responsive HTML Video (...and Audio!)](https://scottjehl.com//posts/using-responsive-video/)
  ```html
  <video>
    <source media="(min-width: 2000px)" src="large.webm" type="video/webm" />
    <source media="(min-width: 2000px)" src="large.mp4" type="video/mp4" />
    <source media="(min-width: 1000px)" src="medium.webm" type="video/webm" />
    <source media="(min-width: 1000px)" src="medium.mp4" type="video/mp4" />
    <source src="small.webm" type="video/webm" />
    <source src="small.mp4" type="video/mp4" />
  </video>
  ```
- [CSS Wrapped: 2023!](https://developer.chrome.com/blog/css-wrapped-2023?hl=en)
- [Why it's essential to excel at the things AI excels at](https://youtube.com/watch?v=mdoMPWSSsqs)
  - Learning areas that AI excels in, like coding, English, design and data, will provide more opportunities as these re fields where AI is commonly utilized.
  - Relying entirely on external support and outsourcing prevents one from developing self-awareness, confidence and resilience to overcome challenges.
  - Gaining expertise in an AI-strong domain allows one to effectively lead AI-assisted innovations and make the most of AI capabilities.
  - Information alone is insufficient - one must make connections between concepts internally through understanding.
  - Insights emerge from linking disparate ideas, which only occurs through internal reflection not external instruction.
  - Wisdom develops from accumulating insights over time through dedicated study.
  - Specializing in an AI field builds an expertise level others rely on, while AI supports less skilled roles.
  - Psychologically, self-learning builds identity, willpower and problem-solving skills.
  - Opportunities arise from innovating where AI supports human strengths, not replacing them.
  - Mastery requires climbing from foundations, so comprehensively studying AI domains leads to leadership.
- [Open Source Software](https://osssoftware.org/) alternatives to popular projects.

## Week 49, 2023

- [Code is run more than read](https://olano.dev/2023-11-30-code-is-run-more-than-read/)
- [Fairphone](https://www.fairphone.com/en/)
- [Data Engineering Design Patterns](https://www.dedp.online/)
- [Kernighan and Pike were right: Do one thing, and do it well](https://medium.com/source-and-buggy/do-one-thing-and-do-it-well-886b11a5d21)
  - Connection analogy - Applets, Unix Programs, Plugins, Microservices
- [The Creative Playground](https://ralphammer.com/dhow-to-get-started/)

## Week 48, 2023

- https://tests.caniuse.com/avif
- [Visual Anagrams: Generating Multi-View Optical Illusions with Diffusion Models](https://dangeng.github.io/visual_anagrams/)
- [Hydration Mismatch](https://vuejs.org/guide/scaling-up/ssr.html#hydration-mismatch)
  - invalid HTML nesting structure
  - randomly generated values
  - The server and the client are in different time zones
- [Travel by Oisin Carroll](https://imois.in/games/travle/) - A daily game – get between countries in as few guesses as possible
- [Preventing Scroll “Bounce” with CSS](https://css-irl.info/preventing-overscroll-bounce-with-css/)
  ```css
  :root {
    overscroll-behavior: none;
  }
  ```
- [How to read a paper](https://dl.acm.org/doi/10.1145/1273445.1273458)
- [Ten simple rules for structuring papers](https://www.biorxiv.org/content/10.1101/088278v5.full.pdf)
- [The `hanging-punctuation` property in CSS](https://chriscoyier.net/2023/11/27/the-hanging-punctuation-property-in-css/)
- [DALL·E Party](https://dalle.party/) - DALL·E ↔ GPT-4 Vision
  - https://dalle.party/?party=vCwYT8Em
- [Sqids formerly Hashids](https://sqids.org/) is an open-source library that lets you generate YouTube-looking IDs from numbers.
- [Shopify live dashboard](https://bfcm.shopify.com)
- [Stripe live dashboard](https://bfcm.stripe.dev)
- [Vue - scoped style leak](https://github.com/vuejs/vue-loader/issues/957#issuecomment-329947476)
- [Build an OTP input field](https://phuoc.ng/collection/html-dom/build-an-otp-input-field/)

## Week 47, 2023

- [An Interactive Guide to CSS Grid](https://www.joshwcomeau.com/css/interactive-guide-to-grid/)
- [Your Website’s URLs Can and Should Be Beautiful](https://opuszine.us/posts/your-websites-urls-can-should-be-beautiful)
- [Realtime planet shader in WebGL](https://github.com/jsulpis/realtime-planet-shader)
- [Charging a lithium battery to 80% only?](https://electronics.stackexchange.com/a/623375)
  > stay within 30%-80%
  - [How to Prolong Lithium-based Batteries](https://batteryuniversity.com/article/bu-808-how-to-prolong-lithium-based-batteries)
- [Former Mozilla exec: Google has sabotaged Firefox for years](https://www.zdnet.com/article/former-mozilla-exec-google-has-sabotaged-firefox-for-years/)
- [YouTube slows down video load times when using Firefox](https://old.reddit.com/r/youtube/comments/17z8hsz/youtube_has_started_to_artificially_slow_down/)
  - [YouTube blames ad blockers for slow load times, and it has nothing to do with your browser](https://www.androidauthority.com/youtube-blames-ad-blockers-slow-load-times-3387523/)
- [screenshot-to-code](https://github.com/abi/screenshot-to-code) converts a screenshot to HTML/Tailwind CSS. It uses GPT-4 Vision to generate the code and DALL-E 3 to generate similar-looking images.
- [URL explained - The Fundamentals](https://ittavern.com/url-explained-the-fundamentals/)

## Week 46, 2023

- [REST, GraphQL or RPC — A Decision Paralysis](https://itnext.io/rest-graphql-or-rpc-a-decision-paralysis-0acaa84b5a27)
- [Clicking `<a>` element using Enter/Space key is not working even though it is focused (accessibility)](https://stackoverflow.com/a/66311677/5163033)
- [Reasons to prefer blake3 over sha256](https://peergos.org/posts/blake3)
  - https://github.com/BLAKE3-team/BLAKE3
- [Locality of Behaviour (LoB)](https://htmx.org/essays/locality-of-behaviour/)
- [HTML First](https://html-first.com/)
  > https://news.ycombinator.com/item?id=38241304
- [Find bilingual baby names](https://mixedname.com/)
- [Design Docs at Google](https://www.industrialempathy.com/posts/design-docs-at-google/)
- [Debugging dynamic content in browser dev tools](https://darekkay.com/blog/debugging-dynamic-content/)

## Week 45, 2023

- [Don't Use Fixed CSS height or width on Buttons, Links, or Any Other Text Containers](https://ashleemboyer.com/blog/don-t-use-fixed-css-height-or-width-on-text-containers)
  > Despite some web design tools specifying CSS `height` values for elements like buttons, setting `height` or `max-height` can actually put you at risk for failing [WCAG 2.2 Success Criterion 1.4.4 Resize Text](https://www.w3.org/TR/WCAG22/#resize-text).
- [Strikethrough Accessibility](https://www.webaxe.org/strikethrough-html-accessibility/)
- [Internet Artifacts](https://neal.fun/internet-artifacts/)
- [The Expressivity Limitations of Object-Oriented Programming](https://two-wrongs.com/expressive-limitations-of-oop.html)
- [Monaspace](https://monaspace.githubnext.com/)
  ```shell
  system_profiler -json SPFontsDataType | grep \"family | sort | uniq # https://stackoverflow.com/a/67132993/5163033
  ```
  Or  
  In Desktop view, Press “⌘ + Space” to start Spotlight, then type in “font book”
- [Webgl Fluid Simulation](https://paveldogreat.github.io/WebGL-Fluid-Simulation/)
- [Don't disable buttons](https://gomakethings.com/dont-disable-buttons/) - it breaks accessibility
  > [`disabled` shouldn't block focus](https://news.ycombinator.com/item?id=38196458)
- [You don’t need to work on hard problems](https://www.benkuhn.net/hard/)
  > In the real world the most important problems are vague and have many evaluation dimensions. Author found it rewarding to optimize for speed, cost and other pragmatic factors rather than just difficulty.
- [Litestream](https://docs.servicestack.net/ormlite/litestream#litestream)
- [Microservices Lessons From Netflix](https://newsletter.systemdesign.one/p/netflix-microservices)

## Week 44, 2023

- [Speeding up the JavaScript ecosystem - Tailwind CSS](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-8/)
- [Tracking SQLite Database Changes in Git](https://garrit.xyz/posts/2023-11-01-tracking-sqlite-database-changes-in-git)
  > [So it does look like git's delta encoding works with sqlite's blocks.](https://news.ycombinator.com/item?id=38117779)
- [Full-Stack Tao: Start With the Domain](https://alexkondov.com/full-stack-tao-start-with-the-domain/)
- [grist-core](https://github.com/gristlabs/grist-core) is the evolution of spreadsheets.
- [Window-swap](https://www.window-swap.com/) – open a new window somewhere in the world
  - https://www.earthcam.com/
- [Critical rendering path](https://developer.mozilla.org/en-US/docs/Web/Performance/Critical_rendering_path)
- [Immanuel Kant—What can we know?](https://ralphammer.com/immanuel-kant-what-can-we-know/)
- [Toxins in chocolate](https://www.asyousow.org/environmental-health/toxic-enforcement/toxic-chocolate#chocolate-tables)
- [SQLite is not without its shortcomings.](https://www.epicweb.dev/why-you-should-probably-be-using-sqlite#weaknesses)
  > https://news.ycombinator.com/item?id=38036921
- [LiteFS - Distributed SQLite](https://fly.io/docs/litefs/)
- [Turso](https://turso.tech/) which uses SQLite under the hood and even has a concept called "embedded replicas" for zero latency reads.
- [How to draw beautiful software architecture diagrams (part 1)](https://terrastruct.com/blog/post/draw-software-architecture-diagrams/)

## Week 43, 2023

- [Kysely](https://github.com/kysely-org/kysely) is a type-safe and autocompletion-friendly typescript SQL query builder.
- [Object-Oriented Programming is Bad](https://www.youtube.com/watch?v=QM1iUe6IofM)
- [I Hate NestJS](https://ethang.dev/blog/i-hate-nest-js/)
  - [starbugs's opinion](https://news.ycombinator.com/item?id=38003433)
- [Radix Vue](https://github.com/radix-vue/radix-vue) - Vue port of Radix UI Primitives. An open-source UI component library for building high-quality, accessible design systems and web apps.
- [I Won't Use Next.js](https://www.epicweb.dev/why-i-wont-use-nextjs) - https://news.ycombinator.com/item?id=38018217
- [Oh-Auth - Abusing OAuth to take over millions of accounts](https://salt.security/blog/oh-auth-abusing-oauth-to-take-over-millions-of-accounts)
  > Not verifying access tokens as required by OAuth specifications allows an attacker to harvest credentials from a malicious site and hijack accounts on other trusted platforms.
- [The Three Cs: 🤝 Concatenate, 🗜️ Compress, 🗳️ Cache](https://csswizardry.com/2023/10/the-three-c-concatenate-compress-cache/)
- [The Pudding](https://pudding.cool/) is a digital publication that is the best internet rabbit hole.
- [Select element: now with horizontal rules](https://developer.chrome.com/en/blog/hr-in-select/)
- [Was Rust Worth It?](https://jsoverson.medium.com/was-rust-worth-it-f43d171fb1b3)
  > While Rust allows creating reliable software, its steep learning curve, rigid structure, and issues with async code can present roadblocks.
- [Openapi Devtools](https://github.com/AndrewWalsh/openapi-devtools) - Effortlessly discover API behaviour with a Chrome extension that automatically generates OpenAPI specifications in real time for any app or website.
- [The OSI Deprogrammer](https://docs.google.com/document/d/1iL0fYmMmariFoSvLd9U5nPVH1uFKC7bvVasUcYq78So/)
- [the actual osi model](https://computer.rip/2021-03-27-the-actual-osi-model.html)
- [Time to move from Node.js Buffer to Uint8Array](https://sindresorhus.com/blog/goodbye-nodejs-buffer)
- [Software disenchantment](https://tonsky.me/blog/disenchantment/)
  - https://news.ycombinator.com/item?id=37987255
- [Base64 Encoding, Explained](https://www.akshaykhot.com/base64-encoding-explained/)
- [Pushing for a lower dev estimate is like negotiating better weather with a meteorologist](https://smartguess.is/blog/your-estimate-is-less-than-that/) discusses how stakeholders often push development teams to provide lower estimates than initially given, without valid reasons for why the effort would decrease.
  - Estimates cannot be pushed lower without new information.
  - With open communication around constraints and tradeoffs, teams can set appropriate expectations and deliver value along the way.
- [Flappy Bird Implemented in Typescript types](https://zackoverflow.dev/writing/flappy-bird-in-type-level-typescript/)
- [Hexagonal Grids](https://www.redblobgames.com/grids/hexagons/) discusses different approaches to representing hexagonal grids in code, including cube, axial, offset, and doubled coordinates.
  - Each system has tradeoffs in terms of simplicity for algorithms and storage.
  - Axial coordinates are recommended for algorithms as they allow basic math operations.
  - Offset coordinates may be better for storage.

## Week 42, 2023

- [useFetch triggers a request on the client side in nested components (using resolveComponent) #20476](https://github.com/nuxt/nuxt/issues/20476)
- [Build a Better Mobile Input](https://better-mobile-inputs.netlify.app/)
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#%3Cinput%3E_types
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inputmode
  - https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete
- [Styling External Links with Attribute Selectors](https://css-irl.info/styling-external-links-with-attribute-selectors/)
  - `a[class~='link']`, `a[href*='css-irl' s]`
- [The Ultimate Low-Quality Image Placeholder Technique](https://csswizardry.com/2023/09/the-ultimate-lqip-lcp-technique/)
- [Fast-Paced Multiplayer (Part IV): Lag Compensation](https://www.gabrielgambetta.com/lag-compensation.html)
- [Fast-Paced Multiplayer (Part III): Entity Interpolation](https://www.gabrielgambetta.com/entity-interpolation.html)
- [How to escape CSS selectors in JavaScript](https://www.stefanjudis.com/today-i-learned/how-to-escape-css-selectors-in-javascript/) - a handy static method in the `CSS` JavaScript namespace to help with this exact problem — [`CSS.escape()`](https://developer.mozilla.org/en-US/docs/Web/API/CSS/escape_static)
- [Fast-Paced Multiplayer (Part II): Client-Side Prediction and Server Reconciliation](https://www.gabrielgambetta.com/client-side-prediction-server-reconciliation.html)
- [Write more "useless" software](https://ntietz.com/blog/write-more-useless-software/) for the joy of computing.
- [Reflect](https://reflect.net/) - High-performance sync for multiplayer web apps
  - [Ready Player Two](https://rocicorp.dev/blog/ready-player-two) - Transactional Conflict Resolution instead of CRDTs
- [PartyKit](https://github.com/partykit/partykit/) simplifies developing multiplayer applications
- [Microfrontends should be your last resort](https://www.breck-mckye.com/blog/2023/05/Microfrontends-should-be-your-last-resort/) argues teams should first refactor their code into isolated domains and minimize dependencies before considering microfrontends.
- [alternative-front-ends](https://github.com/mendel5/alternative-front-ends/) - Overview of alternative open source front-ends for popular internet platforms (e.g. YouTube, Twitter, etc.)
- [Organizing multiple Git identities](https://garrit.xyz/posts/2023-10-13-organizing-multiple-git-identities)
  - [You can also filter based on the remote URL!](https://news.ycombinator.com/item?id=37904125)
- [Populating the page: how browsers work](https://developer.mozilla.org/en-US/docs/Web/Performance/How_browsers_work)
- [One Game, By One Man, On Six Platforms: The Good, The Bad and The Ugly](https://ruoyusun.com/2023/10/12/one-game-six-platforms.html)

## Week 41, 2023

- [A comprehensive guide to the dangers of Regular Expressions in JavaScript](https://www.sonarsource.com/blog/vulnerable-regular-expressions-javascript/) explains how certain regex patterns can cause exponential backtracking on long strings, leading to regular expression denial of service (ReDoS) vulnerabilities. Two real world examples caused major outages at Stack Overflow and CloudFlare due to unintentionally vulnerable regex use.
- [JavaScript Hydration Is a Workaround, Not a Solution](https://thenewstack.io/javascript-hydration-is-a-workaround-not-a-solution/)
  > JavaScript hydration is a technique used to add interactivity to server-rendered HTML pages by attaching event handlers to DOM elements on the client-side.  
  > However, this process requires recovering the necessary information to rebuild the application state and framework state. The document argues that hydration is an overhead because it duplicates the work already done by the server.
  >
  > A better approach called resumability avoids this overhead by serializing and transferring the necessary information from server to client.
  > This allows lazy execution of event handlers on the client-side instead of eagerly executing all components.
- [Angular, Qwik Creator on How JS Frameworks Handle Reactivity](https://thenewstack.io/angular-qwik-creator-on-how-js-frameworks-handle-reactivity/)
  > Three approaches: values, signals, and observables.
  >
  > Angular and React use values and take a coarse-grained approach, re-rendering everything when data changes.  
  > Vue is more fine-grained and will skip re-rendering unchanged components.  
  > Svelte compilers code to be more efficient.  
  > Qwik downloads only the minimal code needed through signals and resumability, making it highly optimized for start-up performance.  
  > Solid uses signals to be the most fine-grained, only executing code initially.
- [Speeding up the JavaScript ecosystem - The barrel file debacle](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-7/)
  > The use of barrel files, which only re-export other files, is very common in large JavaScript projects. However, they can significantly slow down development tasks by forcing the rebuilding of the entire module graph for every file.
- [AI is an Ideology, Not a Technology](https://www.wired.com/story/opinion-ai-is-an-ideology-not-a-technology/) argues that artificial intelligence is better understood as an ideology rather than just a technology. It promotes a view of autonomous machine intelligence that could replace humans, but this is a mirage since AI relies heavily on human data and contributions. An alternative view is to focus on how people are central to developing AI systems through providing examples, problem-solving and understanding the technology.
- [Thread-per-core](https://without.boats/blog/thread-per-core/)
  > The thread-per-core architecture for Rust async programs has been controversial. While it promises better performance and ease of implementation, it may only achieve one, not both. A share-nothing approach keeps data in separate core caches but is complex to implement transactionally.
  >
  > [The debate isn't about thread-per-core work stealing executors, it's whether async/await is a good abstraction for it in Rust. And the more async code I write the more I feel that it's leaky and hard to program against.](https://news.ycombinator.com/item?id=37791635)

## Week 40, 2023

- [Speeding up the JavaScript ecosystem - Polyfills gone rogue](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-6/)
  > Many popular npm packages depend on 6-8x more packages than they need to. Most of these are unnecessary polyfills.
- [Why HTTP/3 is eating the world](https://blog.apnic.net/2023/09/25/why-http-3-is-eating-the-world/)
  > It uses the QUIC protocol, which improves on TCP by more extensively encrypting metadata and enabling faster connection setup. QUIC also enhances performance by eliminating issues like head-of-line blocking and improving network handling. While HTTP/3 was created to work over QUIC, the true innovation was QUIC itself, which updates TCP with security and efficiency improvements. QUIC encryption makes it easier to update features, since middleboxes cannot access metadata. Overall, QUIC and HTTP/3 enhance web performance and security by modernizing core Internet protocols.
- [Meta in Myanmar](https://erinkissane.com/meta-in-myanmar-part-i-the-setup) discusses how hate speech and misinformation spread on Facebook contributed to real-world violence against Rohingya Muslims in Myanmar starting in 2012. Activists had warned Facebook for years about this issue but the company was slow to act.
- [Encrypted Client Hello](https://blog.cloudflare.com/announcing-encrypted-client-hello/)
- [Draggable objects](https://www.redblobgames.com/making-of/draggable/)
- [MMO Architecture: Source of truth, Dataflows, I/O bottlenecks and how to solve them](https://prdeving.wordpress.com/2023/09/29/mmo-architecture-source-of-truth-dataflows-i-o-bottlenecks-and-how-to-solve-them/) discusses architecture challenges for massively multiplayer online (MMO) games. Unlike enterprise systems, the source of truth for an MMO's game world is the in-memory state, not the database, as persisting frequent updates would cause bottlenecks. To address this, the article recommends using a data service with the full state cached in memory.
- [Everything authenticated by Microsoft is tainted.](https://graz.social/@publicvoit/111147782761723981)
- [🚨🚨 That's a lot of YAML 🚨🚨](https://noyaml.com/)
  > [There are a lot of problems in YAML, but I think the main real problem is trying to put logic inside configuration.](https://news.ycombinator.com/item?id=37687365)
- [Live Near Your Friends](https://headlineshq.substack.com/p/issue-no-029-live-near-your-friends) - in distance of 5-minute walk
  - [The Tail End](https://waitbutwhy.com/2015/12/the-tail-end.html)

## Week 39, 2023

- [Google is picking ChatGPT responses from Quora as correct answer](https://twitter.com/8teapi/status/1706520893621784780)
- [Unity's oldest community announces dissolution](https://bostonunitygroup.s3.us-east-1.amazonaws.com/index.html)
- [Ian's Shoelace Site](https://www.fieggen.com/shoelace/)

## Week 38, 2023

- [Understanding NestJS Architecture](https://medium.com/aws-tip/understanding-nestjs-architecture-f257d054211d)
- [View Transitions Break Incremental Rendering](https://ericportis.com/posts/2023/view-transitions-break-incremental-rendering/)
- [🏃‍♂️🏃‍♀️🏃 JS minification benchmarks](https://github.com/privatenumber/minification-benchmarks)
- [Patterns for Reactivity with Modern Vanilla JavaScript](https://frontendmasters.com/blog/vanilla-javascript-reactivity/)
- [Responsive Viewer Chrome extension](https://github.com/skmail/responsive-viewer)
- [Reliably Send an HTTP Request as a User Leaves a Page](https://css-tricks.com/send-an-http-request-on-page-exit/)
- [Get All That Network Activity Under Control with Priority Hints](https://www.macarthur.me/posts/priority-hints)
- [Web Incubator Community Group](https://wicg.io/) (WICG) is a community group of the [World Wide Web Consortium (W3C)](https://www.w3.org/) that incubates new web platform features.
- [A (more) Modern CSS Reset](https://andy-bell.co.uk/a-more-modern-css-reset/)
- [Car allergic to vanilla ice cream](http://www.cs.cmu.edu/~wkw/humour/carproblems.txt)
- [We can't send email more than 500 miles](http://web.mit.edu/jemorris/humor/500-miles)
  - https://news.ycombinator.com/item?id=23777700
- [Svelte 5: Runes](https://svelte.dev/blog/runes)

  > [reactivity and two way data binding creating a spaghetti mess of changes affecting other changes all over the place unless you're really careful is why React was made in the first place](https://news.ycombinator.com/item?id=37584877)

  > [Svelte uses signals as an implementation detail, but in a way that prevents the sorts of headaches you're describing.](https://news.ycombinator.com/item?id=37585078)

  - [MrJohz's opinion among front-end frameworks](https://news.ycombinator.com/item?id=37589355)

- https://v0.dev/
- [OSS Game Engines are increasing their stars on GitHub due to Unity's missteps](https://nitter.net/OSSInsight/status/1703087927763542305)
  - [OSS Game Engine - Ranking](https://ossinsight.io/collections/game-engine/)
- [How Instagram scaled to 14 million users with only 3 engineers](https://instagram-engineering.com/what-powers-instagram-hundreds-of-instances-dozens-of-technologies-adf2e22da2ad)
  - Keep things very simple.
  - Don’t re-invent the wheel.
  - Use proven, solid technologies when possible.
- [My favourite API is a zipfile on the European Central Bank's website](https://csvbase.com/blog/5) - curl, zip, sqlite
- [Akiyoshi's illusion pages](https://www.ritsumei.ac.jp/~akitaoka/index-e.html)

## Week 37, 2023

- [Hacker News Daily Top 10 posts](https://github.com/headllines/hackernews-daily) - You can subscribe by [watching this repo](https://github.com/headllines/hackernews-daily#how-does-it-work) or via [RSS](https://feeds.pub/feed/http%3A%2F%2Frsshub.app%2Fgithub%2Fissue%2Fheadllines%2Fhackernews-daily).
- [How to build a IP geolocation database from scratch?](https://ipapi.is/geolocation.html)
- [ThumbHash](https://github.com/evanw/thumbhash) - A very compact representation of an image placeholder
  - [unpic/placeholder🖼️](https://github.com/ascorbic/unpic-placeholder) is a library for generating low quality image placeholders (LQIP) by extracting the dominant color from image, or by server-side rendering a [BlurHash](https://blurha.sh/) value.
- [Some notes on Local-First Development](https://bricolage.io/some-notes-on-local-first-development/)
  - [cr-sqlite](https://github.com/vlcn-io/cr-sqlite) - Convergent, Replicated, SQLite - "It's like Git, for your data."
- [preload vs prefetch](https://phuoc.ng/collection/this-vs-that/preload-vs-prefetch/)
- [An Internet of PHP](https://timotijhof.net/posts/2023/an-internet-of-php/)

## Week 36, 2023

- [Building a Native Superapp with Micro Frontends and Federated Capacitor](https://ionic.io/blog/building-a-native-superapp-with-micro-frontends-and-federated-capacitor)
- [Making Sense of React Server Components](https://www.joshwcomeau.com/react/server-components/)
- [The small web is beautiful](https://benhoyt.com/writings/the-small-web-is-beautiful/)
- [Turbo 8 is dropping TypeScript](https://world.hey.com/dhh/turbo-8-is-dropping-typescript-70165c01) - https://github.com/hotwired/turbo/pull/971
- [Measuring developer productivity? A response to McKinsey](https://tidyfirst.substack.com/p/measuring-developer-productivity)
- [Javascript labeled statement](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/label)
- [The Worst Programmer I Know](https://dannorth.net/2023/09/02/the-worst-programmer/)
  > Tim wasn’t delivering software; Tim was delivering a team that was delivering software.
- [How To Edit Your Own Lousy Writing](https://stingingfly.org/2017/10/24/edit-lousy-writing/) ([[Vomit Draft|writing.vomit-draft]])
  > The article provides advice on how to improve one's writing through effective editing and revising. It states that first drafts are usually poor but that is normal, as editing is the hidden yet vital second half of writing. By learning to read one's own work as a reader would, an author can better see where the writing fails to effectively convey the intended story. It takes many drafts to transform the ideas in one's head into clear writing that evokes the same experience for others. While the process can feel despairing, persisting through multiple revisions is necessary to craft a story that readers can fully understand and engage with. Effective editing focuses first on major structural issues before minor details.
- [Explaining The Postgres Meme](https://avestura.dev/blog/explaining-the-postgres-meme)
  - [SQL iceberg explained](https://www.youtube.com/watch?v=JZRWkfXNQOk)

## Week 35, 2023

- [Getting all links from any web site into a spreadsheet using browser developer tools](https://christianheilmann.com/2023/08/24/quick-tip-getting-all-links-from-any-web-site-into-a-spreadsheet-using-browser-developer-tools/) - `console.table($$('a'),['innerHTML','href'])`
- [Animated Koots](https://www.animatedknots.com/)
- [Absurd Success](https://www.marginalia.nu/log/87_absurd_success/)
  > The author describes making several improvements to their search engine that significantly increased its performance and scalability. They reworked the URL database to use a single SQLite table instead of large MySQL tables, generating unique IDs during indexing rather than relying on database auto-increment. This reduced RAM usage and allowed indexing to continue while the database was updated. They also changed how the reverse index was constructed, building multiple smaller pre-indexes in memory and then merging them, instead of using a large in-memory lexicon. This avoided writing terabytes of random data to disk and allowed indexing disparate datasets together. Overall these changes halved RAM usage and addressed all known scaling issues, improving the system considerably more than expected.
- [🧠 The Psychology of Design](https://growth.design/psychology) - 106 Cognitive Biases & Principles That Affect Your UX #bookshelf
- [VPN Relationship Map](https://windscribe.com/vpnmap) - Find out who owns your data and see all the shady relationships in the VPN industry.
- [git bisect](https://git-scm.com/docs/git-bisect) - during fix vite plugin error
- [Programming as Theory Building](https://algoritmos-iii.github.io/assets/bibliografia/programming-as-theory-building.pdf)
  - [Theory building and why employee churn is lethal to software companies](https://www.baldurbjarnason.com/2022/theory-building/)
- [As I get older, I just don't care about new technology](https://old.reddit.com/r/webdev/comments/1613yqj/as_i_get_older_i_just_dont_care_about_new/)

## Week 34, 2023

- [PSA: Add dir="auto" to your inputs and textareas.](https://mough.xyz/312/psa-add-dir-auto-to-your-inputs-and-textareas)
- [Server-Side Rendering is a Thiel Truth](https://www.timr.co/server-side-rendering-is-a-thiel-truth/)
- [How architecture diagrams enable better conversations](https://www.unravelled.dev/how-architecture-diagrams-enable-better-conversations/)
  - https://www.workingsoftware.dev/software-architecture-canvas/
  - https://canvas.arc42.org/architecture-communication-canvas
  - https://arc42.org/overview/ - https://arc42.org/download
  - https://softwarearchitecturefordevelopers.com/
- [Understanding the Difference Between : and :: in CSS](https://medium.com/@islizeqiang/understanding-the-difference-between-and-in-css-64c9d36c21af)
  > :: are used to create additional elements within an element
- [Tailwind, and the death of web craftsmanship](https://pdx.su/blog/2023-07-26-tailwind-and-the-death-of-craftsmanship/)
  > While Tailwind may help with initial development speed, it can reduce craftsmanship and make code harder to work with over time.
- [testing your animation refresh rate with css crimes??](https://cohost.org/lunasorcery/post/2465593-testing-your-animati)

## Week 33, 2023

- [Nobody ever paid me for code](https://www.bitecode.dev/p/nobody-ever-paid-me-for-code)
- [When to use "chore" as type of commit message?](https://stackoverflow.com/a/26944812/5163033)
  > "`grunt task`" means nothing that an external user would see:
  >
  > - implementation (of an _existing feature_, which doesn't involve a fix),
  > - configuration (like the `.gitignore` or `.gitattributes`),
  > - private internal methods...

## Week 32, 2023

- [A Blog Post With Every HTML Element](https://www.patrickweaver.net/blog/a-blog-post-with-every-html-element/)
  - `<base>`
- [meta seo inspector](https://www.omiod.com/meta-seo-inspector/) is a Chrome extension useful to inspect in 1 click the meta data usually not visible while browsing

## Week 31, 2023

- [Google AMP – The Newest of Evasive Phishing Tactic](https://cofense.com/blog/google-amp-the-newest-of-evasive-phishing-tactic/)
  > `https://www.google.com/amp/s/${phishing URL}`
- [[Building Software Together|dev.building-software-together]] ch.21~28
- [A non-mathematical introduction to Kalman filters for programmers](https://praveshkoirala.com/2023/06/13/a-non-mathematical-introduction-to-kalman-filters-for-programmers/)
- [Excuse me, is there a problem?](https://longform.asmartbear.com/problem/)
- [Resume and pause animations in CSS](https://www.amitmerchant.com/run-and-pause-animations-in-css/)
  - `animation-play-state` property. - `running` and `paused`
- Software Engineering at Google - ch.16~25
- [CSP Testing Using Cypress](https://glebbahmutov.com/blog/csp-testing-using-cypress/)
- [Splitting the Web](https://ploum.net/2023-08-01-splitting-the-web.html)
- [So, you want to deploy on the edge?](https://zknill.io/posts/edge-database/)
  - [What is Edge?](https://news.ycombinator.com/item?id=36941299)

## Week 30, 2023

- Software Engineering at Google - ch.7~15
  > Code is a liability, not an asset. Code itself doesn’t bring value: it is the functionality that it provides that brings value. That functionality is an asset if it meets a user need: the code that implements this functionality is simply a means to that end.
- [Hono + htmx + Cloudflare is a new stack](https://blog.yusu.ke/hono-htmx-cloudflare/)
- [Testing on the Toilet: Don't Put Logic in Tests](https://testing.googleblog.com/2014/07/testing-on-toilet-dont-put-logic-in.html)
  > Production code computes outputs from inputs while tests specify concrete input/output pairs. Complex test logic should be moved to helper functions with their own tests, leaving test bodies simple.
- [[Browser] Critical Rendering Path 최적화](https://beomy.github.io/tech/browser/critical-rendering-path/#%EB%A6%AC%EC%86%8C%EC%8A%A4-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84-%EC%A7%80%EC%A0%95)
- [[Core Team RFC] New SFC macro: defineModel](https://github.com/vuejs/rfcs/discussions/503)
- [Nanosecond timestamp collisions are common](https://www.evanjones.ca/nanosecond-collisions.html)
  - https://datatracker.ietf.org/doc/html/draft-peabody-dispatch-new-uuid-format

## Week 29, 2023

- Software Engineering at Google - ch.1~6
- [How React 18 Improves Application Performance](https://vercel.com/blog/how-react-18-improves-application-performance)
- [[Browser] 리소스 우선순위 - preload, preconnect, prefetch](https://beomy.github.io/tech/browser/preload-preconnect-prefetch/)
  > `prefetch`를 사용하면 리소스를 미리 캐시 해 두기 때문에 성능이 향상될 것이라고 예상. 하지만 vue-cli3에서 제공하는 prefetch 기능을 사용하면 오히려 첫 렌더링 성능이 저하되는 것으로 확인

## Week 28, 2023

- [JavaScript closest](https://davidwalsh.name/element-closest)
  ```js
  const link = document.querySelector("li a")
  const list = a.closest("ul")
  ```

## Week 27, 2023

- [What does the image decoding attribute actually do?](https://www.tunetheweb.com/blog/what-does-the-image-decoding-attribute-actually-do/)
  > So does this make a difference as an HTML attribute? probably not that much.
- [In Defence of DOMContentLoaded](https://csswizardry.com/2023/07/in-defence-of-domcontentloaded/)
  > The DOMContentLoaded event fires once all of your deferred JavaScript has finished running.
- [The hardest part of building software is not coding, it’s requirements](https://stackoverflow.blog/2023/06/26/the-hardest-part-of-building-software-is-not-coding-its-requirements/) - Why replacing programmers with AI won’t be so easy.

## Week 26, 2023

- [MJML](https://github.com/mjmlio/mjml) - the only framework that makes responsive-email easy
- [SSMPL : A Wishful Thinking HTML Replacement Proposal](https://medium.com/codex/ssmpl-a-wishful-thinking-html-replacement-proposal-1e11e8d86bf6)
- [Slonik](https://github.com/gajus/slonik) - A [battle-tested](https://github.com/gajus/slonik#user-content-battle-tested) Node.js PostgreSQL client with strict types, detailed logging and assertions.
- [Stop using Knex.js](https://gajus.medium.com/stop-using-knex-js-and-earn-30-bf410349856c) - Using SQL query builder is an anti-pattern
  > Knex.js (and other query builders) was designed to be a building block for ORMs; it does not add value when majority of the query is static.  
  > I recommend that you use a query builder for those few queries that need to be generated dynamically, and use raw SQL for everything else. It is not one or the other; the two work together.
- [Is ORM still an 'anti pattern'?](https://github.com/getlago/lago/wiki/Is-ORM-still-an-%27anti-pattern%27%3F)

  > - ["ORMs make the easy parts slightly easier, but they make the hard parts really hard"](https://news.ycombinator.com/item?id=36500429)

  > - Sequelize is extremely simpler and writing code with it is a joy compared to hibernate.
  > - A year ago i had to develop a big Java application without orm (cto’s choice): i didn’t remember how tedious, error prone and slow is development without orm!!! Never do it again!
  > - I think the best approach is to use orm for common crud tasks and add specific sql queries when things get a little bit complicated.
  >   [andretti1977](https://news.ycombinator.com/item?id=36503105)

- [Inverted Triangle Architecture For CSS (ITCSS)](https://apiumhub.com/tech-blog-barcelona/inverted-triangle-architecture-for-css-itcss/)
- [A Complete Guide to CSS Cascade Layers](https://css-tricks.com/css-cascade-layers/)
  > `@layer reset, default, themes, patterns, layouts, components, utilities;`
- [try](https://github.com/binpash/try) lets you run a command and inspect its effects before changing your live system. `try` uses Linux's [namespaces (via `unshare`)](https://docs.kernel.org/userspace-api/unshare.html) and the [overlayfs](https://docs.kernel.org/filesystems/overlayfs.html) union filesystem.

## Week 25, 2023

- [Handles are the better pointers](https://floooh.github.io/2018/06/17/handles-vs-pointers.html)
- [Microsoft Clarity - Free Heatmaps & Session Recordings](https://clarity.microsoft.com/)
- [Modern CSS in Real Life](https://chriscoyier.net/2023/06/06/modern-css-in-real-life/)
  > - `margin-right`: Translated to RTL, spacing problem. use `margin-inline-end` (or `gap`).
  > - `img` alt: With that brief information, perhaps someone might be able to, say, recognize the exact pier in the photo if they had been there before or the like.
  > - higher layer will win, regardless of specificity.
  > - `@import url(~) layer;` - my @import of Bootstrap is plunked onto a layer. Note: we don’t even have to name it, and we can use this keyword instead of @layer while importing. - my super weak CSS selector in which I’m trying to override header margin does win
  > - `@layer reset, default, themes, patterns, layouts, components, utilities;`
- [Software effort estimation is mostly fake research](https://shape-of-code.com/2021/01/17/software-effort-estimation-is-mostly-fake-research/)
  > from [HK news](https://news.ycombinator.com/item?id=36350632)
  >
  > - It's not fake research. It's actually quite an established science in the 24 years I've been doing it.
  > - Take your first guess, double it, double it again if the stakeholder is a poser, add 20% per developer less experience than you, subtract 10% for the features you're going to essentially copy paste, add 15% for sick leave (browsing HN) and then double it for every question you have that are unresolved and divide it by the room temperature multiplied by the amount of people with mechanical keyboards.
  > - That gives you roughly the right estimate for any job, until the next sprint.
- [My Custom CSS Reset](https://www.joshwcomeau.com/css/ccustom-css-reset/)
  - In MacOS Mojave, released in 2018, Apple disabled subpixel antialiasing across the operating system.
  - Confusingly, MacOS browsers like Chrome and Safari still use subpixel antialiasing by default. We need to explicitly turn it off, by setting `-webkit-font-smoothing` to `antialiased`.

## Week 24, 2023

- [Edge sends images you view online to Microsoft, here is how to disable that](https://www.neowin.net/news/edge-sends-images-you-view-online-to-microsoft-here-is-how-to-disable-that/)
- [The Surprising Power of Documentation](https://vadimkravcenko.com/shorts/proper-documentation/)
- [CIA 2010 covert communication websites](https://cirosantilli.com/cia-2010-covert-communication-websites)
- [Effortlessly Support Next Gen Image Formats](https://dennisforbes.ca/articles/jpegxl_just_won_the_image_wars.html)
  - use the `picture` element

## Week 23, 2023

- [Redditor creates working anime QR codes using Stable Diffusion](https://arstechnica.com/information-technology/2023/06/redditor-creates-working-anime-qr-codes-using-stable-diffusion/)
- [Software Engineering at Google](https://abseil.io/resources/swe-book) #bookshelf
- [How to avoid layout shifts caused by web fonts](https://simonhearne.com/2021/layout-shifts-webfonts/)
  - use `font-display: optional` to prevent layout shifts
    - hide text for up to 100ms, then only use the web font if it is available - never swapping
    - If font-display: optional is not possible for your design, use f-mods to reduce the impact of font swaps
  - subset fonts and serve as `woff2`
  - use variable fonts or a limited set of weight variations
  - preload critical fonts
  - host your own fonts on your main domain
- [Aimless.js](https://github.com/ChrisCavs/aimless.js) - The missing JavaScript randomness library.
- [The Rise of the Serverless Monoliths](https://medium.com/@dbottiau/the-rise-of-the-serverless-monoliths-63d3d2d98164)
- [What the heck is the edge anyway?](https://blog.turso.tech/what-the-heck-is-the-edge-anyway-a159a12f2412)
- [libSQL](https://github.com/libsql/libsql) is a fork of SQLite that is both Open Source, and Open Contributions.
- [`display: contents` considered harmful](https://ericwbailey.website/published/display-contents-considered-harmful/)

## Week 22, 2023

- [Webp2jpg-online](https://github.com/renzhezhilu/webp2jpg-online) - image conversion and image stitching, pure front-end implementation, fast speed, privacy protection, and offline use,20 languages supported. [link](https://imagestool.com/webp2jpg-online/)
- [Tidy First? Kent Beck on Refactoring](https://www.infoq.com/presentations/refactoring-cleaning-code/)
  - Software design is an exercise in human relationships between waiters who want new features and changers who want to improve the code structure.
  - Change the structure first. Then change the behavior and it'll be so much easier.
- [Reading Code - Chakra UI](https://alexkondov.com/reading-code-chakra-ui/)
- [Mastering the Art of Efficient JavaScript DOM Manipulation](https://itnext.io/mastering-the-art-of-efficient-javascript-dom-manipulation-899b5cbf5a3f)
  - Use document fragments
  - Use event delegation - `event.target.matches`
- [ls-lint](https://github.com/loeffel-io/ls-lint) - An extremely fast directory and filename linter - Bring some structure to your project filesystem

## Week 21, 2023

- [SST](https://github.com/serverless-stack/sst) makes it easy to build modern full-stack applications on AWS.
  - [Deploying Next.js on the edge with SST — Is SST the game-changer it’s claimed to be?](https://engineering.udacity.com/deploying-next-js-on-the-edge-with-sst-is-sst-the-game-changer-its-claimed-to-be-1f05a0abc27c)
- [Understanding React Concurrency](https://www.bbss.dev/posts/react-concurrency/)
  > The basic premise of React concurrency is to rework the rendering process such that while rendering the next view, the current view is kept responsive.
- [Dealing with cold starts](https://twitter.com/thdxr/status/1661433744970973190)
- [An Ode to React Effects](https://alexkondov.com/an-ode-to-effects/)
  > Most of the problems with `useEffect` are rooted in bad software design, not the hook’s API.
- [Be Careful Using ‘Menu’](https://adrianroselli.com/2023/05/be-careful-using-menu.html)
  - [Stop Using ‘Pop-up’](https://adrianroselli.com/2021/07/stop-using-pop-up.html)
- [11 HTML best practices for login & sign-up forms](https://evilmartians.com/chronicles/html-best-practices-for-login-and-signup-forms)
  - [Don’t Use The Placeholder Attribute](https://www.smashingmagazine.com/2018/06/placeholder-attribute/)
    - Can’t be automatically translated;
    - Is oftentimes used in place of a label, locking out assistive technology;
    - Can hide important information when content is entered;
    - Can be too light-colored to be legible;
    - Has limited styling options;
    - May look like pre-filled information and be skipped over.
- [RIP, Passwords. Here’s What’s Coming Next.](https://www.nytimes.com/wirecutter/blog/what-are-passkeys-and-how-they-can-replace-passwords/)
- [You don't need a modal window](https://youdontneedamodalwindow.dev/)
  - https://marmelab.com/react-admin-demo/#/reviews
- [A primer on functional architecture](https://increment.com/software-architecture/primer-on-functional-architecture/)

  > Just because a business workflow involves an entity, such as an “order,” doesn’t mean it has anything in common with other workflows that use that entity. For example, the “pay for an order” workflow and the “delete an order” workflow both involve orders but have completely different business logic. There’s no need for them both to depend on an arbitrary “order” service that lumps a disparate set of functions together.

  - [The Entity Service Antipattern](https://www.michaelnygard.com/blog/2017/12/the-entity-service-antipattern/)

- [Services By Lifecycle](https://www.michaelnygard.com/blog/2018/01/services-by-lifecycle/)
- [OrmHate](https://martinfowler.com/bliki/OrmHate.html)
  > Essentially the ORM can handle about 80-90% of the mapping problems, but that last chunk always needs careful work by somebody who really understands how a relational database works.  
  > ... A framework that allows me to avoid 80% of that is worthwhile even if it is only 80%.
- [Creating Seamless User Experiences: A Comprehensive Guide to Micro Frontend Architectural Patterns](https://blog.bitsrc.io/creating-seamless-user-experiences-a-comprehensive-guide-to-micro-frontend-architectural-patterns-9118a70386b7)
- [The Guardian Optimizes Mobile Push-Notification Delivery Architecture](https://www.infoq.com/news/2023/05/guardian-push-architecture/)
- [Affinity Photo as a Photoshop replacement for many people.](https://news.ycombinator.com/item?id=35988307)
- https://twitter.com/hobdaydesign/status/1655680006901624839

## Week 20, 2023

- [DevTools Tips](https://devtoolstips.org/) - A collection of useful cross-browser DevTools tips
- [Closing Modals By Pressing the Back Button in Vue.js](https://javascript.plainenglish.io/closing-modals-by-pressing-the-back-button-in-vue-js-568589b4503f)
- [Announcing Vue 3.3](https://blog.vuejs.org/posts/vue-3-3)
  - [defineModel](https://blog.vuejs.org/posts/vue-3-3#definemodel)
  - [Better Getter Support with `toRef` and `toValue`](https://blog.vuejs.org/posts/vue-3-3#better-getter-support-with-toref-and-tovalue)

## Week 19, 2023

- [I'm never investing in Google's smart home ecosystem again](https://www.androidauthority.com/google-smart-home-3319869/)
- [file-type](https://github.com/sindresorhus/file-type) is detected by checking the [magic number](<https://en.wikipedia.org/wiki/Magic_number_(programming)#Magic_numbers_in_files>) of the buffer.
- [HTMX is the Future](https://quii.dev/HTMX_is_the_Future)
  - [When Should You Use Hypermedia?](https://htmx.org/essays/when-to-use-hypermedia/)
- [Prime Video Switched from Serverless to EC2 and ECS to Save Costs](https://www.infoq.com/news/2023/05/prime-ec2-ecs-saves-costs/)
- [On Starting A Side-Project: Hotwire vs. Angular](https://www.bennadel.com/blog/4458-on-starting-a-side-project-hotwire-vs-angular.htm)
- [How to cache node_modules in GitHub Actions with Yarn](https://dev.to/mattpocockuk/how-to-cache-nodemodules-in-github-actions-with-yarn-24eh)
- [24 Powerful HTML Attributes Every Senior Web Engineer Should Master!](https://javascript.plainenglish.io/24-powerful-html-attributes-every-senior-web-engineer-should-master-ad8a4df0776e)
- [The Interactive Guide to Rendering in React](https://ui.dev/why-react-renders)
- [Favour TypeScript Types Over Interfaces](https://www.lloydatkinson.net/posts/2023/favour-typescript-types-over-interfaces/)

## Week 18, 2023

- [changelogen](https://github.com/unjs/changelogen) - 💅 Beautiful Changelogs using Conventional Commits
- [TypeScript Advanced Types for Next.js: Examples and Best Practices In 2023](https://blog.bitsrc.io/typescript-advanced-types-for-next-js-examples-and-best-practices-in-2023-a3a3946a353e)
- [Record Type in TypeScript](https://dmitripavlutin.com/typescript-record/)
- [There’s more than one way to write an IP address](https://ma.ttias.be/theres-more-than-one-way-to-write-an-ip-address/)

## Week 17, 2023

- [What is Source Command in Linux and How Does it Work?](https://linuxhandbook.com/source-command/)
- [Arrow Functions vs Regular Functions in JavaScript – What's the Difference?](https://www.freecodecamp.org/news/the-difference-between-arrow-functions-and-normal-functions/)
- [Pico CSS](https://github.com/picocss/pico) - Minimal CSS Framework for semantic HTML
- [Quickstart for GitHub Packages](https://docs.github.com/en/packages/quickstart)
- [A Completely Non-Technical Explanation of AI and Deep Learning](https://www.parand.com/a-completely-non-technical-explanation-of-ai.html)
- [THE NATURE OF CODE](https://natureofcode.com/book/) #bookshelf
- [How does JWT work? is HS256 the best option?](https://iorilan.medium.com/how-does-jwt-work-is-hs256-the-best-option-6cd9463da7b3) - look EDDSA
- [A 5 years+ tech lead said they shard a database to scale but then he failed to answer this question](https://iorilan.medium.com/a-5-years-tech-lead-said-they-shard-a-database-to-scale-but-then-he-failed-to-answer-this-question-8be39115dcb0)
- [Next.js 13 is not ready for production](https://itsteknas.medium.com/next-js-13-is-not-ready-for-production-a8a8e50fbebf)

## Week 16, 2023

- [Tachyon](https://github.com/weebney/tachyon) is a byte sized script that makes your website feel blazingly fast. It does this by prerendering pages before a user navigates to them, making page transitions virtually instant.
- [90% of My Skills Are Now Worth $0 ...but the other 10% are worth 1000x](https://tidyfirst.substack.com/p/90-of-my-skills-are-now-worth-0)
- [The relative font weight axis — how variable fonts ease font weight transitions](https://www.stefanjudis.com/today-i-learned/the-relative-font-weight-axis-how-variable-fonts-ease-font-weight/)
- [Modern HTML email (tables no longer required)](https://fullystacked.net/posts/modern-html-email/)
- [Can I Email](https://www.caniemail.com/clients/)
- [Introducing the Space Git Flow](https://blog.jetbrains.com/space/2023/04/18/space-git-flow/) - Branching Strategies about Git flow, GitHub flow, Trunk-based development, Space Git Flow
- [Korean as a Concatenative, Stack-Oriented Language](https://m.post.naver.com/viewer/postView.nhn?volumeNo=8912179&memberNo=33582594)
- [Midjourney AI Guide](https://enchanting-trader-463.notion.site/Midjourney-AI-Guide-41eca43809dd4d8fa676e648436fc29c)
- https://docs.midjourney.com/docs/permutations

## Week 15, 2023

- [You Don't Need Another Library to Compose Micro Frontends at Run Time](https://blog.bitsrc.io/you-dont-need-another-library-to-compose-micro-frontends-at-run-time-e803077ade67)
- [EventTarget.dispatchEvent()](https://developer.mozilla.org/ko/docs/Web/API/EventTarget/dispatchEvent)
- [Improving CSS Shapes with Trigonometric Functions](https://danielcwilson.com/posts/css-shapes-with-trig-functions/)
- [Jumping HTML tags. Another reason to validate your markup](https://pepelsbey.dev/articles/jumping-html-tags/)
- [HTMHell](https://www.htmhell.dev/) - A collection of bad practices in HTML, copied from real websites.
- [The 42 Best Pens for 2023: Gel, Ballpoint, Rollerball, and Fountain Pens](https://www.jetpens.com/blog/The-42-Best-Pens-for-2023-Gel-Ballpoint-Rollerball-and-Fountain-Pens/pt/974)
  - [The Difference Between Ballpoint, Gel, and Rollerball Pens](https://www.jetpens.com/blog/The-Difference-Between-Ballpoint-Gel-and-Rollerball-Pens/pt/167)
- [Croner](https://github.com/Hexagon/croner) - Cron for JavaScript and TypeScript
- [Edit Anything by Segment-Anything](https://github.com/sail-sg/EditAnything)
- [50 Ideas That Changed My Life](https://perell.com/essay/50-ideas-that-changed-my-life/)
- [How does database sharding work?](https://planetscale.com/blog/how-does-database-sharding-work)

  > why are you not using a database that does sharding for you?

- [Gource](https://github.com/acaudwell/Gource) is a visualization tool for source control repositories.
- [What happens when you leak AWS credentials and how AWS minimizes the damage](https://xebia.com/blog/what-happens-when-you-leak-aws-credentials-and-how-aws-minimizes-the-damage/)

## Week 14, 2023

- [Improving Web Accessibility with Semantic HTML and Testing Techniques and Tools](https://www.infoq.com/news/2023/04/web-accessibility/)
- [CSS Masking - Ahmad Shadeed](https://ishadeed.com/article/css-masking/)
- [An On-Ramp to Flow](https://census.dev/blog/an-on-ramp-to-flow)
  > Before stepping away, leave the code in a state where it is Obviously Broken, but Easy to Fix.  
  > Applying this technique means thinking about how to exit flow in a way that makes it easy to re-enter.
- [Two-way data binding and reactivity with 15 lines of vanilla JavaScript](https://gomakethings.com/two-way-data-binding-and-reactivity-with-15-lines-of-vanilla-javascript/)
  - Proxy, Event delegate
- [New React docs pretend SPAs don't exist anymore](https://wasp-lang.dev/blog/2023/03/17/new-react-docs-pretend-spas-dont-exist)
  > The strongly recommended way to start a new React project is to use a framework such as Next.js, while the traditional route of using bundlers like Vite or CRA is fairly strongly discouraged.
- [AI won’t steal your job, people leveraging AI will](https://cmte.ieee.org/futuredirections/2023/04/03/ai-wont-steal-your-job-people-leveraging-ai-will/)
- [Saying Goodbye to GitHub](https://ersei.net/en/blog/bye-bye-github)
  - bruce511's [another opinion](https://news.ycombinator.com/item?id=35419257)
- [He who submits a resume has already lost](https://www.residentcontrarian.com/p/he-who-submits-a-resume-has-already)
- [Twitter's Recommendation Algorithm](https://blog.twitter.com/engineering/en_us/topics/open-source/2023/twitter-recommendation-algorithm)
  - https://github.com/twitter/the-algorithm
- [One In Two New Npm Packages Is SEO Spam Right Now](https://blog.sandworm.dev/one-in-two-new-npm-packages-is-seo-spam-right-now)
- [CSS hyphens](https://developer.mozilla.org/en-US/docs/Web/CSS/hyphens)
  - `<wbr>`, `&shy;` - [Two ways to safely break a long word in HTML](https://www.amitmerchant.com/two-ways-to-safely-break-a-long-word-in-html/)

## Week 13, 2023

- [Why You Should Use Bash Over Python](https://dnastacio.medium.com/bash-over-python-39e0eba502f9)
- [SVGOMG](https://jakearchibald.github.io/svgomg/) is **[SVGO](https://github.com/svg/svgo)**'s **M**issing **G**UI, aiming to expose the majority, if not all the configuration options of SVGO.
- [Why Engineers Need To Write](https://www.developing.dev/p/why-engineers-need-to-write)
  > Writing for a child forces me to keep the words and concepts very, very simple, and to write in a style that builds up usage of the program from first principles. Writing for the grumpy old-timer is a practice in minimizing questions from them, forcing me to do a sort of final pass on the overall design of what I'm writing about, to defend design choices, and to add future improvements to the backlog. Drafting the documentation for semi-finished features that are still in progress has sometimes led me to change the design in order to make writing the docs targeting these two people simpler.  
  > — [albrewer](https://news.ycombinator.com/item?id=35307562)

## Week 12, 2023

- [Summarize anything with the Universal Summarizer](https://blog.kagi.com/universal-summarizer)
- [Cheating is All You Need](https://about.sourcegraph.com/blog/cheating-is-all-you-need)

  > Software engineering exists as a discipline because you cannot EVER under any circumstances TRUST CODE.
  >
  > - You get the LLM to draft some code for you that’s 80% complete/correct.
  > - You tweak the last 20% by hand.

  > > Someone is hesitant about 5 times as productive because we only need to "check the code is good" for [two main reasons](https://news.ycombinator.com/item?id=35275438).

- [GitHub Copilot X: The AI-powered developer experience](https://github.blog/2023-03-22-github-copilot-x-the-ai-powered-developer-experience/)
  - [Copilot X](https://github.com/github-copilot/chat_waitlist_signup/)
  - [Copilot Docs](https://githubnext.com/projects/copilot-for-docs/)
  - [Copilot for PRs](https://githubnext.com/projects/copilot-for-pull-requests/)
  - [Copilot CLI](https://githubnext.com/projects/copilot-cli/)
- [Why Tacit Knowledge is More Important Than Deliberate Practice](https://commoncog.com/tacit-knowledge-is-a-real-thing/)
- [MySQL for Developers](https://planetscale.com/courses/mysql-for-developers/introduction/course-introduction) #bookshelf
- [Web fingerprinting is worse than I thought](https://www.bitestring.com/posts/2023-03-19-web-fingerprinting-is-worse-than-I-thought.html)
- [Laying Out a Print Book With CSS](https://iangmcdowell.com/blog/posts/laying-out-a-book-with-css/)
  - https://pagedjs.org/documentation/
  - https://www.print-css.rocks/
  - https://doc.courtbouillon.org/weasyprint/stable/
- [How to Use v-model with Form Inputs in Vue](https://dmitripavlutin.com/vue-v-model-form-inputs/)
- [Category Theory Illustrated](https://abuseofnotation.github.io/category-theory-illustrated/) #bookshelf
- [Steampipe](https://github.com/turbot/steampipe) is the universal interface to APIs. Use SQL to query cloud infrastructure, SaaS, code, logs, and more.
  - https://github.com/turbot/steampipe-plugin-googlesheets
- [libgsqlite](https://github.com/0x6b/libgsqlite) - A SQLite extension which loads a Google Sheet as a virtual table.
- [How A Web Design Goes Straight To Hell](https://theoatmeal.com/comics/design_hell)
- [Transformers.js](https://github.com/xenova/transformers.js) - Run 🤗 Transformers in your browser! We currently support [BERT](https://huggingface.co/docs/transformers/model_doc/bert), [ALBERT](https://huggingface.co/docs/transformers/model_doc/albert), [DistilBERT](https://huggingface.co/docs/transformers/model_doc/distilbert), [T5](https://huggingface.co/docs/transformers/model_doc/t5), [T5v1.1](https://huggingface.co/docs/transformers/model_doc/t5v1.1), [FLAN-T5](https://huggingface.co/docs/transformers/model_doc/flan-t5), [GPT2](https://huggingface.co/docs/transformers/model_doc/gpt2), [BART](https://huggingface.co/docs/transformers/model_doc/bart), [CodeGen](https://huggingface.co/docs/transformers/model_doc/codegen), [Whisper](https://huggingface.co/docs/transformers/model_doc/whisper), [CLIP](https://huggingface.co/docs/transformers/model_doc/clip), [Vision Transformer](https://huggingface.co/docs/transformers/model_doc/vit), and [VisionEncoderDecoder](https://huggingface.co/docs/transformers/model_doc/vision-encoder-decoder) models, for a variety of tasks including: masked language modelling, text classification, text-to-text generation, translation, summarization, question answering, text generation, automatic speech recognition, image classification, zero-shot image classification, and image-to-text.
- [Structured text tools](https://github.com/dbohdan/structured-text-tools) - The following is a list of text-based file formats and command line tools for manipulating each.
- [Understanding lazy load and hydration in nuxt](https://stackoverflow.com/a/70263401/5163033)
  - [It is almost always better to use `v-if` on the component instance.](https://twitter.com/MaOberlehner/status/1353747260434227201)

## Week 11, 2023

- [Master the Art of Caching for System Design Interviews: A Complete Guide](https://levelup.gitconnected.com/master-the-art-of-caching-for-system-design-interviews-a-complete-guide-676bb49d194)
- [Highlights from Git 2.40](https://github.blog/2023-03-13-highlights-from-git-2-40/)
- [Basics of CI/CD Pipeline](https://medium.com/jaanvi/basics-of-ci-cd-pipeline-5762e0eca44e)
  1. Version control
  2. Build
  3. Unit test
  4. Deploy
  5. Auto test
  6. Deploy to production
  7. Measure & validate
- [Managing State In Vue With Pinia ORM](https://blog.openreplay.com/managing-state-in-vue-with-pinia-orm/)

## Week 10, 2023

- [The Best Engineering Blogs](https://draft.dev/learn/engineering-blogs)
- [Everything You Need to Know About the Gap After the List Marker](https://css-tricks.com/everything-you-need-to-know-about-the-gap-after-the-list-marker/)
- [Study finds mushrooms magnify memory by boosting nerve growth](https://medicalxpress.com/news/2023-02-mushrooms-magnify-memory-boosting-nerve.html)
  > I think it should be everyone's primary focus to sleep well, drink water, get outside, get active, and eat generally decently. I hate to say it, but if you're not eating a good amount of vegetables and fruit, decent protein, sleep, etc, no amount of XYZ will catch up to that detriment.
  >
  > — [CE02](https://news.ycombinator.com/item?id=35056071)
- [rallly](https://github.com/lukevella/rallly) - Self-hostable doodle poll alternative. Find the best date for a meeting with your colleagues or friends without the back and forth emails.

## Week 9, 2023

- [All you may need is HTML](https://fabiensanglard.net/html/index.html)
  - [0x10 RULES](https://fabiensanglard.net/ilike/index.html)
- [devalue](https://github.com/Rich-Harris/devalue) - Gets the job done when JSON.stringify can't
- [vite-plugin-federation](https://github.com/originjs/vite-plugin-federation) - Module Federation for vite & rollup
- [js-beautify](https://github.com/beautify-web/js-beautify) - partly deobfuscate scripts
- [Some More On-Scroll Typography Animations](https://tympanus.net/codrops/2023/02/22/some-more-on-scroll-typography-animations/)
- [Why I’m sticking with Vue in 2023](https://medium.com/@lindblomdev/why-im-sticking-with-vue-in-2023-d67bce7bc2f4)
  - Script setup + composition API produce clean code
  - Performance is good
  - Best tooling I have used
- [Resizing with CSS](https://css-irl.info/resizing-with-css/)
- [48 Accessibility Bookmarklets You Can Use For A11Y Testing](https://www.digitala11y.com/accessibility-bookmarklets-testing/)
- [fontaine](https://github.com/danielroe/fontaine) - Automatic font fallback based on font metrics
- [Firecracker internals: a deep dive inside the technology powering AWS Lambda](https://www.talhoffman.com/2021/07/18/firecracker-internals/)
  - https://github1s.com/firecracker-microvm/firecracker
- [Improve Your VSCode Workflow to the Max](https://www.builder.io/blog/vscode-tips)
  - [GitHub Copilot Labs](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-labs)
- [jose](https://github.com/panva/jose) - "JSON Web Almost Everything" - JWA, JWS, JWE, JWT, JWK, JWKS for Node.js, Browser, Cloudflare Workers, Deno, Bun, and other Web-interoperable runtimes.
- [Easy implemented dark mode](https://twitter.com/flaviocopes/status/1627609246014619649)
- [What to Expect from Vue in 2023 and How it Differs from React](https://thenewstack.io/vue-2023/)
- [The Unreasonable Effectiveness of Conditional Probabilities](https://two-wrongs.com/unreasonable-effectiveness-of-conditional-probabilities.html)
  - https://news.ycombinator.com/item?id=34900823
- [Debugging Node.js, The Right Way](https://www.builder.io/blog/debug-nodejs)
  ```shell
  node server.js --inspect-brk
  ```
  - [chrome dev tools](https://cdn.builder.io/api/v1/image/assets%252FYJIGb4i01jvw0SRdL5Bt%252Ff5dd633650214ff28d620d233299329b?format=webp&width=2000)

## Week 8, 2023

- [test && commit || revert](https://medium.com/@kentbeck_7670/test-commit-revert-870bbd756864)
- [Limbo: Scaling Software Collaboration](https://medium.com/@kentbeck_7670/limbo-scaling-software-collaboration-afd4f00db4b)
  > Sort commits into “couldn’t possibly cause problems” (you’ll be mostly right) and “might cause problems”. Treat them differently. Rearrange your workflow so you have mostly “couldn’t possibly cause problems” commits.
- [My class required AI. Here's what I've learned so far.](https://oneusefulthing.substack.com/p/my-class-required-ai-heres-what-ive)
- [`a = 0-x` is about 3-10x faster than `a = -x`](https://twitter.com/mhevery/status/1626259524930932745)
- [How to Favicon in 2023: Six files that fit most needs](https://evilmartians.com/chronicles/how-to-favicon-in-2021-six-files-that-fit-most-needs/)
- [Important SEO-Related HTML Tags, And How To Optimize Them](https://blog.openreplay.com/important-seo-related-tags-in-html-and-how-to-optimize-them/)
- https://pointerpointer.com/
- [How to Inspect Interactions in the Browser](https://www.builder.io/blog/inspect-interactions-in-the-browser)
- [I love building a startup in Rust. I wouldn't pick it again.](https://www.propelauth.com/post/i-love-building-a-startup-in-rust-i-wouldnt-pick-it-again)
  > If you're thinking about building something in Rust, a good question to ask is, "what would I use if Rust didn't exist?" If your answer is something like Go or Node.js, then Rust is probably not the right choice. If your answer is C or C++ or something similar, then Rust is very likely the right choice.
  > [zeroxfe](https://news.ycombinator.com/item?id=34836164)
- [Writing Javascript without a build system](https://jvns.ca/blog/2023/02/16/writing-javascript-without-a-build-system/)
  - For me, a complicated Javascript build system just doesn’t seem worth it for small 500-line projects
  - [if I want a build system, use esbuild](https://jvns.ca/blog/2021/11/15/esbuild-vue/)
- [CSS Named Colors: Groups, Palettes, Facts, & Fun](https://austingil.com/css-named-colors/)

## Week 7, 2023

- [Electric Clojure](https://github.com/hyperfiddle/electric) – a signals DSL for fullstack web UI, with compiler-managed network sync
  - https://news.ycombinator.com/item?id=34771771
- [Just 4 pages a day. It really adds up.](https://news.ycombinator.com/item?id=34779980)
- [Comparing the Top Eight Managed Kubernetes Providers](https://medium.com/@elliotgraebert/comparing-the-top-eight-managed-kubernetes-providers-2ae39662391b)
  - Best overall: Azure
  - Best for startups: Linode
  - Best for cost: OVHCloud
- [SQLite the only database you will ever need in most cases](https://www.unixsheikh.com/articles/sqlite-the-only-database-you-will-ever-need-in-most-cases.html)
  - https://news.ycombinator.com/item?id=34813140
- [Squares in Squares](https://erich-friedman.github.io/packing/squinsqu/)
- [What's up with monomorphism?](https://mrale.ph/blog/2015/01/11/whats-up-with-monomorphism.html)
- [Rethinking the Modern Web](https://dev.to/oxharris/rethinking-the-modern-web-5cn1)
- [Use Maps More and Objects Less](https://www.builder.io/blog/maps)
- [React Server Components vs. Server-Side Rendering](https://www.thearmchaircritic.org/mansplainings/react-server-components-vs-server-side-rendering)
  - https://beta.nextjs.org/docs/rendering/fundamentals
- [Type vs Interface in TypeScript](https://blog.bitsrc.io/type-vs-interface-in-typescript-cf3c00bc04ae)
- [Unpacking API Management policies [Part 2]: 5 ways to handle REST API authentication](https://cloud.google.com/blog/products/api-management/5-ways-to-implement-rest-api-authentication/?hl=en)
- [useSignal() is the future of web frameworks and is a better abstraction than useState(), which is showing its age.](https://javascriptweekly.com/link/135369/web)
- [Using Notion as a Headless CMS with Nuxt](https://dev.to/trentbrew/using-notion-as-a-headless-cms-with-nuxt-3mk)
- [Speeding up the JavaScript ecosystem - eslint](https://marvinh.dev/blog/speeding-up-javascript-ecosystem-part-3/)
- [Why Create React App exists](https://github.com/reactjs/reactjs.org/pull/5487#issuecomment-1409720741)
- [Discover the Magic of Portals: A Beginner’s Guide to React’s Most Powerful Tool](https://blog.bitsrc.io/discover-the-magic-of-portals-a-beginners-guide-to-react-s-most-powerful-tool-f6f1965ea305)
  - Portals allow you to render components outside of their parent component’s tree.
  - When should you use portals?
    - Modals and dialogs
    - Tooltips and popovers
    - Overlaying content
- [Environment Variables in JavaScript: process.env](https://dmitripavlutin.com/environment-variables-javascript/)
- [The Guide To Responsive Design In 2023 and Beyond](https://ishadeed.com/article/responsive-design/)
- [A HISTORICAL REFERENCE OF REACT CRITICISM](https://www.zachleat.com/web/react-criticism/)
- [OrgChart](https://github.com/dabeng/OrgChart) - It's a simple and direct organization chart plugin. Anytime you want a tree-like chart, you can turn to OrgChart.
- [Optimal Images in HTML](https://www.builder.io/blog/fast-images)
- [I made ChatGPT and Bing AI have a conversation (and they are friends now)](https://moritz.pm/posts/chatgpt-bing)
- [Five Tips For a Healthier Postgres Database in the New Year](https://www.crunchydata.com/blog/five-tips-for-a-healthier-postgres-database-in-the-new-year)
- [How to Search Files Effectively in the Linux Terminal](https://www.freecodecamp.org/news/how-to-search-files-in-the-linux-terminal/)
- Ask HN: What Happened to Elm?
  - [In version 0.19, the core team hardcoded a whitelist into the compiler of which projects are allowed to use native code (which happened to basically be the core team's pet projects). This basically crippled the language beyond usability for everyone else.](https://news.ycombinator.com/item?id=34746350)

## Week 6, 2023

- [Image Compression with Singular Value Decomposition](https://timbaumann.info/svd-image-compression-demo/)
- [A Better Way to Work With Number and Date Inputs in JavaScript](https://www.builder.io/blog/numbers-and-dates)
  - valueAsNumber, valueAsDate
- [Three attributes for better web forms](https://adactio.com/journal/19842)
  - inputmode, enterkeyhint, and autocomplete.
- [Understand the Lexical Scoping in JavaScript](https://javascript.plainenglish.io/understand-the-lexical-scoping-in-javascript-6b85ca94b565)
- [JavaScript Require – How to Use the require() Function in JS](https://www.freecodecamp.org/news/how-to-use-the-javascript-require-function/)
- [When You Should Prefer Map Over Object In JavaScript](https://www.zhenghao.io/posts/object-vs-map)
- [The new Wikipedia appearance that took the whole village](https://medium.com/@dlyall/the-new-wikipedia-appearance-that-took-a-whole-village-52637b34a00f)
  - [Vue.js has been selected as Wikimedia Foundation's future JavaScript framework](https://lists.wikimedia.org/hyperkitty/list/wikitech-l@lists.wikimedia.org/thread/SOZREBYR36PUNFZXMIUBVAIOQI4N7PDU/)
  - [RFC: Adopt a modern JavaScript framework for use with MediaWiki](https://phabricator.wikimedia.org/T241180) and [EvanYou comment](https://phabricator.wikimedia.org/T241180#:~:text=Project%20lead%20of%20Vue.js%20here.)
- [The Intermediate Plateau: What Causes It? How Can We Move Beyond It?](https://www.scotthyoung.com/blog/2023/01/03/intermediate-plateau/)
- [codeium](https://www.codeium.com/) - Free AI-powered code completion for everyone, everywhere
- [Windows 11: a spyware machine out of users' control?](https://www.techspot.com/news/97535-windows-11-spyware-machine-out-users-control.html)
- [sqlc](https://github.com/kyleconroy/sqlc) - A SQL Compiler
- [Use GPT-3 incorrectly: reduce costs 40x and increase speed by 5x](https://www.buildt.ai/blog/incorrectusage)
  - To reduce costs and increase speed, they developed a technique to generate a moderately sized corpus of completions made by a larger model, and fine-tune a smaller model to do the same task. This can reduce costs by 40x and increase speed by 5x. This is an interesting approach to using GPT-3 to reduce costs and increase speed, and could be useful for other applications.
  - [Knowledge distillation](https://en.m.wikipedia.org/wiki/Knowledge_distillation)
- [Increment Selection - vs code extension](https://marketplace.visualstudio.com/items?itemName=albymor.increment-selection)
- [Screw motivation, what you need is discipline.](https://www.wisdomination.com/screw-motivation-what-you-need-is-discipline/)
- [Visual design rules you can safely follow every time](https://anthonyhobday.com/sideprojects/saferules/)
  - https://news.ycombinator.com/item?id=34684761
- [Optimal program design 2.0](https://mennohenselmans.com/optimal-program-design/)
- [`<vue-clamp>`](https://github.com/Justineo/vue-clamp) - Clamping multiline text with ease.
- [Comparing Manual and Free Automated WCAG Reviews](https://adrianroselli.com/2023/01/comparing-manual-and-free-automated-wcag-reviews.html)
- [Introduction to Linux Server Administration!](https://github.com/livialima/linuxupskillchallenge)
  - https://theleo.zone/posts/linux-upskill/
- [deadfile](https://github.com/M-Izadmehr/deadfile) - Simple util to find deadcode and unused files in any JavaScript project (ES5, ES6, React, Vue, ...).

## Week 5, 2023

- [History of Lisp Parentheses](https://github.com/shaunlebron/history-of-lisp-parens)
- [JavaScript Closure: A Simple Explanation](https://dmitripavlutin.com/javascript-closure/)
- [10 Web Development Trends in 2023](https://www.robinwieruch.de/web-development-trends/)
- [5 Must-Know Differences Between ref() and reactive() in Vue](https://dmitripavlutin.com/ref-reactive-differences-vue/)
- [International domain names: where does https://meßagefactory.ca lead you?](https://lemire.me/blog/2023/01/23/international-domain-names-where-does-https-mesagefactory-ca-lead-you/) - The result depends on your browser.
- [Two ways to safely break a long word in HTML](https://www.amitmerchant.com/two-ways-to-safely-break-a-long-word-in-html/)
  - `<wbr>`
  - `&shy;`
- [Demystifying Fresh — Build Your own Islands of Interactivity](https://blog.bitsrc.io/demystifying-fresh-building-your-own-islands-of-interactivity-4b774cc30393)
- [Netlify lost my trust](https://news.ycombinator.com/item?id=34614533) and replies
- [Virtual DOM is pure overhead](https://svelte.dev/blog/virtual-dom-is-pure-overhead)
  - [comment by former React core team member Pete Hunt](https://news.ycombinator.com/item?id=34615578) and replies
- [When Discord is open in the background, NVIDIA card will not reach full speed](https://nvidia.custhelp.com/app/answers/detail/a_id/5443/~/when-discord-is-open-in-the-background%2C-graphics-card-memory-clocks-will-not)
  - https://news.ycombinator.com/item?id=34615351
- [Trigger.dev](https://github.com/triggerdotdev/trigger.dev) is an open-source platform that makes it easy for developers to create event-driven background tasks directly in their code.
  - https://pipedream.com/
  - https://temporal.io/
  - https://github.com/windmill-labs/windmill
- [Weeklong improved colour contrasts sensitivity after single 670 nm exposures associated with enhanced mitochondrial function](https://www.nature.com/articles/s41598-021-02311-1)
  - https://news.ycombinator.com/item?id=34611077
- [MySQL vs PostgreSQL in 2023.](https://dbconvert.com/blog/mysql-vs-postgresql/)
- [Understanding Authentication In Websites: A Banking Analogy](https://www.smashingmagazine.com/2023/01/authentication-websites-banking-analogy/)
- [Carbonyl](https://github.com/fathyb/carbonyl) is a Chromium based browser built to run in a terminal. [Read the blog post](https://fathy.fr/carbonyl).
- [Ask HN: What would be your stack if you are building an MVP today?](https://news.ycombinator.com/item?id=34530052)
- [What we look for in a resume](https://huyenchip.com/2023/01/24/what-we-look-for-in-a-candidate.html)
- [LastPass breach gets worse](https://old.reddit.com/r/sysadmin/comments/10kp4ye/lastpass_breach_gets_worse/)
- [IPinside: Korea’s mandatory spyware](https://palant.info/2023/01/25/ipinside-koreas-mandatory-spyware/)
  - [South Korea’s online security dead end](https://palant.info/2023/01/02/south-koreas-online-security-dead-end/)
  - [TouchEn nxKey: The keylogging anti-keylogger solution](https://palant.info/2023/01/09/touchen-nxkey-the-keylogging-anti-keylogger-solution/)
- [Bitwarden design flaw: Server side iterations](https://palant.info/2023/01/23/bitwarden-design-flaw-server-side-iterations/)
- [The Ultimate Guide To Software Architecture Documentation](https://www.workingsoftware.dev/software-architecture-documentation-the-ultimate-guide/)
  - https://arc42.org/download
- [Why React isn't dying](https://tkdodo.eu/blog/why-react-isnt-dying)

## Week 4, 2023

- [Transducers: Efficient Data Processing Pipelines in JavaScript](https://medium.com/javascript-scene/transducers-efficient-data-processing-pipelines-in-javascript-7985330fe73d)
- [The Page With No Code](https://danq.me/2023/01/11/nocode/)
  - https://no-ht.ml/
- [Techniques to improve reliability](https://github.com/openai/openai-cookbook/blob/main/techniques_to_improve_reliability.md)
  > Applying this simple trick to the MultiArith math dataset, the authors found `Let's think step by step` quadrupled the accuracy, from 18% to 79%!
- [Interview Questions to ask as a candidate](https://docs.google.com/spreadsheets/d/11DoQ-Bhvs5mfRwB0Bz6OHwoChhFVK7u_KqlbFgR-ezY/)
- [Topcat's System Design Template](https://leetcode.com/discuss/career/229177/My-System-Design-Template)
- [Unable to make a single bit of progress, my goto strategy is similar to what writers call a vomit draft.](https://news.ycombinator.com/item?id=34449984)
- [Git-Sim: Visually Simulate Git Operations In Your Own Repos](https://initialcommit.com/blog/git-sim)
  - https://github.com/initialcommit-com/git-sim
- [Function Composition in Large React Applications: Best Practices and Real-World Examples](https://medium.com/@rivoltafilippo/function-composition-in-large-react-applications-best-practices-and-real-world-examples-805aba8d37b1)

## Week 3, 2023

- [5 Mistakes to Avoid When Self Hosting a Website from Home](https://noted.lol/5-mistakes-to-avoid-when-self-hosting-from-home/)
- [Nerd Fonts](https://github.com/ryanoasis/nerd-fonts) is a project that patches developer targeted fonts with a high number of glyphs (icons). Specifically to add a high number of extra glyphs from popular 'iconic fonts' such as [Font Awesome](https://github.com/FortAwesome/Font-Awesome), [Devicons](https://vorillaz.github.io/devicons/), [Octicons](https://github.com/primer/octicons), and [others](https://github.com/ryanoasis/nerd-fonts#glyph-sets).
- [ai-collection](https://github.com/ai-collection/ai-collection) - A List of Awesome Generative AI Applications
- [1000+ Free Developer Certifications](https://www.freecodecamp.org/news/free-certificates/)
- [Design Doping: My Obsession with AI as the Ultimate Brainstorming Partner](https://medium.com/geekculture/design-doping-my-obsession-with-ai-as-the-ultimate-brainstorming-partner-2ff28de2e34b)
- [Every Software Developer should write a blog](https://dev.to/nasirovelchin/every-software-developer-should-write-a-blog-4622)
- [API Management in Nuxt 3 with TypeScript](https://www.vuemastery.com/blog/api-management-in-nuxt-3-with-typescript)
- [10 Advanced TypeScript Tips for Development](https://levelup.gitconnected.com/10-advanced-typescript-tips-for-development-2666298d50f)
- [Evergreen notes](https://notes.andymatuschak.org/Evergreen_notes)
- [How to draw ideas](https://ralphammer.com/how-to-draw-ideas/)
  - [A quick beginner’s guide to drawing](https://ralphammer.com/a-quick-beginners-guide-to-drawing/)
- [Make me think!](https://ralphammer.com/make-me-think/)
  - ![Users with complexity](assets/images/ux/makemethink_3.gif) ![From complicated to simple](assets/images/ux/makemethink_4.gif)
  - ![From simple to too simple](assets/images/ux/makemethink_6.gif)
- [sysend](https://github.com/jcubic/sysend.js) - Web application synchronization between different tabs
- [Static HTML comments](https://sive.rs/shc)

## Week 2, 2023

- [How to Destructure Props in Vue (Composition API)](https://dmitripavlutin.com/props-destructure-vue-composition/)
- [Type-safe React Query](https://tkdodo.eu/blog/type-safe-react-query)
- [C4-PlantUML](https://github.com/plantuml-stdlib/C4-PlantUML) combines the benefits of [PlantUML](https://plantuml.com/) and the [C4 model](https://c4model.com/) for providing a simple way of describing and communicate software architectures.
- [VS Code Shortcuts To Code Like You’re Playing a Piano](https://betterprogramming.pub/vs-code-shortcuts-to-code-like-youre-playing-a-piano-e5db7b272d1)
- [recommended routine - bodyweightfitness](https://www.reddit.com/r/bodyweightfitness/wiki/kb/recommended_routine/)
  - [MuscleWiki](https://musclewiki.com/) - Find exercises that work specific muscles
- [OWASP Cheat Sheet Series](https://cheatsheetseries.owasp.org/) #bookmark
  - https://owasp.org/sitemap/ - Key Projects
- [2022 JavaScript Rising Stars](https://risingstars.js.org/2022/en)
- 🤖 [just](https://github.com/casey/just) is a handy way to save and run project-specific commands.
- [Introduction to Statistical Lebarning](https://www.statlearning.com/)
- [Do-nothing scripting: the key to gradual automation](https://blog.danslimmon.com/2019/07/15/do-nothing-scripting-the-key-to-gradual-automation/)
- [Extreme questions to trigger new, better ideas](https://longform.asmartbear.com/posts/extreme-questions/)
  - 10x prices, No customers, No tech support, ...
- https://github.com/search?o=desc&q=stars%3A%3E100000&s=stars&type=Repositories
- https://github.com/sindresorhus/awesome - 😎 Awesome lists about all kinds of interesting topics
- [roadmap.sh](https://roadmap.sh/) - Community driven roadmaps, articles and resources for developers
- [fish](https://fishshell.com/) - the friendly interactive shell
- [Testing Without Mocks: A Pattern Language](https://www.jamesshore.com/v2/projects/testing-without-mocks/testing-without-mocks) #bookmark
  - https://news.ycombinator.com/item?id=34293631

## Week 1, 2023

- [Component Party](https://component-party.dev/) - Web component JS frameworks overview by their syntax and features: Svelte, React, Vue 2, Vue 3, Angular, SolidJS, Lit, Ember, Alpine, Qwik
  - I like Alpine mostly. But what about component.
- [React Wrap Balancer](https://react-wrap-balancer.vercel.app/) is a simple React Component that makes your titles more readable in different viewport sizes.
- [Lesser-Known And Underused CSS Features In 2022](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/)
  - [currentColor](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#currentcolor)
  - [Counters](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#counters)
  - [scroll-padding](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#scroll-padding)
  - [Font Rendering Options](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#font-rendering-options)
  - [Creating Stacking Context with `isolate`](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#creating-stacking-context-with-isolate)
  - [Render Performance Optimization](https://www.smashingmagazine.com/2022/05/lesser-known-underused-css-features-2022/#render-performance-optimization)
- [Reduce WSL2 Disk Usage](https://blakey.co/blog/reduce-wsl2-disk-usage)
- [DuckDB](https://duckdb.org/why_duckdb) is an in-process SQL OLAP Database Management System [— What’s the Hype About?](https://betterprogramming.pub/duckdb-whats-the-hype-about-5d46aaa73196)
  - Processing and storing tabular datasets, e.g. from CSV or Parquet files
  - Interactive data analysis, e.g. Joining & aggregate multiple large tables
  - Concurrent large changes, to multiple large tables, e.g. appending rows, adding/removing/updating columns
  - Large result set transfer to client
- [Flying away from AWS](https://terrateam.io/blog/flying-away-from-aws)
  - https://news.ycombinator.com/item?id=34238150
- [Deploying CSS Logical Properties On Web Apps](https://www.smashingmagazine.com/2022/12/deploying-css-logical-properties-on-web-apps/)
  ```css
  margin-inline: auto;
  margin-block: 0;
  inset: 0;
  inset-inline: 10%;
  ```
- [By default, the aws sync command does not delete files.](https://stackoverflow.com/a/30638955/5163033)
- [Web Hackers vs. The Auto Industry: Critical Vulnerabilities in Ferrari, BMW, Rolls Royce, Porsche, and More](https://samcurry.net/web-hackers-vs-the-auto-industry/)
- [HN: Modules, not microservices](https://news.ycombinator.com/item?id=34230641)
  > - I just want to point out that for the second problem (scalability of CPU/memory/io), microservices almost always make things worse.
  > - I was working at Amazon when they started transitioning from monolith to microservices, and the big win there was locality of data and caching.
  > - Microservices are less _efficient_, but are still more _scalable_.
  > - I am working on a project that uses a microservice architecture to make the individual components scalable and separate the concerns. However one of the unexpected consequences is that we are now doing a lot of network calls between these microservices, and this has actually become the main speed bottleneck for our program, especially since some of these services are not even in the same data center. We are now attempting to solve this with caches and doing batch requests, but all of this created additional overhead that could have all been avoided by not using microservices.
- [HyperUI](https://github.com/markmead/hyperui) is a large collection of free Tailwind CSS components for marketing, ecommerce and application UI 🐳
- Free UI faces for designers, avatars, dummy faces, AI generated people faces | [Lorem Faces](https://loremfaces.com/)
- [HTTP Status Dogs](https://httpstatusdogs.com/) - Hypertext Transfer Protocol Response status codes. And dogs.
- [Optimizing images for mobile browsers with a UX mindset](https://blog.logrocket.com/ux-design/optimizing-images-mobile-browsers-ux-mindset/)
  - Formats for the win
  - Load responsively - With the HTML [`<picture> element`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture), we can load the image in the right size and format, no matter the device. It ensures the best image-loading experience every time, taking into account a device’s DPR automatically.
- [Books for Software Engineers in 2023](https://grantisom.com/2023/01/02/mustread-books-for.html)
  - https://news.ycombinator.com/item?id=34225417
- [Mafs](https://github.com/stevenpetryk/mafs) is a set of opinionated React components for creating math visualizations.
- [Ask HN: Why did Frontend development explode in complexity?](https://news.ycombinator.com/item?id=34218003)
- [Functional Programming - How and Why](https://onsclom.bearblog.dev/functional-programming-how-and-why/)
- [What is my viewport](https://whatismyviewport.com/) - A simple online tool for quickly finding the dimensions of your current device's viewport!
- [Top 5 Web APIs for performance-based analysis (and how to use them)](https://blog.logrocket.com/top-5-web-apis-performance-based-analysis/)
- [Making the Web Faster with Service Workers and Performance Research](https://calendar.perfplanet.com/2022/making-the-web-faster-with-service-workers-and-performance-research/)
  - Cache dynamic website resources like HTML and APIs which can be plugged into websites via Service Workers
    - automatically dealing with personalization in HTML
    - keeping caches up-to-date by crowdsourcing cache checks
    - caching dynamic resources in the complete web cache hierarchy including browser cache through Bloom filter-based cache coherence algorithms
- [4 minutes run hard enough to push heart rate to 90%, 3 minutes recover, repeat 4 times](https://news.ycombinator.com/item?id=34213181)
  - https://www.ntnu.edu/cerg/advice
  - [Get running with Couch to 5K](https://www.nhs.uk/live-well/exercise/running-and-aerobic-exercises/get-running-with-couch-to-5k/)
- [HTTP/3 Prioritization Demystified](https://calendar.perfplanet.com/2022/http-3-prioritization-demystified/)
  - https://news.ycombinator.com/item?id=34231934
- [2022 Roundup of Web Research](https://css-tricks.com/2022-roundup-of-web-research/)
- [7 Unnecessarvy VSCode Extensions You Should Uninstall Now](https://codingbeautydev.com/blog/unnecessary-vscode-extensions/)
- [Top 7 tips/features in Vue 3](https://medium.com/@felixdavid12/top-7-tips-features-in-vue-3-7119cee4a918) 3. Reactive CSS
- The global **`structuredClone()`** method creates a [deep clone](https://developer.mozilla.org/en-US/docs/Glossary/Deep_copy) of a given value using the [structured clone algorithm](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API/Structured_clone_algorithm).
- [12 CSS Tricks You Might Not Know](https://medium.com/@pythonlearn1024/12-css-tricks-you-might-not-know-3054475e861e)
