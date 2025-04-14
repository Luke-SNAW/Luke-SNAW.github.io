---
id: qqewq42kqj04mhnus5kckzx
title: Four years of running a SaaS in a competitive market
desc: ""
updated: 1744605415294
created: 1744605270644
---

> https://maxrozen.com/on-four-years-running-saas-competitive-market

When I played around with the technology that would eventually become [OnlineOrNot](https://onlineornot.com/) back in 2021, a quick search showed me that there were 200 listed alternatives to the tool I wanted to replace. I thought most of them sucked.

There are even more today.

Over the years, many more started and shut down a few months later (it turns out running a business in a highly competitive space doesn't make you rich overnight). Others raised VC money or were acquired by a private equity firm, and started their descent into [enshittification](https://en.wikipedia.org/wiki/Enshittification).

I started work on OnlineOrNot because I wanted to build software that didn't have to get worse for its users in order to maximize shareholder value. In short, it's a self-funded, sustainable business that I intend to run for decades.

It's default-alive, as I keep a full time job so that I can build the business the way I want.

I've published one of these articles every year since starting, and there were things that I "learned" in the first year, that turned out to be total bullshit by the third year. So this article doesn't just look at the last 12 months, but across the entire lifetime of this business.

---

## Principles that haven't changed

While I've learned a lot about running a business over the years, there are some unchanging principles:

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#two-hours-a-day-every-workday)Two hours a day, every workday.

Years before I even started OnlineOrNot, I started hacking on my own projects in the two hours I have before starting my workday. Having a consistent block of time for myself has let me publish hundreds of articles, a book, dozens of software projects, and more.

Since starting, I worked out that the amount of time per day isn't as important as putting _any effort_ in, every day, for years.

> But how do you find time before your workday?

I started waking up two hours earlier, and adjusted the rest of my day accordingly.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#no-other-side-projects)No other side projects.

> the person who chases two rabbits catches neither

Of course, there are exceptional folks out there chasing a dozen rabbits and managing to catch some of them - I know myself well enough to realize that I'm not that person.

Building out the marketing and sales processes to take a business from $0 to $500 MRR is challenging enough. I don't see a point in repeating the hardest part of starting a business over and over again, instead of doubling down on what's already working (this is also a lesson for picking a marketing approach, more on that later).

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#solve-customer-pain)Solve customer pain.

When a user signs up for OnlineOrNot, I have an automated email going out asking what brought them to sign up today. I explicitly tell them I read and reply to every email. This is the main source of my insight for building product.

I ask my customers what isn't working, and I make it work.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#be-ruthlessly-iterative)Be ruthlessly iterative.

If I can't get a piece of work released in two hours, I cut the scope down to something achievable, and iterate on that.

It's worth noting that this is the ideal, and I don't always succeed at cutting down scope to exactly two hours. Over time I've realised that with how my brain works, I enjoy shipping early versions as quickly as possible, and building out the functionality once it's deployed (behind a feature flag).

Waiting until the entire feature is built before deploying completely saps my motivation in comparison, and I find myself easily distracted when building this way.

## [](https://maxrozen.com/on-four-years-running-saas-competitive-market#lessons)Lessons

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#read-a-few-books-and-start-building)Read a few books, and start building

I read dozens of business books when I wanted to get started, mainly from not wanting to repeat mistakes that others have made.

Sometimes though, you need to make mistakes for yourself.

As an example, it took me getting on the front page of Hacker News, having 6000 people visit my landing page, a few hundred people attempt to sign-up, and only single-digits making it through to the app for me to realise something might be wrong.

I had something like a 75% drop-off rate on my sign-up form alone. I got it down to 50% just by adding an extra OAuth login provider.

If I had to do it all again, I'd start with only three books:

- The Mom Test by Rob Fitzpatrick
- Deploy Empathy by Michele Hansen
- Badass: Making Users Awesome by Kathy Sierra

and if you need specific detail on building and running a SaaS, The SaaS Playbook by Rob Walling.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#solve-pain-dont-try-to-sell-a-subscription)Solve pain, don't try to sell a subscription

The product's goal is to solve your customer's pain, rather than sell subscriptions to your SaaS.

This is a mindset shift from "I'm just going to keep building features, they'll come eventually!" to "I should be helping my users solve this annoying problem in their job"

Building a SaaS is just one of the ways you could be solving their problem. There are other ways you could help, like recording screencasts, writing docs, articles, books, running workshops, providing code samples, etc.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#ship-small-ship-often)Ship small, ship often

People will suggest you should build particular features to improve your product.

They'll never use those features.

They're probably just trying to be helpful, and saw a similar feature in another product. Because you're new to running a SaaS, you'll be excited that people are actually talking to you, and rush out to build that feature for them.

I'm not going to tell you not to build the feature (that's the advice I was given, and I built unused features anyway). You should ask how they would use the feature, ask other customers how they deal with the problem, build the smallest possible version of that feature, and see how the rest of your customers use it. You don't want to be building snowflake features only one person uses.

It stings a lot less to remove a feature no one wanted after spending a few hours on it, rather than a few months.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#ship-first-worry-about-scale-later)Ship first, worry about scale later

In the first iteration of OnlineOrNot, I didn't optimise the architecture at all.

There was actually a bug that limited the total number of uptime checks the system could handle to around 100. I also didn't have proper error screens, so when users ran into that issue, all they saw on the screen was:

> Error!

Not a great look.

At the same time, I prefer being embarrassed by incomplete UI than building things people don't need. There was never a guarantee that OnlineOrNot would attract thousands of users, it could have ended up as another SaaS I built only for myself.

My immediate solution was to upgrade my database to a higher tier, increasing the number of uptime checks that could connect to the database, and in the meanwhile I got to work on rearchitecting the product.

A few hours later, I had a solution in place that could handle millions of checks per week on the smallest AWS database, and made that error screen look a bit more professional.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#have-an-early-access-program)Have an early-access program

Shipping early is incredibly useful. Early on in your product's development, almost all users that sign up are expecting rough edges (especially if they've seen your unpolished landing page).

As time goes on, you're going to get folks expecting a mature product, so you can't just keep shipping imperfect features to your entire userbase.

My solution for this was to add a checkbox in each user's account with the label "Join the Early Access Program". Folks that opt in get to see OnlineOrNot's latest features before they're ready, in exchange for patience and feedback.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#build-a-free-trial-as-soon-as-possible)Build a free trial as soon as possible

The common wisdom these days is to not even bother with a free tier - it's too difficult to get right. When I started though, a free tier was a great way to attract people and get them talking about your product.

The thing is, you still need a way to let them sample "the good stuff", especially if the free tier is significantly less useful than your paid tiers.

It took me 11 months to realise I should build an onboarding flow that ended with asking if folks wanted a free trial. Particularly, it asked:

> Do you want to start a free trial?

What it was actually saying was:

> Do you want to experience OnlineOrNot's best features for 14 days before deciding if it's worth your time, or spend months with a product that has the good stuff disabled, unsure if it'll actually solve your problems?

I eventually decided to experiment with defaulting all users to a free trial first, so that everyone could experience the _entire product_ first. This one experiment more than doubled OnlineOrNot's monthly growth rate.

It turned out that starting the business relationship with "this is a paid service, you'll need to add payment details to continue getting the good stuff" helps the business significantly more than "this is a free service, if you use it a lot, you might have to pay for it".

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#docs-are-the-product)Docs _are_ the product

Back when I started, folks used to say that "developers don't read documentation".

This turned out to be bullshit.

Some of the early customers in my ideal customer profile (ICP) came in praising OnlineOrNot's documentation, and I doubled down on it since. I even went as far as [building my API docs from scratch](https://onlineornot.com/built-my-http-docs-from-scratch) to have full control over the user experience.

Back when I had product analytics, I noticed people would struggle to do something in OnlineOrNot's UI, get frustrated, check the docs, and one of two things would happen:

1. They would find the exact feature they're looking for in the sidebar, and keep using the product for a long time
2. They would not find what they were looking for, not create any checks, and just churn

In short, successful use of the docs drove retention.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#build-for-mobile)Build for mobile

Contrary to popular belief (for B2B SaaS), folks actually work from their phones, and I think the rate is increasing.

Something like 50% of users start their journey to my product on mobile. They would quickly create an account, add a few pages to monitor, then eventually get on their laptop/desktop to review their checks from time to time.

For the first 6 months I didn't support mobile well, and folks that signed up on their phone churned rapidly. I eventually took the time to build responsive views for mobile, and new mobile users stuck around.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#ask-people-how-they-found-you)Ask people how they found you

One of the most valuable code changes I made halfway through the first year was asking people as they signed up: "How did you find out about OnlineOrNot?"

You need to know where your users are finding you.

There are dozens of marketing channels you could be using to attract potential customers. You only have a fixed amount of attention, so if you find a channel that's working more than others, you need to focus that attention on that channel until you notice diminishing returns.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#i-dont-use-invasive-analytics)I don't use invasive analytics

When I started, I integrated with standard SaaS product analytics software that most big SaaS products use. They tend to have features like session recording, where you can see exactly where their mouse moves in your product, and funnel tracking for working out how many users make it the whole way through from landing page to using your product.

This turns out to be useful in bigger companies. You have stakeholders to align with your vision of how the product should be built, it's easy to point to some data and show that version A resulted in sign-up uplift over version B.

The thing is, most products don't get enough users through the funnel to prove that the result you see is actually because something is better, rather than random chance.

As a solo founder with only two hours to spare every morning, I just didn't have the time to go through all that data and try to convince myself something. Instead I have an "inner-circle" of users that I DM for a vibe-check on features and problems in the product, and build things by taste.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#talk-to-potential-customers-even-if-you-think-you-have-nothing-for-them)Talk to potential customers, even if you think you have nothing for them

I was contacted by a CTO early on, asking if OnlineOrNot supported some particular feature.

My normal reaction would've been to just say "sorry, no" and leave it at that. Out of curiosity I started asking what pain they're trying to solve, I also asked the inner-circle users if they ran into this pain too, and what they'd like to achieve with the feature, and I told this CTO how I figured I would build it.

They signed up to a paid plan the next day, they've been customers ever since, and the feature gets used by other customers too.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#you-dont-get-to-spend-as-much-time-solving-the-problem-as-you-think)You don't get to spend as much time solving the problem as you think

Of all the time I spent programming in the last four years, significantly less than half went to actually solving the problem I wanted to solve (knowing if a site is down, and alerting folks when that happens). The majority went to building a SaaS platform around that problem.

SaaS platform things you didn't even realise you'd need, like multiple types of authentication and user management, trials, onboarding, recurring database jobs, team management and invoice management, lifecycle emails, and more.

A lot of folks outsource this type of work (and I do! If Stripe didn't exist, I probably wouldn't be selling a service nor using subscription-based billing), but there's always stuff you don't feel comfortable outsourcing, or that you handle differently, so you need to build it yourself.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#pricing-is-hard-to-get-right)Pricing is hard to get right

Price too high, and you'll either have churn from folks who expect your app does everything or completely kill your sign-up rate. Too low, and you'll have customers that demand you rewrite your app just because they gave you $9.

Refund the difficult customers, raise your prices, and move on. Be prepared to experiment a lot with pricing, especially early on and as you build functionality.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#dont-tunnel-vision-your-mrr)Don't tunnel-vision your MRR

Tracking your MRR is a crap way to measure how you're doing as a business.

Things you did weeks (if not months) ago will affect your MRR today, so you won't really know if pricing changes work until you've already got a decent number of customers going through different stages of their customer journey.

Depending on your product, it could take up to 60 days for a user to go from signing up for the first time, to entering their credit card details.

Find another success metric to figure out if people are actually using your product, and whether it's bringing them value. Things like number of images generated, or number of form completions, for example.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#never-give-away-unlimited-anything)Never give away "unlimited" anything

There will always, **always** be a whale customer for whom an unlimited amount of your value metric for $250/mo will be the deal of a lifetime. Generally speaking, never offer unlimited anything, especially if it costs you additional money for each thing created.

Lifetime deals fall under this advice too.

You aren't "finding users" for your product, you're finding people that expect you to build exactly the feature they want from you, years down the line, for that $100 they gave you once. Of which you likely only saw 30%, if you used a third-party to run the lifetime deal on their marketplace.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#rate-limit-your-paid-resources)Rate limit your paid resources

If you call any sort of paid API (whether it's AI, sending SMS/email etc) as part of your service, you're going to want to rate limit calls to that service.

> But my users are paying me for this service, shouldn't they be able to use it as much as they want?

Of course there are exceptions (and it depends on your Terms of Service), such as if an extremely large company starts using your service, but generally speaking, this will save you from a large unexpected bill at the end of the month, or being labelled a spammer by your vendors.

If someone genuinely needs to use your service at an extremely high rate, they'll get in touch.

This particular insight comes from the time OnlineOrNot sent thousands of SMSes to a web agency when the one server holding hundreds of their WordPress websites started running out of RAM.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#stop-trying-to-explain-everything-on-one-page)Stop trying to explain everything on one page

> If you try to be everything to everyone, you'll end up being nothing to no one

I think this applies particularly well to copywriting for landing pages.

As I built additional features into OnlineOrNot, I would try add additional sections to my main landing page, and it ended up an incoherent mess, diluting the overall message. I would have folks emailing me to ask if I supported sending alerts to Slack, when it was the second feature I built for OnlineOrNot.

Instead, by breaking up each feature into its own landing page:

- [main landing page](https://onlineornot.com/)
- [uptime monitoring](https://onlineornot.com/website-monitoring)
- [api monitoring](https://onlineornot.com/api-monitoring)
- [status pages](https://onlineornot.com/status-pages)
- [cron job monitoring](https://onlineornot.com/cron-job-monitoring)

I can take the space to explain each feature, without diluting the message.

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#its-hard-to-bring-in-more-traffic-easy-to-change-what-your-current-traffic-does)It's hard to bring in more traffic, easy to change what your current traffic does

Getting noticed on the internet is a long, slow game.

Eventually over months (if not years), if you're consistent at quality content marketing, the number of readers on your articles will grow from 1-2 a day, to a few hundred per day.

Increasing the number of people landing on your site isn't particularly easy.

On the other hand, what people do once they land on your site is entirely within your influence, and something you can change today (such as adding an additional OAuth login provider to your sign-up form, that I mentioned earlier).

### [](https://maxrozen.com/on-four-years-running-saas-competitive-market#competitors-dont-really-matter)Competitors don't really matter

You might have noticed I haven't mentioned anything about competitors here, despite operating in a highly competitive market.

The truth is I don't think they change much.

Sure, there are more "table-stakes" features that customers need before they'll even consider using you, but **the real competitor is a lack of awareness of your product**, more than anything.

---

> https://news.hada.io/topic?id=20325

- Max Rozen이 창업한 OnlineOrNot은 이미 **200개 이상의 경쟁 제품이 존재**하는 시장에서 시작됨
- 초기에는 많은 제품이 사용하기 불편했으며, 이후 수많은 경쟁 제품이 등장하고 빠르게 사라짐
- 일부 경쟁 제품은 VC 자금을 받고 대기업에 인수되며 사용자 경험이 점점 악화되는 방향으로 전개됨
- OnlineOrNot은 자가 자금으로 운영되는 **장기 지속 가능한 사업**을 목표로 함
- 저자는 여전히 풀타임 직장을 유지하며 꾸준히 SaaS를 개발함
- 매년 회고글을 작성하며, 과거에 배운 교훈 중 일부는 시간이 지나며 틀렸음이 드러남

## 변하지 않은 원칙들

수년간 사업 운영에 대해 많은 것을 배웠지만, 여전히 변하지 않고 유지하고 있는 핵심 원칙들이 있음

### 매일 근무일마다 2시간씩 투자함

- OnlineOrNot을 시작하기 전부터 매일 아침 출근 전 2시간 동안 개인 프로젝트에 몰두함
- 이 시간을 활용해 수백 편의 글, 책 한 권, 여러 소프트웨어 프로젝트를 완성함
- 하루에 얼마를 투자하느냐보다 **매일 꾸준히 노력하는 것 자체**가 더 중요함
- 이 시간을 확보하기 위해 **2시간 일찍 기상**하고 일과를 조정함

### 다른 사이드 프로젝트는 하지 않음

- "두 마리 토끼를 쫓는 자는 하나도 잡지 못한다"는 말처럼, 하나에 집중함
- 일부 예외적인 인물은 여러 프로젝트를 성공시키지만, 본인은 그와 다름을 인정함
- $0에서 $500 MRR까지 올리는 과정이 가장 어렵고 반복할 필요가 없다고 판단함
- 이미 작동하는 모델에 집중하고, 마케팅 방식도 같은 관점에서 선택함

### 고객의 고통을 해결하는 것이 우선임

- 사용자가 가입하면 자동 이메일을 통해 "왜 가입하셨나요?"라는 질문을 보냄
- 이메일을 모두 읽고 직접 답장하며, 이것이 제품 개선의 핵심 인사이트가 됨
- **사용자가 불편해하는 점을 파악하고, 실제로 그것을 해결함**

### 집요하게 반복하며 개선함

- 어떤 작업도 **2시간 내에 배포하지 못한다면**, 범위를 줄여 먼저 배포함
- 항상 이상적으로 딱 2시간에 맞추진 못하지만, **빠르게 초기 버전을 배포**하고 기능을 확장하는 방식을 선호함
- 모든 기능을 다 만들고 배포하려 하면 오히려 동기부여가 사라지고 집중력이 흐려짐
- **기능 플래그 뒤에서 점진적으로 기능을 완성하는 방식**이 훨씬 효과적임

## 배운 교훈들

### 책 몇 권만 읽고 바로 만들어 보기

- 시작할 때 실수를 줄이기 위해 수십 권의 비즈니스 책을 읽었음
- 하지만 결국 **직접 실수하면서 배우는 것이 가장 효과적**이라는 점을 깨달음
- 예: Hacker News 메인에 올라 6000명이 방문했지만 실제 앱까지 도달한 사용자는 한 자릿수에 불과
- 가입 폼에서만 75% 이탈 → OAuth 로그인 옵션 하나 추가로 이탈률 50%까지 개선
- 만약 다시 시작한다면 아래 세 권만 읽고 바로 시작했을 것:
  - _The Mom Test_ (Rob Fitzpatrick)
  - _Deploy Empathy_ (Michele Hansen)
  - _Badass: Making Users Awesome_ (Kathy Sierra)
  - SaaS 운영의 실전 디테일이 필요하다면 _The SaaS Playbook_ (Rob Walling) 추가 추천

### 구독 판매보다 문제 해결이 먼저임

- SaaS의 목적은 구독을 파는 것이 아니라 **고객의 고통을 해결하는 것**
- "기능을 계속 만들면 언젠가는 사람들이 써주겠지" → "사용자의 업무에서 짜증나는 문제를 해결하자"로 사고 전환 필요
- SaaS는 문제 해결의 한 방식일 뿐이며, 그 외에도 screencast, 문서, 글쓰기, 책, 워크숍, 코드 샘플 등 다양한 접근 가능

### 작게 만들고 자주 배포하기

- 사용자들은 기능 아이디어를 제안하지만 실제로는 거의 사용하지 않음
- 처음 SaaS를 시작한 사람은 누군가와 대화하는 것만으로도 감격해서 무작정 기능을 만들어버리기 쉬움
- 그 기능을 어떻게 사용할 건지 물어보고, 다른 사용자들의 문제 해결 방식도 조사한 후,
  - **최소한의 기능으로 먼저 구현**해서 반응을 확인해야 함
- 단 한 명만 사용하는 ‘눈송이 기능’을 만드는 것보다, 다수가 쓰는 기능을 만들기 위한 전략적 접근이 중요
- 몇 시간 투자한 기능을 제거하는 것은 아프지만, **몇 달 투자한 기능을 제거하는 건 훨씬 더 고통스러움**

### 일단 배포하고, 확장은 나중에 고민하라

- OnlineOrNot 초기 버전은 **아키텍처 최적화 없이** 빠르게 출시됨
- 실제로는 시스템이 처리할 수 있는 체크 수가 약 100개로 제한되는 버그가 있었고,
  - 문제 발생 시 사용자에게 단순히 "Error!"만 보여주는 UI로 매우 미완성된 상태였음
- 하지만 저자는 **불필요한 기능을 만드는 것보다 미완성 UI로 욕먹는 쪽**을 선택함
- 처음부터 수천 명의 사용자가 올 거라는 보장이 없기 때문에, 빠르게 검증하는 것이 더 중요했음
- 임시로 데이터베이스를 상위 플랜으로 업그레이드하여 체크 수용량을 늘림
- 몇 시간 내에 수백만 개 체크를 처리할 수 있는 구조로 리팩토링하고, 오류 화면도 개선함

### 얼리 액세스 프로그램 운영

- 제품 개발 초기에는 대다수 사용자가 **불완전한 기능에 대해 어느 정도 관용적**
- 시간이 지나며 더 성숙한 제품을 기대하는 사용자가 늘어나게 됨
- 이를 해결하기 위해 각 사용자 계정에 "얼리 액세스 프로그램 참여" 체크박스를 추가함
  - 참여자는 아직 완성되지 않은 최신 기능을 먼저 사용해보고 피드백을 제공함
- **테스트와 피드백의 균형을 맞추는 방법**으로 유용하게 작동함

### 무료 체험은 가능한 빨리 도입하라

- 요즘은 "무료 플랜은 맞추기 너무 어려우니 하지 말자"는 조언이 일반적임
- 그러나 초기에는 **무료 플랜이 입소문과 사용자 유입에 효과적**이었음
- 단점은 무료 플랜이 유료 기능과 차이가 클 경우, **좋은 기능을 체험할 방법이 필요**하다는 점
- 시작 11개월 후에야 온보딩 과정에서 "무료 체험을 시작하시겠습니까?"라는 질문을 추가함
  - 실제 의미는 다음과 같음:
    > “좋은 기능을 14일간 체험하고 결정하시겠습니까, 아니면 몇 달을 기능이 제한된 상태로 써보다 결국 실망하시겠습니까?”
- 이후 실험적으로 **모든 사용자에게 기본적으로 무료 체험을 제공**하게 했고,
  - 이 실험 하나만으로 월간 성장률이 2배 이상 증가함
- 결론:
  - "이건 유료 서비스입니다. 좋은 기능을 계속 쓰려면 결제 정보가 필요합니다"는 메시지가
  - "이건 무료 서비스예요. 많이 쓰면 유료일지도요"보다 **비즈니스적으로 훨씬 효과적**

### 문서 자체가 제품임

- 과거에는 "개발자는 문서 안 읽는다"는 말이 흔했지만, **완전히 잘못된 말**
- 이상적인 고객 중 일부는 OnlineOrNot의 문서를 칭찬했고, 이를 계기로 문서에 집중 투자함
- API 문서도 직접 구축해 **사용자 경험을 완전히 제어**할 수 있도록 설계함
- 제품 분석 도구로 관찰한 결과:
  1. 사용자가 UI에서 문제를 겪고, 문서를 확인 후 **기능을 찾아내면 제품을 계속 사용함**
  2. 원하는 정보를 못 찾으면 체크를 생성하지 않고 **이탈**
- **문서의 품질이 곧 사용자 유지율에 직결됨**

### 모바일 환경을 고려해 제품을 설계하라

- 일반적인 생각과는 달리, **B2B SaaS 사용자들도 스마트폰으로 업무를 시작함**
- 실제로 전체 사용자의 약 50%가 **모바일에서 제품 사용을 시작**함
  - 계정을 만들고 몇 개의 페이지를 등록한 후, PC에서 다시 확인하는 흐름
- 처음 6개월 동안 모바일 환경을 고려하지 않았고, 모바일 가입자는 대부분 이탈했음
- 이후 반응형 UI를 도입한 결과, **모바일 사용자 유지율이 눈에 띄게 증가**

### 사용자에게 유입 경로를 직접 물어보라

- 1년차 중반에 도입한 가장 가치 있는 코드 변경 중 하나는
  - **가입 시 "어디서 OnlineOrNot을 알게 되었나요?"** 라는 질문을 추가한 것
- 사용자 유입 채널을 파악하는 것은 마케팅 효율 극대화에 매우 중요함
- 마케팅 채널은 수십 개나 되지만, 집중할 수 있는 자원은 제한적임
- 잘 작동하는 채널이 확인되면 **그 채널에 집중 투자하고**, 반응이 줄어들 때까지 지속함

### 침입적 분석 도구는 사용하지 않음

- 처음에는 일반 SaaS 제품처럼 **세션 추적, 퍼널 분석 도구**를 도입했으나, 실효성이 낮았음
- 대규모 팀에는 유용할 수 있으나, 소규모 서비스에는 **랜덤한 결과로 오해할 가능성**이 큼
- 솔로 창업자로서 매일 아침 2시간밖에 없는 상황에서는,
  - 방대한 데이터를 분석하기보다는, **신뢰하는 사용자 그룹(inner-circle)에게 직접 의견을 받는 방식**이 더 효과적이었음
- 기능이나 문제점에 대해 감각적으로 피드백을 받고, **감성 기반 판단으로 제품을 개선함**

### 기능이 없어도 잠재 고객과 대화하라

- 어느 날 CTO로부터 특정 기능 지원 여부를 문의받았음
- 원래는 "죄송합니다. 아직 없습니다"라고 끝낼 생각이었지만,
  - **호기심에 그들이 겪고 있는 문제와 해결하고자 하는 목표를 질문**
  - inner-circle 사용자에게도 해당 문제를 겪는지 물어봄
  - 기능을 어떻게 설계할지에 대한 아이디어를 공유함
- 결과적으로 **이 CTO는 다음 날 유료 가입자가 되었고**, 지금까지도 고객으로 남아 있음
- 해당 기능은 다른 사용자들도 잘 활용하고 있음

### 문제 해결보다 플랫폼 구축에 더 많은 시간을 씀

- 지난 4년간의 개발 시간 중 **절반 이상은 SaaS 플랫폼 구축에 사용됨**
  - 본래 목표인 “웹사이트 다운 여부 확인 및 알림”은 일부분일 뿐
- 실제로 필요했던 기능들:
  - 다양한 인증 방식과 사용자 관리
  - 체험판, 온보딩
  - 반복적인 DB 작업, 팀 관리, 인보이스 처리
  - 라이프사이클 이메일 등
- 일부는 Stripe 같은 서비스로 아웃소싱했지만,
  - **직접 처리하거나 개별화가 필요한 부분도 많아 결국 직접 구현**

### 가격 책정은 정말 어려움

- 가격이 너무 높으면 기대치가 올라가거나 아예 가입을 꺼림
- 가격이 너무 낮으면 $9 낸 사용자가 **전체 앱을 자기 입맛대로 고쳐달라고 요구**하기도 함
- 해법:
  - 까다로운 고객은 **환불해주고 보내줌**
  - 가격을 올리고, 다음으로 나아감
  - 특히 초기에 기능을 확장해 나갈수록, **지속적인 가격 실험이 필수적**

### MRR에만 집착하지 마라

- **MRR(Monthly Recurring Revenue)** 는 사업 성과를 측정하기에 부적절한 지표일 수 있음
- 몇 주 또는 몇 달 전에 했던 일이 **지금의 MRR에 영향을 미치므로**, 실시간 효과 측정이 어려움
- 일부 SaaS 제품은 사용자가 가입 후 실제 결제까지 **60일 이상 소요될 수 있음**
- 따라서 다른 지표를 통해 실제 사용 여부와 가치 전달 여부를 파악해야 함
  - 예: 생성된 이미지 수, 제출된 폼 수 등 **행동 기반 성공 지표** 사용 권장

### “무제한 제공”은 절대 하지 마라

- 항상 **“무제한”을 최대한 활용할 사용자(whale customer)** 는 존재함
- 예: $250/월만 내고 엄청난 리소스를 사용하는 고객
- 무제한이 제공하는 단위가 **비용이 발생하는 항목**이라면, 무조건 손해임
- 이 조언은 **라이프타임 딜**에도 해당됨
  - $100에 평생 사용을 약속하면, 이후 수년간 기능 추가 요구를 받을 수 있음
  - 제3자 마켓플레이스를 이용했다면 실제 수익은 이 중 30%만 수령할 수도 있음
- 결국 진짜 고객이 아닌, **단기적 이익을 원하고 오래 묶이는 사용자를 초대하는 꼴**

### 유료 리소스는 반드시 rate limit 적용

- AI, SMS, 이메일 전송 등의 **유료 API를 사용하는 경우**, 사용량 제한이 필수임
- "유료 고객이니까 무제한으로 써도 되는 거 아닌가요?" → 예외적인 경우는 있을 수 있으나,
  - 대부분의 경우 **비용 폭탄 또는 벤더로부터 스팸 레이블** 위험 발생
- 실제 사례:
  - WordPress 사이트 수백 개가 호스팅된 서버가 RAM 부족으로 오류 발생
  - 그 결과 수천 개의 SMS 알림이 자동 발송되어 큰 비용이 발생함
- 진짜 대량 사용이 필요한 고객이라면 **직접 연락을 해올 것임**

### 한 페이지에 모든 걸 설명하려 하지 마라

> "모든 사람에게 모든 것을 전달하려 하면, 아무에게도 아무것도 전달하지 못한다"

- 이 말은 **랜딩 페이지 카피라이팅에 특히 잘 적용됨**
- OnlineOrNot에 기능이 추가될 때마다 메인 랜딩 페이지에 설명을 계속 추가했더니
  - 메시지가 산만해지고 사용자의 이해도도 떨어짐
  - 예: Slack 알림 기능이 두 번째로 만든 기능이었지만, 많은 사람들이 이 기능이 있는지조차 몰랐음
- 해결책: **기능별로 별도 랜딩 페이지를 만들어 설명**
  - 메인: [https://onlineornot.com/](https://onlineornot.com/)
  - 업타임 모니터링: [https://onlineornot.com/website-monitoring](https://onlineornot.com/website-monitoring)
  - API 모니터링: [https://onlineornot.com/api-monitoring](https://onlineornot.com/api-monitoring)
  - 상태 페이지: [https://onlineornot.com/status-pages](https://onlineornot.com/status-pages)
  - 크론잡 모니터링: [https://onlineornot.com/cron-job-monitoring](https://onlineornot.com/cron-job-monitoring)
- 각각의 페이지에서 충분한 공간을 들여 **명확하게 기능을 전달**할 수 있음

### 트래픽 늘리기는 어렵고, 전환율 개선은 지금 당장 가능함

- 인터넷에서 주목받는 것은 **장기전이며 매우 느림**
  - 꾸준히 양질의 콘텐츠 마케팅을 해도, 1~2명의 방문자가 수백 명으로 늘기까지는 수개월~수년 소요
- 트래픽 자체를 늘리는 것은 쉽지 않음
- 반면, **이미 온 사용자들의 행동은 즉시 바꿀 수 있음**
  - 예: 가입 폼에 OAuth 로그인 옵션을 추가하는 것처럼, **오늘 적용 가능한 개선이 전환율을 높임**

### 경쟁자는 그렇게 중요하지 않음

- 이 글 전체에서 **경쟁자 이야기가 거의 없는 이유**는 실제로 큰 영향을 미치지 않기 때문임
- 물론 기본적인 기능은 갖추어야 고객이 고려 대상에 올리지만,
  - 진짜 경쟁자는 **사용자가 이 제품의 존재 자체를 모르는 것**
- 기능보다도 **인지도와 접근성**이 핵심 경쟁 요소임
