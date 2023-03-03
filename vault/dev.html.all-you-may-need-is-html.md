---
id: 5oywa6mz3c9g33telcdhq99
title: All You May Need Is HTML
desc: ""
updated: 1677803183831
created: 1677802759054
---

> https://fabiensanglard.net/html/index.html

## All you may need is HTML

Readers occasionally request which static HTML generator is used by `fabiensanglard.net`, and if they can take the same stylesheet/ fonts to start their own blog. I usually send back the whole 134 lines of `gen.php`[^1] and invite them to copy whatever they need to get started[^2].

I also add a, somewhat unsolicited, piece of advice. Writers who are getting started may not need any of this stuff. All you may need is HTML.

## The bare minimum

Starter pack I recommend.

1. A host for your `index.html` files ➔ Hostgator $33/year plan.
2. A DNS pointing to the host ➔ Hostgator for an extra $12.95/year.
3. Editor to write `index.html` files ➔ Sublime Text[^3] on all platforms.
4. Tool to upload the `index.html` to the host ➔ Cyberduck[^4] on Win/Mac and sshfs on Linux.

## Why you may not need css

The fluff does not really matter much. Several articles in my hall of fame use the default font `Times New Roman` and blue hyperlinks.

- [The 3D Software Rendering Technology of 1996's Thief: The Dark Project](https://nothings.org/gamedev/thief_rendering.html) (nothings.org).
- [Lode's Computer Graphics Tutorial](https://lodev.org/cgtutor/raycasting.html) (lodev.org).
- [The Truth about Visplane Overflows](https://soulsphere.org/mirrors/www.rome.ro/lee_killough/editing/visplane.shtml) (leekillough.com).

Check out `nothings.org`'s beauty. It has everything it needs[^5]. An author, a date, and awesome content for someone interested in real-time 3D.

Another example is Paul Graham's straight-from-1998 layout [website](http://www.paulgraham.com/) which does not prevent him from being a highly-regarded author.

## The problems css solves

If you can stick to the same style long enough and also write articles for long enough, your style sheet can become your brand. Some people will love your style and some people will despise it. Mostly css appeals to our vanity and ego[^6].

## Why you may not need a website generator

By starting with a markup based generator, you rob yourselves of the opportunity to learn the core technology running the whole internet. Instead you will learn to use a layer built on top of it with little to no re-usable knowledge. Inevitably, you will want to do something the framework did not forecast and will come up with convoluted ways to do it anyway.

Additionally, depending on how long you will write and how often you do it, setting up a generator may be counterproductive[^7].

## The problems a generator solves

Pages on this website used to be authored with pure HTML. Now a script, `gen.php`, turns `src.php` files into `index.html` files. There are three reasons for that.

1. I like to use drawings and screenshots but `img` tags trigger layout reflow. The PHP script generates `img` tags including the `width` and `height` of the `src`. By integrating these values in the markup, the browser layout engine can reserve space for an image before it is downloaded.
2. I prefer footnotes to inline hyperlinks because they avoid the underline marker. These can be done client-side with Javascript but I prefer to do it once server-side.
3. Articles can be sandwiched with header/footer automatically which allows to tune all articles at once. This is by far the most appealing once you have a lot of content.

If #3 is all you need, you may be better off using a recursive sandwich bash script turning `src.html` into `index.html`.

There used to be a fourth reason. To save bandwidth, `img` were presented within a `picture` tag so browsers supporting it could use `webp` while others fell back to `png`. Automatic webp conversion and `picture` generation are no longer needed[^8] since Safari added `webp` support in late 2020.

## Why you may not need custom fonts

Custom fonts are a waste of bandwidth and a visual annoyance because they come with one of three evils called latency, FOUT, and FOIT[^9]. If you don't need monospace, go with a websafe font[^10]. `Verdana` is a great choice. It looks fantastic and ships on all major OSes so your website will look the same on all platforms.

## The problems custom font solves

If you want to use monospace, a custom font may be useful. The one monospace safefont, `Courier New`, is not legible. Originally this website's `font-family` simply requested `monospace`. This approach resulted in varying reading experience depending on the OS. Windows browsers got `Consolas`, Linux users got `DejaVu Sans Mono`, and macOS people got `Courier`. Using a custom `DejaVU` makes the reading experience consistent (at the, barely tolerable, cost of FOUT).

## The problems that everything else creates

The more tech you add to your stack, the more maintenance work will be required to keep it up and running. Recognizing cycle eaters helps to not waste motivation on overhead.

- Avoid CMS. Stuff like WordPress have to be updated constantly to patch vulnerabilities[^11].
- Avoid anything requiring a database. It is annoying to backup and a pain to migrate. This website used to be hosted by `asmallorange`. When I became dissatisfied, all I had to do was to open an account on `hostgator`, upload my `html` files, and change the DNS entry.
- Avoid comment systems. Custom ones will be spammed. Disqus-like will need key maintenance and could be suggested to term changes.
- Avoid external dependencies. Stuff like analytic engines can 404, 503, or become sluggish.

[^1]: [fabsite.zip](https://fabiensanglard.net/html/fabsite.zip)
[^2]: Also, copying a CSS is missing out on a creative journey.
[^3]: [Sublime Text](https://www.sublimetext.com/)
[^4]: [Cyberduck](https://cyberduck.io/)
[^5]: [0x10 rules](https://fabiensanglard.net/ilike/index.html)
[^6]: Too strong a statement. Spacing and black hyperlink (vs blue) can help legibility.
[^7]: [Is It Worth the Time?](https://xkcd.com/1205/)
[^8]: [Can I use WebP image format?](https://caniuse.com/webp)
[^9]: [Fighting FOIT and FOUT Together](https://css-tricks.com/fighting-foit-and-fout-together/)
[^10]: [CSS Web Safe Fonts](https://www.w3schools.com/cssref/css_websafe_fonts.php)
[^11]: Saddest WordPress casualty is [dadhacker.com](http://www.dadhacker.com/blog/).
