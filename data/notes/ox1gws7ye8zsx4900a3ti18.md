
> https://arnon.dk/why-you-should-separate-your-billing-from-entitlement/

Building your own entitlement service is key for supporting a modern, flexible SaaS product.

Whenever I read about billing systems, there’s a lot of talk about the billing aspects but not so much around entitlements. In the spirit of sharing, and since I haven’t found any good articles about it, I decided to tell you why we designed our own entitlement system at [Pleo](https://www.pleo.io/).

But first:

## What is an entitlement?

If you’re a pedant, look away because you may not like these definitions.

> **An entitlement is a customer’s access to a specific feature or product, within a given plan.**

The question of just _how_ a feature entitlement relates to the plan can be kind of difficult to explain, so here’s my attempt:

[entitlement](https://i0.wp.com/arnon.dk/wp-content/uploads/2022/02/image.png?ssl=1)

Composition of pricing and feature entitlements

- 1 – The **plan level**: Lots of products, and primarily SaaS products, include different plans or plan levels. You’ll also commonly see about 3 levels.
- 2 – **Payment terms** – e.g., “monthly”, “yearly”. These could change the entitlements, but that is a bit unusual.
- 3 – a set of **entitlements** that make up this plan or tier. These would commonly be called features, products, or services.
- 4 – **Entitlement limits** – adjacent to controlling which features are included, an entitlement limit places a specific limit on some capabilities.
- 5 – **Geographic variations** – not all features are available in all geographies, so some features may be limited to a specific market even within a specific plan level.
- 6 – **Entitlement variation –** a variation of the service-level of a feature. For example, you may only get basic support with some plan levels, whereas a higher plan level would include a dedicated account manager.

---

## Why entitlements matter for SaaS companies

If you lay your products out just like I did in the example above, you may not need to care while things are simple and small.

At Pleo, our plans are a bit more complex, but the general principle is mostly the same. In the past, we could get away with hard-coding checks, like this:

```
if plan == 'gold' then show_feature() else do_nothing()
```

In that horrible pseudocode, the “Gold” plan levels get all features, while lower levels will not see these more premium features.

[The classic flow for checking a customer’s entitlement goes through checking for the plan, and then matching features. Responses are in yellow.](https://i0.wp.com/arnon.dk/wp-content/uploads/2022/02/image-5.png?ssl=1)

Overlaying the potential upgrades isn’t too hard either. _“Want to use feature 4? Upgrade to our Silver plan!”_. Easy peasy.

_Or so it may seem._

### Things get complex when changes happen

Suppose one day you want to modify your basic level to remove a feature that costs too much to be valuable. Now you must go through all places in your codebase and modify these hardcoded checks.

Not only that, some of your customers may rely on this feature and won’t accept it being removed. If you remove these hardcoded checks, there is no sane way to let a subset of customers keep this feature once removed.

> **Pro tip: never hardcode customer names or IDs in your system.**

You are faced with either force-upgrading them, or making another plan level that includes this feature, effectively “grandfathering” them into a plan that can’t be selected. That statement _alone_ is enough to make anyone who’s worked on billing shiver with disgust.

## Why you should separate your entitlements from billing

So herein lies the problem: if you ever want to make any change to your company’s offering, or if you find yourself expanding to new territories, you really should have a separate mechanism to handle entitlements.

In blunt terms:

1. **If you will change what features are included in a plan**, you should have a separate entitlement system.
2. **If you think you won’t want to force customers onto new plans**, you should have a separate entitlement system.
3. **If some features are optional add-ons**, you should have a separate entitlement system.
4. **If you ever hope to expand to new countries and markets**, you should have a separate entitlement system.
5. **If you want to let customers experience features separately from their billing status**, you guessed it… You should have a separate entitlement system!

With an entitlement system, you manage each feature’s business logic in one central system, instead of in your applications.

Using an entitlement service doesn’t do away with the billing system. This is a distinctly different concept, even though it seems semantic.

You probably still need to know if the customer has paid and what price plan they paid for, what their billing status is (_paid_ or _delinquent_), what phase they’re in (like _in trial_ or _evergreen_) but now you’re letting the entitlement system decide if the user should gain access to features in the system.

[Responses in yellow indicate which features a user may have enabled, and which are possible as paid upgrades.](https://i0.wp.com/arnon.dk/wp-content/uploads/2022/02/image-6.png?ssl=1) Please excuse the crude psuedo-code.

### What should an entitlement system know?

This centralised system can contain answers for lots more combinations:

- For a specific user on a plan, what limits are there?
- For a specific user, what features should there be regardless of what plan they’re on?
- For a specific user on a plan (i.e., a user on the gold plan), what features are there?
- For a user on a plan in a specific country (i.e., a user on the gold plan in Finland), what features are there, and which upgrades are possible?
- For a specific customer, are they in their _trial_ phase, or an _evergreen_ phase?
- For a very specific user on plan, in a country (i.e., a grandfathered account who used to be on the silver plan, in Finland, which has extra features), what features are there?
- … and potentially more variations, depending on your setup.

---

## A modern entitlement/billing architecture – my top 6 tips

[The modern billing architecture offloads the business logic into the entitlement system, instead of the front-end or the application.](https://i0.wp.com/arnon.dk/wp-content/uploads/2022/02/image-4.png?ssl=1)

1. **Your modern application should rely on an entitlement service, instead of the billing system.** The requests should go to the entitlement system, and then to the identity systems and billing systems, to understand a customer’s state.
2. **You may be thinking “isn’t this causing a single point of failure?”** – and yeah, you’re right. It is. But it’s not worse than checking the billing system directly. Any system can be down.
3. **Have sane fallbacks for downtime.** In case the entitlement system (or a downstream system) fails, you should have some sane defaults. You may not want to prevent access entirely, but you probably shouldn’t allow a customer to make changes that they won’t be able to undo once the system is fully functioning again.
4. **Plan for overrides.** Your entitlement service should be able to overlay or override any entitlement, should the need arise. For example, you may want to allow a customer that has not paid to access the system for a short duration, without restarting the billing relationship.
5. **Plan for the future**. Sometimes you know about a future change well ahead. Your system should be able to handle a future change without modifying the current status. By setting a `valid-from` and `valid-until` date, you can safely switch entitlements at a future time, while maintaining the current status-quo.
6. **There is no 6.**

---

## The outcomes of having a separated entitlement system

**We can now launch features without redeploying.** Instead of going through hundreds of lines of code, altering behaviour, and then redeploying our software – we schedule it with our entitlement service.

**We can now plan for feature launches by scheduling the entitlement to go live for a specific market at a specific time-of-day.** It has actually also partially replaced tools like LaunchDarkly (which was overkill for some of our use-cases).

**Changing entitlements takes minutes, and is entirely predictable.** As our company decided to expand to new markets, we found ourselves relying heavily on our entitlement service. We know exactly when things go live. Plus, we have a full view of all features and entitlements across all plans and geographies.

Anyway, I hope you found this helpful. If you’d like to hear more or have any questions, do reach out!
