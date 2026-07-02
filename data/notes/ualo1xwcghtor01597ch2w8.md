
https://css-irl.info/my-browser-support-strategy/

# Testing

There is no substitute for real-device testing, so if you have access to a device lab you should absolutely use it. At the very least, aim to test on a few different devices if you can get hold of them. Issues with touch interaction, for example, will only become apparent if you’re using an actual touch-screen device.

## Testing platforms

If you can’t test on real devices (and plenty of companies don’t have the budget to keep a well-stocked device lab), online testing platforms such as [Browserstack](https://www.browserstack.com/) and [LamdaTest](https://www.lambdatest.com/) enable us to test on a range of platforms and devices. Some of these platforms provide cheaper emulator options, but I would urge you to use the real-device option if you can, as they will help you catch issues that aren’t replicated in emulators. They may be more expensive, but can help you prevent more costly issues arising if a bunch of customers can’t access your site!

## Which browsers to test?

With the thousands of different devices, operating systems and browser versions, it’s clearly impossible to test in every possible environment! So which ones should you test in? I find the [Statcounter](https://gs.statcounter.com/browser-market-share) website to be very useful here, as it shows the most-used browsers over the course of a year. You can filter by year, date, platform and region: If you’re making a website for Trowbridge town council in the UK, for example, the UK stats are probably going to be far more valuable to you than the worldwide ones.

The site also lets you specifically check the stats for [browser versions](https://gs.statcounter.com/browser-version-market-share), which is what I find most useful for testing. As a rule of thumb, I aim to cover at least the past two years of the most popular listed browsers with my testing, plus a couple of older browsers/devices — particularly versions of Safari that may be running on older devices.

If you’re working for a client, and you’re in a position to do so, it might be worth coming up with a written agreement that sets out explicitly how far back you intend to test, and what they can expect from browsers that don’t support all the features (versus what constitutes a bug). Educating clients about progressive enhancement could save quite a lot of time and explanation down the line, when they’re reporting “bugs” that are in fact fallbacks for older browsers!

## Other ways to test

In addition to cross-browser testing, there are some other methods we should consider when testing our websites:

- **Keyboard navigation** – Many people use a keyboard instead of a mouse. Can you navigate the website using only your keyboard? Are focused elements apparent?
- **Screenreaders** – People with visual impairment might use a screenreader to browse the website, which reads the content of the page. MacOS has a built-in screenreader, [VoiceOver](https://www.apple.com/voiceover/info/guide/_1121.html), and Chromebooks include [Chrome Vox](https://support.google.com/accessibility/answer/7031755?hl=en). (I definitely need to get better at testing with screenreaders!)
- **Zooming** – Plenty of users (myself included!) increase the zoom level in their browsers. Try zooming to at least 15%. Does the font size increase as expected? Does the layout break?
- **Reduced motion** – Users can set a preference for reduced motion at OS level. Does your website [respect their motion preferences](https://www.smashingmagazine.com/2021/10/respecting-users-motion-preferences/)? Can they pause animations that might be distracting, or worse, trigger cognitive issues?
- **Accessibility tools** – Tools like [Axe](https://www.deque.com/axe/) scan you webpage and check for accessibility issues (such as missing alt text, colour contrast and semantic markup) that would be time-consuming to check manually. It’s worth running your site through one of these tools to catch issues that might otherwise go unnoticed.

This list is by no means exhaustive, but should give you some things to think about when you’re next testing your website. Remember, by building with progressive enhancement, we can aim to reduce the number of issues raised by testing, and provide an experience that accommodates everyone.
