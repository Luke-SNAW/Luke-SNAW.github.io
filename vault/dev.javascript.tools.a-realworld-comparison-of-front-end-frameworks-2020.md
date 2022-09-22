---
id: 7mfj1k5i7pl532a9ue79q4i
title: A Realworld Comparison of Front End Frameworks 2020
desc: ""
updated: 1663733174843
created: 1663732748940
---

> https://medium.com/dailyjs/a-realworld-comparison-of-front-end-frameworks-2020-4e50655fe4c1

We are doing it again. This is 2020, there is also [2019](https://medium.com/free-code-camp/a-realworld-comparison-of-front-end-frameworks-with-benchmarks-2019-update-4be0d3c78075), [2018](https://medium.com/free-code-camp/a-real-world-comparison-of-front-end-frameworks-with-benchmarks-2018-update-e5760fb4a962), and [2017](https://medium.com/free-code-camp/a-real-world-comparison-of-front-end-frameworks-with-benchmarks-e1cb62fd526c).

**Let me start with this — this is by all means not a comparison of what should be your next choice for Front-End. It’s a small, relatively unsophisticated, comparison of three things: Performance, Size, and Lines of Code of pretty similar application.**

With that in mind here is how it works:

**We are comparing RealWorld App —** something more than a “to do” app. Usually “to-dos” don’t convey enough knowledge and perspective to actually build real applications.

**It is somehow standardized —** A project that conforms to certain rules — [there is a spec](https://github.com/gothinkster/realworld/tree/master/spec). Provides a back-end API, static markup, and styles.

**Written or reviewed by an expert —** A consistent, real-world project that, ideally, an expert in that technology would have built or reviewed.

# Which libraries/frameworks are we comparing?

As of the writing, there are 24 implementations of Conduit at the [RealWorld repo](https://github.com/gothinkster/realworld). It doesn’t matter if it has a big following or not. The only qualification is — it appears on the [RealWorld repo](https://github.com/gothinkster/realworld) page.

# What metrics do we look at?

**Performance** — how long does this App take to show content and become usable?

**Size** —how big is the App? We will only compare the size of the compiled JavaScript file(s). HTML and CSS are common to all variants and are downloaded from a CDN (Content Delivery Network). All technologies compile or transpile to JavaScript, thus we only size this file(s).

**Lines of Code** — how many lines of code did the author need to create the RealWorld app based on spec? To be fair some apps have a bit more bells and whistles, but it should not have a significant impact. The only folder we quantify is `src/` in each app. Doesn’t matter if it was auto generated or not — you still need to maintain it.

# Metric #1: Performance

We’ll check the Performance score from [Lighthouse Audit](https://developers.google.com/web/tools/lighthouse/) that ships with Chrome. Lighthouse returns a Performance score between 0 and 100. 0 is the lowest possible score. For more details check [Lighthouse Scoring Guide](https://developers.google.com/web/tools/lighthouse/v3/scoring).

## Audit Settings

![](https://miro.medium.com/max/1400/1*0B_8wqM-vS597MOtGaDWvQ.png)

Lighthouse Audit Settings for all tested apps

## Rationale

The sooner you paint and the sooner someone can do something, the better the experience for the person who is using the App.

![](assets/images/realworld-comparison-of-front-end-frameworks-2020__performance.png)

Performance (points 0–100) — higher is better.

## Remarks

_Note: PureScript was skipped due to a lack of Demo application._

## Conclusion

Lighthouse Audit doesn’t sleep. You can see this year that apps that are not maintained/updated are falling off the 90 cliff. If your app scores >90 it will probably not make a tons of difference. That said AppRun, Elm, and Svelte are really impressive.

# Metric #2: Size

Transfer size is from the Chrome network tab. GZIPed response headers plus the response body, as delivered by the server.

This depends on the size of a framework as well as on any extra dependencies added. Also how well a build build tool can eliminate the unused code from a bundle.

## Rationale

The smaller the file, the faster the download, and less to parse.

![](assets/images/realworld-comparison-of-front-end-frameworks-2020__transfer-size-in-kb.png)

Transfer size in KB — fewer is better

## Remarks

_PureScript was skipped due to a lack of Demo application._

_Angular +ngrx +nx please don’t blame me for Angular + ngrx + nx — check Chrome Dev Tools Network Tab, and if I counted wrong — let me know._

_Rust + Yew + WebAssembly includes also .wasm file(s)_

## Conclusion

Amazing work by Svelte and Stencil community, getting it under 20KB, is really an achievement.

# Metric #3: Lines of Code

Using [cloc](https://github.com/AlDanial/cloc) we count the lines of code in each repo’s src folder. Blank and comment lines are **not** part of this calculation. Why is this meaningful?

> _If debugging is the process of removing software bugs, then programming must be the process of putting them in — Edsger Dijkstra_

## Rationale

This shows how succinct given library/framework/language is. How many lines of code do you need to implement almost the same app (some of them have a bit more belts and whistles) accordingly to the specification.

![](assets/images/realworld-comparison-of-front-end-frameworks-2020__lines-of-code.png)

\# lines of code — fewer is better

## Remarks

_Svelte was added after the article was initially published — thanks to_ [_Svelte master_](https://twitter.com/MasterSvelte/status/1245765234561708032)_._

_riotjs-effector-universal-hot was skipped due to_ [_cloc_](https://github.com/AlDanial/cloc) _not being able to process_ `_.riot_` _files._

_Angular+ngrx: LoC calculation done with_ `_/libs_` _folder only including_ `_.ts_` _and_ `_.html_` _files. If you believe this is wrong, please let me know what is the correct number and how did you calculate it._

## Conclusion

Only Imba and [ClojureScript with re-frame](https://www.learnreframe.com/) can implement the app under 1000LoC. Clojure is known for being unusually expressive. Imba is here for the first time (last year cloc, didn’t know the .imba file format) and it looks like it’s here to stay. If you care about you LoC you know what to go for.

# Summary

Keep in mind that this is not exactly an apples-to-apples comparison. Some implementations use code splitting and some don’t. Some of them are hosted at GitHub, some at Now and some at Netlify. Do you still want to know which one is the best? I leave it up to you.

# FAQ

## #1 Why were framework X, Y, and Z not included in this comparison?

Because the implementation is not completed at [RealWorld repo](https://github.com/gothinkster/realworld). Consider contributing! Implement the solution in your favorite library/framework of choice and we will include it next time!

## #2 Why do you call it the real world?

Because it’s a bit more than a To-Do app. By RealWorld we don’t mean that we’ll compare salaries, maintenance, productivity, learning curves, etc. There are [other surveys](https://insights.stackoverflow.com/survey/2018/) that answer some of these questions. What we mean by RealWorld is an application that connects to a server, authenticates, and allows users to CRUD — just as a real-world app would do.

## #3 Why didn’t you include my favorite framework?

Please see #1 above, but just in case, here it comes again: because the implementation is not completed at [RealWorld repo](https://github.com/gothinkster/realworld). I don’t do all of the implementations — it’s a community effort. Consider contributing if you want to see your framework in the comparison.

## #4 Which version of the library/framework did you include?

The one that is available at the time of writing (Mar 2020). The information comes from [RealWorld repo](https://github.com/gothinkster/realworld). I’m sure you can find this out from the [GitHub repo](https://github.com/gothinkster/realworld).

## #5 Why did you forget to include a framework that is more popular than the one in the comparison?

Again, see #1 and #3. The implementation is not complete at [RealWorld repo](https://github.com/gothinkster/realworld); it’s that simple.

> If you like this article you should [follow me on Twitter](https://twitter.com/JacekSchae). I only write/tweet about programming and technology.
