---
id: gxdmu6nba4j6r1lobzgen1e
title: Improved Process Isolation in Firefox 100
desc: ""
updated: 1652400041201
created: 1652399959656
---

- https://hacks.mozilla.org/2022/05/improved-process-isolation-in-firefox-100/
- https://news.ycombinator.com/item?id=31355857

---

This is a bit buried at the bottom, but:

> For Linux users, we removed the connection from content processes to the X11 Server, which stops attackers from exploiting the unsecured X11 protocol.

It's hard to overstate how much of a benefit this is in terms of security for those on Linux. Any application with access to the X11 socket effectively has the keys to the kingdom, because it can hijack other applications, including those running at higher privileges, at will. (There have been halfhearted attempts to address this over the years, but nothing that's been effective or widely adopted.) The only real solution for desktop app security on Linux is to forbid direct access to X11 entirely, and so it's a huge deal that Firefox is now able to do this.

In general, doing this sort of thing is a monumental undertaking for large applications like Firefox. Kudos to my former colleagues for pulling it off.

->
Scenario: evil.com wants to take advantage of a use-after-free in some DOM API to install a keylogger.
Before X11 isolation, it can: (1) get RCE in content process; (2) send events to your GNOME Shell to open a terminal; (3) send keyboard events to the terminal to download the keylogger, start it, and add it to some config file that makes it start automatically on future logins.

After X11 isolation, it will: (1) get RCE in content process; (2) get stopped because it can't send keyboard/mouse events to other applications anymore.
