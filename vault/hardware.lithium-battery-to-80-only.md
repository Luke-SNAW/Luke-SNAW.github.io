---
id: phcdzo4gyx8xkivm6ilrot5
title: Charging a lithium battery to 80% only?
desc: ""
updated: 1700611472143
created: 1700611378401
---

> https://electronics.stackexchange.com/a/623375
>
> [How to Prolong Lithium-based Batteries](https://batteryuniversity.com/article/bu-808-how-to-prolong-lithium-based-batteries)

_When you run, you cover less distance by sprinting for a short time compared to running at marathon pace. Same goes for batteries._

The longevity of Li-ion batteries is greatly affected by a) how deep you discharge them and b) how full you charge them. Not in a linear way. The quantitative benefits or discharging the battery are out of the scope of this question (although if that is of interest, you can check out [this other question](https://electronics.stackexchange.com/questions/146623/how-deep-should-we-discharge-lithium-batteries-to-maximise-their-lifetime/146624#146624) \[disclaimer: I wrote the accepted answer\]), but they are universally recognized and it seems like the benefits of under-charging your battery are actually at least as important in the long run:

Using a reputable battery management application I use on my phone, I have observed how "cycles wear" varies vs "charging setpoint" and calculated the relative energy gain at the end of the battery life compared to 100% charging and discharging\*:
[![](https://i.stack.imgur.com/IHZ87.jpg)](https://i.stack.imgur.com/IHZ87.jpg)

As you can see, **charging to 80% instead of 100% multiplies by 4 the amount of energy the battery will have transferred to you over its life** - the only tradeoff being to compromise on how much energy you can get out of a full charge (big slices, small cake VS small slices, large cake). This also means you can use your battery for 4 times longer before it gets to the end of its rated life. Note the use of "rated life", because in practice batteries lose capacity as they age and get used, to a point they become unusable.

**If the above plot was flat, you'd be right**, charging at 80% the battery would be useless because we would charge it more often (less convenient) and it would not live longer. **But it's not, not even close.**

So, just like in a race, you have a choice: either run smart, or run fast. In practice "smart" would actually mean here that at times, you would have to charge at 100% to survive an intense day, but that in general you should charge it at a lower level.

It is generally recognized that 80% is a good compromise between convenience and life span. I think I remember that in satellites, the battery is generally designed to charge/discharge between a third and 2 thirds of its rated capacity to maximize its lifetime to 15+ years.

My general advice for maximizing the battery is **only use your battery as much as you need**, i.e. _charge it as often as possible, and as little as possible._ **If you need a rule of thumb, [stay within 30%-80%](https://batteryuniversity.com/article/bu-415-how-to-charge-and-when-to-charge).**

\*: This particular calculation assumes deep discharging, but although the benefits may be altered by (safer) more shallower discharging, the qualitative takeaway is the same. Note, also, that obviously this chart is not at all accurate below 50% (my app does not even give estimates below that) and probably not that accurate close to 50%. I believe it above 75% though.

[Example of scientific proof from the Battery University (e.g. Table 3).](https://batteryuniversity.com/article/bu-808-how-to-prolong-lithium-based-batteries)
