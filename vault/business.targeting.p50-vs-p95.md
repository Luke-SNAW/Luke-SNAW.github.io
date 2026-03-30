---
id: o4594n16kk9klo138jbf16w
title: "Don’t Design for Average Users"
desc: ""
updated: 1774855223561
created: 1774854842766
published: false
---

> https://www.uxtigers.com/post/p50-vs-p95

---

> **Summary**: The average user is a terrible design target for digital products. High-end “Whale” users in the 95th or 99th percentile of usage volume (P95 or P99) have different needs and often generate dramatically more business value than the masses of low-end users that hit the P50 median usage metrics. The P95/P50 ratio ranges from 3 to 100 (or higher), depending on domain characteristics, leading to different recommended design strategies.

Averages flatten reality. In product work, a small minority of users often generate a disproportionate share of usage, revenue, support load, and learning about what the product is becoming. That makes the mean a poor guide to design. The more revealing comparison is usually between the median user, who represents typical behavior, and the 95th-percentile user, who marks the beginning of the heavy-use tail.

**I made a short** [**explainer video about this article**](https://youtu.be/PwwzDc_l6zE) **(YouTube, 7 min.).**

In the world of high-stakes digital strategy, the “average user” is a dangerous statistical artifact. For decades, businesses have built roadmaps around the arithmetic mean, using metrics like Average Revenue Per User (ARPU) and mean session duration. This assumes a traditional normal distribution, the “Bell Curve” of the physical world, where measures such as height, weight, and IQ cluster around a predictable center.

The arithmetic mean works well in many physical settings where variation clusters around a center. If you size a doorway for average height plus a safety margin, it serves most people well. Digital behavior is different. Engagement often follows skewed distributions, where large populations of casual users coexist with a small group of intensely active ones.

_We are used to thinking in terms of the normal distribution, and its famous bell curve, because it describes most phenomena in the physical world. However, the digital world operates on entirely different mathematics, making our instinct to design for the average dangerously wrong. (NotebookLM)_

If you were to ask a tech executive to describe their average user, they might point to a dashboard showing a person who spends 20 minutes a day on the app and generates $5.00 in revenue. But **that person is a phantom.**

_In many digital products, the “average user” doesn’t really exist. Users are either far below or far above the mean. (NotebookLM)_

Digital reality obeys different physics. Engagement follows power laws, Zipf distributions, and log-normal skews. The result is a “Mathematical Ghost” where the mean value sits in a hollow valley between a massive volume of casual “tourists” and an ultra-engaged minority. Designing for this arithmetic average forces you to optimize for a phantom, neglecting both the simple needs of the many and the intensive requirements of the few.

_Many digital usage metrics follow a power law that is extremely skewed, with most users at the low end and a few at the high end, yet the tail often contains most of the business value. (NotebookLM)_

To drive growth, you must stop designing for these ghosts and start designing for the radical asymmetry between the median (P50) and the 95th percentile (P95) user.

Digital spaces are governed by **Participation Inequality**. My earlier “90-9-1” rule captured the first version of this pattern: most users lurk, a smaller group contributes occasionally, and a tiny minority creates most of the value. As digital products have scaled, the concentration is now even harsher, particularly on platforms where the P50 user’s contribution is zero.

- **The Three Tiers of the Participation Hierarchy** (as I used to describe it):
  - **90% are Lurkers:** They observe and consume. Their creative contribution is **zero**, making the ratio between them and creators effectively infinite.
  - **9% are Contributors:** They participate intermittently with the occasional "like" or comment.
  - **1% are Superusers:** The engines of the platform who produce nearly all the value.

_Participation inequality, as I defined it in the early days of the Web. The ratios are much more extreme now. (NotebookLM)_

- **Modern Data:**
  - **Wikipedia (The 99.8-0.2-0.003 Rule):** 99.8% of visitors are lurkers. Only 0.2% are active contributors, and a tiny elite of **0.003%** (just 1,000 people) produce **two-thirds of all edits**.
  - **X (Twitter):** One X dataset makes the concentration clear even before you reach P95: the median user **posts 2 times** a month, while the 90th percentile **posts 138 times**, a 69x gap. In other words, the curve is already highly skewed before you get to the true heavy-use tail. In social web apps, the same pattern shows up in task completion and network building: power users explore far more features and follow far more accounts than mainstream users.
  - **TikTok:** The top 1% of creators produce **147x more videos** than light posters.

_The median (P50) user is often a tourist in your application: visiting from time to time but not contributing much business value. (NotebookLM)_

_The heavy (P95) user can be a “Whale” who generates almost all your profits. (NotebookLM)_

This inequality is not a bug; it is the structural reality of the internet. However, this gap expands even further when we move from social consumption to the professional application of Artificial Intelligence.

In AI systems, we witness a **Usage Cliff**: P95 Frontier Workers use AI tools in fundamentally different ways than P50 Tourists. This isn’t just about volume; it’s about a **Skills Gap** and the resulting infrastructure load.

- **The Prompting Chasm: Complexity vs. Simplicity:** A P50 ChatGPT user sends a 50-word prompt in a single "turn." A P95 Frontier User sends prompts averaging **1,750 words** across 6+ turns. This represents a **35x ratio** in message complexity.
- **The Retention Chasm:** P95-focused products (those that successfully cultivate power users) retain **15.6%** of users at 3 months, compared to a meager **2.5%** for the industry median.
- **The Feature Mastery Gap:** The P50 user sticks to the “Happy Path,” adopting only **16% of features**. The P95 user adopts **45% or more**, utilizing APIs, macros, and complex workflows.
- **The Coding Chasm:** Frontier coders send **17x more requests** to AI assistants than the P50 developer.

To analyze the digital economy, we must move from raw numbers to behavioral archetypes. The P95 user is not just a frequent visitor; they are the economic engine that subsidizes the P50 user’s experience. Because the median user often contributes zero, the ratio of economic value for the product between the P95 and the P50 users is **effectively infinite**.

| Feature                    | Median (P50) "Tourist"                                            | Power User (P95) "Whale"                                                           |
| -------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **Archetype Behavior**     | Passive consumption; Transactional.                               | Active creation; Workflow integration.                                             |
| **Primary Driver**         | **External** triggers (Notifications).                            | **Internal** triggers (Habit loops/Work).                                          |
| **Retention & Stickiness** | 5% DAU/MAU.                                                       | 30% DAU/MAU.                                                                       |
| **Business Role**          | Supplies audience, density, and baseline demand.                  | Disproportionate revenue, content, and product learning.                           |
| **Churn Risk**             | High sensitivity to early friction and confusion.                 | High sensitivity to ceilings, latency, and missing controls.                       |
| **Spending Examples**      | **Amazon:** ~$600/year (Non-Prime customer). **Mobile Games:** $0 | **Amazon:** ~$1,400/year (Prime customer). **Mobile Games:** $1,700 lifetime spend |

# Understanding the P95/P50 Ratio

The key metric to understand the difference between average users and valuable users is the P95/P50 ratio. P95 is the 95th percentile, or the metric that characterizes the most active 5% of users. P50 is the 50th percentile (the median) value, where half of the users engage more, and half of the users engage less. For some product categories, the P99 user (the 99th percentile, or the top 1%) is even more important, because they are so much more valuable than even the P95 users.

The P95/P50 ratio is not a universal constant for all computer use; it varies based on cohort policy, task structure, and natural friction. However, empirical data across different sectors highlights a blunt reality: the P95 user is never just a “slightly heavier” user.

One caution: heavy *use* and high *value* are not always the same thing. Some heavy users are profitable, influential, and worth designing around. Others are merely expensive, support-intensive, or exploiting a loophole. A mature product should therefore track at least four separate tails: usage volume, revenue, support cost, and strategic value. The P95 on one axis is not necessarily the P95 on another.

_In many cases, the business value of a few Whales vastly outweighs the much larger number of lower-end users. (NotebookLM)_

**1\. E-Commerce and Services (3x to 10x Ratio):** Physical world constraints bound e-commerce. You can only eat so many meals delivered by DoorDash; you only need to buy so many pairs of shoes. Consequently, the ratios here are more compressed. The median e-commerce shopper might visit a site 1 or 2 times a month. The P95 “Super Shopper” visits daily or several times a week, yielding a session frequency ratio of roughly 3x to 5x, and a revenue ratio that is considerably higher due to increased average order values.

**2\. Enterprise SaaS and Productivity (6x to 17x Ratio):** In Business-to-Business (B2B) software, usage is somewhat constrained by work hours and professional necessity, meaning the median user cannot drop to zero. Yet the disparity remains vast. In enterprise AI adoption, frontier workers at the 95th percentile send 6 times as many messages as the median worker.

When the workflow becomes specialized, the gap explodes. For data analysis tasks, P95 usage is 16 times the median. For AI coding assistance, P95 users send 17 times more requests than the median user. These ratios prove that power users aren’t just working more; they are working _differently_. They routinize the tool, build macros, and integrate APIs, whereas the median user sticks to the basic “happy path.”

**3\. Social Media (The 30x to 550x Ratio):** Because social media engagement is entirely discretionary and not bounded by work shifts or physical goods, the concentration ratios reach astronomical heights.

The median X (Twitter) user posts 2 tweets a month. The 90th percentile user posts 138 times a month: a 69x difference. When evaluating task completion (profile updates, settings tweaks, feature exploration) in social web apps, the P95 user completes 492 tasks compared to the median user’s 7 tasks: a 70x ratio. In network building, power users follow 550 times more accounts than the mainstream user.

_Content creation is one of the domains with the highest participation inequality ratios: most users are happy to lurk and consume the content produced by a tiny fraction of heavy contributors. (NotebookLM)_

**4\. Mobile Gaming (10x to Infinite Ratio):** Nowhere is the concept of the “Whale” more literal than in freemium mobile gaming. The median user spending in a freemium game is exactly $0.00. They monetize only via microscopic fractions of a cent from ad impressions.

The P95 user, however, crosses the threshold into paying territory, and the P99 “Mega Whale” generates the entire economy of the ecosystem. Historically, the top 1% to 5% of users generate 50% to 80% of total revenue. In titles like _Fate: Grand Order_, 20.6% of players spend over $1,800 annually. When the median spend is zero and the P95 spend is uncapped, the ratio is effectively infinite. Time investment mirrors this: a casual median player might log 10 to 20 minutes a day, while a P95 hardcore player logs 3 to 6 hours. The P95 Whale is subsidizing the server costs, the development, and the free ride of the P50 median user.

These are not trivial differences. They represent fundamentally different behavioral regimes.

Here’s an overview of typical P95/P50 ratios for different usage scenarios.

| Category                      | P95/P50 Ratio | Primary Driver                                | Inequality Level |
| ----------------------------- | ------------- | --------------------------------------------- | ---------------- |
| **E-Commerce (Sessions)**     | **3–5×**      | Purchase intent, utility usage                | Moderate         |
| **Enterprise Messaging**      | **6×**        | Professional necessity, role requirements     | Moderate         |
| **Mobile Gaming (Sessions)**  | **10–15×**    | Habit formation, retention selection          | High             |
| **Enterprise Data Analytics** | **16×**       | Skill barriers, workflow integration          | High             |
| **Enterprise Coding/AI**      | **17×**       | Technical specialization, deep integration    | High             |
| **E-Commerce (Revenue)**      | **20×+**      | Purchase frequency, order value               | High             |
| **Social Messaging**          | **34×**       | Discretionary engagement, network effects     | Extreme          |
| **Social Task Completion**    | **70×**       | Feature exploration, platform mastery         | Extreme          |
| **Mobile Gaming (Revenue)**   | **100×+**     | Whale economics, freemium models              | Severe           |
| **Social Network Building**   | **550×**      | Influence accumulation, weak-tie optimization | Severe           |

_User behavior is not uniform, but highly variable, with the P95/P50 ratio often ranging from 10x to 100x. (NotebookLM)_

# Why P95/P50 Varies

Several structural factors drive this variance:

- **Task structure:** Some tasks naturally break into many small loops. Coding, writing, and analysis are iterative, decomposable, and easy to resume. One successful AI interaction creates the next one. That is why coding shows the largest reported enterprise-AI gap at 17x. Creative media is also iterative, but it is slowed by taste, review, and selection, so the ratio is lower at 8x. The product may be the same, yet the economics of interaction differ sharply by task.
- **Role heterogeneity:** The same interface can serve radically different jobs. A single product-level P95 statistic can be a collage of incompatible users: the analyst, the approver, the administrator, and the integrator may all count as “heavy” while needing very different tools. That is why percentile analysis should be paired with job-to-be-done analysis.  Otherwise, you risk building one generic power-user mode that serves none of your actual power users especially well. A general-purpose AI assistant looks uniform on the surface, but data-analysis workers use the analysis tool 16x more than the median in their own function, and frontier firms generate 7x more messages to GPTs than the median firm. This is evidence that the product has become embedded in the workflow of some roles and not others.
- **Friction and infrastructure:** Remove barriers, and the tail widens. When capacity, convenience, and pricing stop punishing usage, the heaviest users pull farther away from the median.
- **Metric choice:** There is no single P95/P50 ratio for a product. The ratio for monthly bytes, number of sessions, session duration, spend, or distinct task types can differ dramatically. In a study of mobile users in Finland, monthly *data volume* was roughly 8–11x at p95 relative to p50, while *session duration* was only about 2.3x. The heavy user was mainly heavier because they came back more often and moved more data, not because each visit was much longer. This matters for design, because different metrics point to different problems.
- **Compounding returns:** When more use produces more value, the upper tail becomes self-reinforcing. OpenAI’s enterprise data shows that users engaging across roughly seven task types report about 5x more time saved than users engaging across about four. That is the benign version. Poker shows the darker version: session counts rise steeply, but spend rises much faster still. Once incremental usage keeps paying off, the tail stops behaving linearly.
- **Organizational maturity:** In enterprise products, heavy use often reflects not only user motivation but also local systems: templates, norms, shared assets, training, governance, and management support. This is why frontier firms in the OpenAI report are only about 2x the median firm in overall messages per seat, yet 7x in messages to GPTs. Advanced usage is not just more usage. It is a more structured usage.

## Time Windows Change the Ratio

A daily window often compresses differences because even power users have a limited number of waking hours. When you aggregate over weeks or months, volume becomes closer to a **cumulative advantage** story (as the active get more active), and tails typically widen. This is one reason “usage over lifetime” distributions, such as reputational points or total matches played, can yield P95/P50 in the tens or higher.

Monthly, Yearly, or Lifetime values are typically the most important to analyze, depending on your product. However, to compare P95/P50 ratios over time (for example, how they change after a redesign), stick to one time window and use it consistently.

- A sudden jump in P95/P50 often means **tail expansion**: either a real product change that amplifies power users, or an artifact of bad analytics that are skewed by bots or scraping.
- A sharp drop can mean **tail compression**: rate limiting, outages affecting heavy users, or a logging change that undercounts high-volume activity.

Tenure matters almost as much as the time window. If you mix week-one novice users with year-three veterans, the product will often look more unequal than it really is, because many low-end users have not yet had time to mature. Cohort the ratio by user age: new, activated, retained, and veteran. That lets you distinguish a healthy growth curve from a product that merely sheds the median and survives on a small expert core.

# The P50 Tourist: Fragile, Transactional, and Friction-Averse

To design effectively, UX professionals must stop drafting personas for a homogenized “average” user. You must bifurcate your user research. You need to design for the P50 Tourist and the P95 Whale separately.

Let us define the **P50 User**. This is your median user. They are the tourist in your application.

The P50 Tourist interacts with your product passively, sporadically, and with minimal economic contribution. They are highly averse to friction. If they encounter a complex dashboard, an unexplained feature, or a multi-step onboarding process, they will simply churn. Their engagement is incredibly fragile, often driven solely by external triggers like push notifications or immediate, low-frequency utility.

_Casual or tourist users should have the easiest possible path. Allow no difficulty to get in their way. (NotebookLM)_

When looking at feature adoption in SaaS, the median user touches only about 16% of a product's available capabilities. They stick strictly to the “happy path” of the core two or three functions necessary to complete a basic task, such as sending a simple message in Slack or updating a single field in Salesforce. They do not explore. They do not customize.

When you design for the P50 Tourist, your sole objective is **activation and retention**. The interface must be ruthlessly simplified. You must conceal complexity and lower cognitive load. The median publisher on a newsletter platform, for example, needs exactly one clean path: draft, preview, send, and see basic results. If you dump advanced segmentation logic and deliverability diagnostics onto their first screen, you will scare them away.

You need these users because they provide audience, density, and reach. But they are not the users who will master your product or pay for depth.

# The P95 Whale: Unbounded, Demanding, and the Engine of Value

Now, let us look at the **P95 User**. This is the Whale. The Superuser. The Innovator.

While the P50 user visits your product, the P95 user _lives_ in it. In enterprise software, they integrate your tool into their minute-by-minute workflow. In streaming, they enter a binge-watching flow state driven by your recommendation algorithm. In social media, they are the hyper-active creators whose content entirely constructs the reality that the P50 users consume.

The P95 Whale generates the vast majority of your business value. They are the 5% of users who drive 80% of your revenue, 80% of your content, and virtually 100% of your platform’s network effects.

Because their usage volume is exponentially higher, their UX needs are the exact opposite of the P50 Tourist. The median user needs explanation; the P95 Whale needs **acceleration**.

_Power users should be encouraged to use the product even more. (NotebookLM)_

Power users tolerate initial friction if it yields long-term efficiency. They are actively frustrated by “simple” step-by-step wizards that slow them down. For the P95 user, you must design for unbounded utility and flow. They require keyboard shortcuts, bulk editing capabilities, API access, reusable templates, macros, and deep customization.

Furthermore, service quality and system performance _must_ be judged by the P95 workflow, not the median. The median user rarely hits edge cases. The P95 Whale will find every single weakness in your system. They will expose your slow database filters, your brittle import functions, and your missing audit trails. If your system experiences tail latency, where the 95th percentile of response times spikes to unplayable or unusable levels, your most valuable users are the ones suffering the most.

When a Whale complains about a missing advanced feature, do not dismiss it as an “edge case.” In a heavy-tailed distribution, the edge case is the economic center of gravity.

Power users matter for another reason: they are often early indicators of where the market is going. They hit edge cases first, invent workarounds first, and reveal which “advanced” features are quietly becoming core workflows. In that sense, the tail is not just today’s revenue concentration. It is tomorrow’s roadmap showing up early.

Finally, you must design defenses against the **Negative Whale**. The same power-law dynamics apply to resource drains and bad actors. A tiny fraction of extreme users can generate the vast majority of your server costs, support tickets, or community toxicity. In social platforms, catering entirely to hyperactive users without moderation can create an intimidating, insular culture that repels P50 Tourists. Your progressive disclosure and system limits must not only empower the positive Whale, but also smoothly constrain the extreme edge-case user whose behaviors degrade the experience for the masses.

# The “Tale of Two Cities” Design Strategy

If the P50 user needs a tricycle and the P95 user needs an F-16 fighter jet, how do you design a single application?

The answer is a **Layered Interface** featuring **Progressive Disclosure**. You must embrace a *Tale of Two Cities* strategy. A flat, uniform interface will underserve both groups: it will be too intimidating for the median user and too restrictive for the power user.

**1\. Build the Simple On-Ramp:** The surface of your product must be optimized for the P50 Tourist. The default state should be clean, guided, and focused entirely on the 20% of features that drive 80% of standard usage. Assume the user has zero attention span and zero desire to learn your software’s underlying architecture. Hide the settings. Hide the advanced configurations. Make the primary call-to-action blindingly obvious.

**2\. Excavate Deep, Uncapped Wells of Value:** Beneath that simple surface, you must engineer deep, uncapped functionality for the P95 Whale. As users demonstrate mastery (indicated by crossing specific thresholds of usage volume or session frequency), you progressively reveal advanced capabilities.

Progressive disclosure works best when it is triggered by evidence, not by menu sprawl. Do not ask novices to self-identify as advanced. Reveal power features when behavior shows readiness: repeated use, larger batch sizes, shortcut adoption, recurring tasks, or attempts to export and automate. The cleanest expert experience is often the one that stays out of sight until the moment it becomes useful.

Do not put advanced bulk-editing tools on the main dashboard; make them instantly accessible via a Command Palette (e.g., Cmd+K) that power users can trigger with muscle memory. Allow Whales to build *on top* of your product. In an enterprise AI tool, the median user needs a simple text box to type a quick prompt; the P95 user needs to save reusable context windows, create shared prompt libraries, and string together multi-agent workflows.

**3\. Decouple Time from Monetization:** In unbounded categories (like gaming, creator tools, or advanced SaaS), you must design UX loops that allow for infinite investment. If a Whale wants to spend 6 hours a day and $1,000 a month in your ecosystem to express their mastery, status, or fandom, your interface must seamlessly encourage that. Do not put artificial friction in front of a Whale who is trying to give you money or generate highly engaging content. The design goal is not endless activity for its own sake, but unbounded utility. Let expert users create more, customize more, automate more, and advance farther without making the novice path heavier.

**4\. Bridge the Gap (Fattening the Tail):** The ultimate goal of product design in a heavy-tailed ecosystem is to “fatten the tail.” You want to build pathways that pull the most motivated P50 users up the curve toward P95 status. This is where UX gamification, algorithmic recommendations, and habit-forming design loops come into play. A mechanic like a “daily streak” (as seen in Duolingo or Snapchat) is a UX bridge specifically engineered to turn a sporadic P50 user into a habitual P95 user.

Once you accept a heavy-tailed product, a new question becomes central: *can you manufacture your next Whale?* The key metric is not only the size of the tail, but the graduation rate into it. Track what percentage of P50 users become P75, what percentage of P75 become P95, and which behaviors predict the jump. A strong product does not merely harvest power users; it teaches, rewards, and scaffolds the making of new ones.

Generative AI offers a new mechanism for tail-fattening: **intention translation.** By allowing P50 Tourists to state their goals in plain language, helped by [prompt augmentation features](https://www.uxtigers.com/post/prompt-augmentation), AI agents can execute the complex workflows previously reserved for P95 experts. When an AI automatically generates a macro, writes a SQL query, or builds a pivot table based on a conversational prompt, it effectively raises the median user’s output to power-user levels without requiring them to overcome the traditional UI learning curve.

**5\. Reconcile the Buyer vs. the User:** In B2B enterprise software, the economic buyer (an executive or manager) is frequently a P50 Tourist who rarely logs in, except to check high-level ROI dashboards. While your product must deliver unbounded complexity for the Whale who uses it daily, your reporting and administrative interfaces must be radically frictionless to satisfy the Tourist who actually pays for it. If your interface caters exclusively to the Whale’s complex workflows, it may overwhelm the executive during a sales demo and cost you the contract.

_Aim to “fatten the tail” by moving the most motivated casual users up the value scale until they eventually become Whales. (NotebookLM)_

## Pricing Strategy

P95/P50 is a natural “fairness lens” for pricing: If usage is only mildly skewed (say P95/P50 ~ 2–5), flat-rate plans are simpler to understand. If usage is sharply skewed (say 20×+), a flat price subsidizes heavy users, especially for AI tools where inference tokens are expensive, so it’s better to have variable pricing.

_If P95/P50 is low, flat pricing is often best. If P95/P50 is high, charge extra for heavy use. (NotebookLM)_

## Churn Analysis

**Churn analysis must weight user segments by their usage ratios**, recognizing that losing a 95th percentile user costs significantly more than losing a median user. Losing a heavy enterprise user can remove far more workflow volume, advocacy, and product feedback than losing several median users. Losing a single high-productivity developer reduces team output by the equivalent of losing 17 average developers, making employee retention a critical priority.

In social media, the 550× following ratio implies that losing a major content creator reduces network value and engagement equivalent to losing hundreds or thousands of median users.

Retention strategies should **prioritize high-volume users** with dedicated support, advanced feature roadmaps, and community recognition, while automated onboarding suffices for median users. The **30-day churn threshold** is critical in mobile apps, where over 95% of users churn after 30 days, concentrating the retained user base increasingly toward high-engagement power users and inflating apparent 95th/50th ratios among survivors.

# Redesigning Your Dashboard and Your Mindset

The era of the “average user” must end. Averages conceal the truth of participation inequality. Averages hide the fact that your product's survival rests on the shoulders of a hyper-active 5%.

_Forget the average. It should not be the front and center of any dashboard used to drive product strategy. (NotebookLM)_

Do not let the mean dominate your dashboards. Keep it for finance or capacity planning if needed, but do not let it stand in for user reality. For product decisions, track the distribution: P25, P50, P75, P95, and, where it matters, P99. Plot the histogram on a log scale. Watch how the tail grows, compresses, or migrates after each major change. Ban the arithmetic mean and insist on seeing the full distribution.

_Design for divergence: it’s real. However, depending on the magnitude of the P95/P50 ratio, your exact strategy should differ. (NotebookLM)_

Monitor your P95/P50 ratio relentlessly:

- If your P95/P50 ratio is small (2x to 5x), you are building a bounded utility product. Focus on broad usability and frictionless task completion.
- If your P95/P50 ratio is massive (20x, 50x, or infinite), you are managing a power-law ecosystem. You must obsess over your Whales. You must give them the advanced tools, the API endpoints, and the uncapped progression systems they crave.

Stop designing a mythical middle ground that pleases no one. Acknowledge the profound behavioral chasm between the casual masses and the obsessive elite. Design a welcoming lobby for the P50 Tourist, but build an entire playground for the P95 Whale. Because in the digital economy, the Whales aren’t an edge case: they pay the bills.

**I made a short** [**explainer video about this article**](https://youtu.be/PwwzDc_l6zE) **(YouTube, 7 min.).**

_Infographic summarizing this article. (NotebookLM)_
