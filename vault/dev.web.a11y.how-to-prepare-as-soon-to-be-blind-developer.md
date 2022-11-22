---
id: d8dUQN3pq8S0thhP0q0pZ
title: How to prepare as soon-to-be blind developer?
desc: ""
updated: 1669098346429
created: 1644886721030
---

> https://news.ycombinator.com/item?id=30339187

Blind person here, happy to answer any questions. I'm speaking from the perspective of someone born blind, so whatever ends up working well for me might not work as well for someone just losing their sight, though I tried to take that fact into account.
The most immediate suggestions that come to mind are:

1. Learn to use a screen reader. You don't need an expensive one. NVDA on Windows, Voice Over on the Mac and Orca on Linux are the way to go. NVDA is probably the least quirky and easiest to find resources for. I'd recommend against Orca, while it can be used, we all know how tricky Linux on the desktop can get, and throwing a screen reader into the mix doesn't help.

2. Forget about the mouse. Screen reader users use the keyboard exclusively. Try disabling the screen too, many sighted users who practice with a screen reader end up relying on what they can see, which makes things more difficult.

3. Accept that inaccessibility is a fact of life, and it has to be worked around. Not all tools are accessible, and some are more accessible than others. If you're looking for an accessible IDE, Vs Code is great and constantly improving. Emacspeak exists, but I don't actually know anyone who uses it, and I know quite a few blind people in tech. Some things that you're now doing through a GUI are best done via the command line, Git is a good example. Programming tools usually aren't the problem, it's everything else that causes issues. Slack and Zoom work great, for example, but many smaller collaboration tools don't.

4. Not all areas of programming are equally accessible. I can't imagine a blind dev working exclusively on the front end, where there's a lot of CSS involved, and where you have to look at Figma designs and debug issues solely based on screenshots. Backend stuff is much more accessible, same with lower-level systems programming. Dev Ops is very much a mixed bag.

I'm happy to answer any further questions either here or via email, my HN username at gmail dot com.

---

I'm a Mac user these days, before that, it was Windows with WSL, Notepad++, Windows Explorer and remote VS Code for bigger projects. I use the command line a lot, but some things are best done with a GUI. I'm not a fan of command line editors, for example, as screen readers don't always deal well with TUIs. They can be used, but they bring their own set of headaches which I just don't want to deal with.
Updates definitely affect your workflow, you need to be careful about what updates you install. This is less of a problem with coding-related tools, but definitely a nightmare when mobile apps are concerned, for example. Web apps are even worse, as you can't avoid updates that completely break accessibility. I've heard stories of people getting in big trouble because a web app that was critical for their job suddenly had a UI overhaul and stopped being accessible. OS updates can cause trouble, in fact, Windows constantly breaking things with their forced updates was one of the major reasons why I switched to Mac OS. It wasn't even accessibility-related, most of it was basic stuff like sound.

---

No idea about Dropbox paper, but those tools are hard to make accessible, so I wouldn't be hopeful.
Google Docs works, there are two accessibility modes, none of which is enabled by default. The old, standard mode hides all content from screen readers and uses a built-in micro screen-reader that outputs whatever is needed to a live region, which your screen reader then reads. The newer one, called braille mode, actually shows you the content, only relying on ARIA when absolutely necessary. Both have their pros and cons, but I'd recommend using Braille Mode for most things, unless you run into use cases that the legacy mode handles better.

I've heard people say that some really advanced docs features have accessibility issues, but I haven't used it that extensively to confirm that.

As always, Etherpad, the open source / non-proprietary / privacy-friendly alternative boasts about being accessible but has so many a11y bugs that it's basically unusable. As always, markdown over git works better than any web-based solution ever could.

---

Switch to Emacs immediately. Emacs speak is extremely useful, and since Emacs can do anything (email, web, usenet, chat, edit docs, etc. etc. etc.) once you learn the keystrokes for forward/back word/sentence/paragraph/page/chapter it makes life MUCH easier. I'm not blind, but was a member of a linux user group who got asked to help out. I ended up installing and configuring it for the user, who was a grad student at the local university.

---

from https://news.ycombinator.com/item?id=22918980

You can definitely continue as a software engineer. I'm living proof. It won't be easy, especially at first. For a while it will feel like you're working twice as hard just to keep up with your sighted peers. But eventually, the better you get with your tools, you'll find you have some superpowers over your sighted peers. For example, as you get better with a screen reader, you'll be bumping the speech rate up to 1.75-2X normal speech. You'll be the only one who can understand your screen reader. You'll become the fastest and most proficient proof reader on your team. Typos will be easily spotted as they just won't "sound right". It will be like listening to a familiar song and then hitting an off note in the melody. And this includes code. Also, because code is no longer represented visually as blocks, you'll find you're building an increasingly detailed memory model of your code. Sighted people do this, too, but they tend to visualize in their mind. When you abandon this two dimensional representation, your non-visual mental map suffers no spatial limits. You'll be amazed how good your memory will get without the crutch of sight. Good luck. If you're a Mac user you can hit me up for tool recommendations.
