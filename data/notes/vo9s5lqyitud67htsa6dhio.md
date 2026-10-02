
> https://opuszine.us/posts/your-websites-urls-can-should-be-beautiful

The key to making a beautiful URL is finding a balance between brevity and clarity.

It’s safe to say that no one ever gives a second thought about URLs. Or a first thought, for that matter. We click on link after link, and never think to look at the browser’s URL bar. We just assume the URL is valid and will take us where we want to go. Indeed, browsers like [Chrome](https://blog.chromium.org/2020/08/helping-people-spot-spoofs-url.html) and [Safari](https://apple.stackexchange.com/questions/371473/always-show-full-url-in-safari-address-bar) have even taken steps to hide URLs entirely. Which is a mistake, because there’s something beautiful and worth appreciating about a well-crafted URL.

Back in the day, however, it wasn’t uncommon for URLs to look like gibberish:

- `domain.com/blog/archive.php?cat_id=25&page=4`
- `domain.com/products/view/?product_id=65847135468`
- `domain.com/forums/view_topic.phtml?topic_id=25874`

The problem with these “ugly” URLs is that they’re written for web _servers_ more so than web _surfers_. No matter how long you stare at those URLs, you’ll never find any real clues concerning their purpose or destination, like which product is associated with the ID of `65847135468`. The only way to find out is to click on the link and hope it’s what you’re looking for, which can be frustrating, confusing, and time-consuming.

Thankfully, you’re more likely to see URLs like these nowadays:

- `domain.com/blog/category/music/page/4`
- `domain.com/products/view/awesome-product-title`
- `domain.com/forums/topic/best-blues-albums-of-2023`

“Pretty” URLs like these — which are the default in CMSes like WordPress — can provide useful, human-readable context that gives you an idea of what you’ll find _before_ you go there. For example, based on that forum topic’s “slug” — `best-blues-albums-of-2023` — it’s reasonable to assume that you’ll find some decent music recommendations should you go there.

Put simply, “pretty” URLs make your site _more accessible and user-friendly_ while also providing some [SEO benefits](https://moz.com/learn/seo/url). But even if your CMS is configured to create “pretty” URLs, you can still make them better — and more beautiful.

---

## Brevity vs. Clarity

The key to making a beautiful URL is _finding a balance between brevity and clarity_. In other words, a good URL is short but not so short as to obscure what it’s pointing to. Put another way, a good URL contains enough information about its related resource to be useful, but not so much information that it drags on and becomes unwieldy. (Suffice to say, this is often more art than science.)

Consider [Derek Sivers](https://sive.rs/)’ site. As befitting the stark design, its URLs are almost comically short:

- `sive.rs/u`
- `sive.rs/pnt`
- `sive.rs/shc`

Looking at that first URL, you’d probably never guess that it’s for his book [_Useful Not True_](https://sive.rs/u) (hence the `/u` slug). Sivers offers [several reasons for such short URLs](https://sive.rs/su), ranging from practical (they’re easier to remember and share) to aesthetic (they look nicer). While I respect and echo Sivers’ desire for efficiency and [reducing digital pollution](https://sive.rs/polut), his site’s URLs go too far to one end of the spectrum; they’re certainly brief but not terribly clear to anyone but him. (Also, as his site grows over time, I wonder if he’ll still be able to remember all of its URLs off the top of his head.)

Some URLs can be very short. It’s pretty standard to see URLs like these on many sites:

- `domain.com/about`
- `domain.com/contact`
- `domain.com/faq`

You see `/about` or `/faq` and you know, almost instinctively, that those are for the site’s “About Us” and “Frequently Asked Questions” pages, respectively. They don’t need any more clarity or context. Indeed, it almost feels wrong to see longer versions of those URLs:

- `domain.com/about-us`
- `domain.com/contact-us`
- `domain.com/frequently-asked-questions`

These longer versions are technically less ambiguous than their shorter counterparts, but unnecessarily so, and they now look ungainly and unwieldy — especially if they have any sub-pages. Of these two URLs, which looks better?

- `domain.com/about/team`
- `domain.com/about-us/our-team-members`

The answer’s pretty clear to me.

---

## Let’s Beautify Some URLs

So what’s the best way to create beautiful URLs while still keeping in mind the balance between brevity and clarity? Here are some tips that I always keep in mind for any site that I’m working on, be it _Opus_ or elsewhere.

### **1. Use as Few URL Segments as Possible**

Every `/` in a URL denotes a segment, which helps identify the site’s structure. Although many sites run on a database rather than a filesystem, a URL’s segments imply a hierarchical structure akin to the folders and files on a server. To keep URLs short, you naturally want to keep the number of segments down to a bare minimum. Doing so forces you to _really_ think about how your site is structured. Segment-heavy URLs like these might be necessary:

- `domain.com/about/locations/usa/nebraska/lincoln/havelock`
- `domain.com/clothing/movies/star-wars/shirts/short-sleeve`
- `domain.com/catalog/toys/robots/transformers/autobots/dinobots`

I bet, however, that you could find some ways to simplify and shorten them, thus making the site easier to navigate and comprehend. (**Note:** This touches on site structure development and content organization, which could be its own series of blog posts.)

When URLs contains lots of segments, I often find that the resulting pages’ content is so thin and spread out that it’s hard to justify. There may be some SEO benefits to such an approach, but as a user, it’s annoying to come across threadbare pages when it would be more convenient were all of that content collected into a single page.

Returning to the above URLs, does the organization really have so many locations in Lincoln that [Havelock](https://www.lincoln.org/listing/havelock/2795/) needs it own URL? Are there so many locations in Nebraska that Lincoln needs its own page/section? Could you get away with something as concise as `domain.com/locations/havelock` instead?

### **2. Slugs Don’t Need to Match Titles**

I briefly touched on this earlier when I explained why `domain.com/about` is better than `domain.com/about-us`. The `-us` can be assumed and is therefore unnecessary even if the page’s title is “About Us.” Building on that, look at these blog post URLs:

- `domain.com/blog/this-is-my-very-first-blog-post`
- `domain.com/blog/i-finally-saw-the-shawshank-redemption-and-heres-my-review`
- `domain.com/blog/ive-been-reading-comic-books-recently-and-these-are-some-of-my-favorites`

Chances are, these URL slugs are basically the post titles but URL-ified (e.g., converted to lowercase, stripped of punctuation, with spaces replaced by dashes). If you clicked on that first URL, it’s a pretty safe bet that the post’s title would be “This Is My Very First Blog Post.” But just because that’s the title, that doesn’t mean that needs to be the slug, too. You can shorten and simplify a post’s slug while still capturing the spirit of its title:

- `domain.com/blog/very-first-blog-post`
- `domain.com/blog/shawshank-redemption-review`
- `domain.com/blog/some-recent-comic-book-faves`

One might argue that these simpler URLs lack the personality of the longer ones, and that might be the case. If you deem long, unwieldy URLs as intrinsic to your site’s brand, then by all means, keep using them. And if SEO is a concern, then make sure your URL still contains any relevant keywords.

For what it’s worth, I use this approach for all of my URLs, especially those for my [reviews](https://opuszine.us/reviews). Take, for instance, [my review of Slowdive’s latest album](https://opuszine.us/reviews/everything-is-alive-slowdive-2023-dead-oceans). The page title is “_Everything Is Alive_ by Slowdive (Review)” but this is the review’s URL:

- `opuszine.us/reviews/everything-is-alive-slowdive-2023-dead-oceans`

It’s unnecessary to have `review` in the slug since that’s already a URL segment. Thus, my review slugs follow this convention: release title, artist name, year of release, and publisher/label/studio. Which results in URLs like these:

- `opuszine.us/reviews/winks-kisses-20th-anniversary-deluxe-edition-airiel-2023-feeltrip-records`
- `opuszine.us/reviews/ergo-proxy-shuko-murase-2006-manglobe`
- `opuszine.us/reviews/saviour-machine-1993-intense-records`

There are some caveats, though. Self-released albums won’t have any label info in the slug, for example. And as you can see, this convention can result in lengthy URLs. But the goal is to make sure the user knows _exactly_ what’s being reviewed, which might not be possible if the slug was shorter or matched the post’s title exactly.

### 3. Stop with the Stop Words (Sometimes)

[“Stop” words](https://www.semrush.com/blog/seo-stop-words/) — which include “a,” “an,” “in,” “is,” “the,” and “was” — are words that don’t really add any value to a URL, particularly from an SEO perspective (though [they’re not a major factor](https://www.searchenginejournal.com/stop-words-in-url/464774/) one way or the other). They tend to be articles, prepositions, conjunctions, and pronouns. As such, it’s often possible to remove them to simplify a URL, as I’ve done in several of the above examples.

But remember, beautiful URLs _inform users and give them helpful context_. Which means there are times when [removing stop words can result in worse URLs](https://onlinemediamasters.com/why-you-shouldnt-remove-stop-words-from-urls/) by making them nonsensical and even misleading. Compare:

- `domain.com/blog/i-ate-my-family`
- `domain.com/blog/my-kid-annoying`
- `domain.com/blog/practicing-drums-hard`

To these versions with the stop words still in place:

- `domain.com/blog/i-ate-with-my-family`
- `domain.com/blog/my-kid-is-not-annoying`
- `domain.com/blog/practicing-drums-can-be-hard`

Those are two _very_ different sets of blog posts.

I’ll often remove all of the stop words from a slug and see what it looks like. If it’s nonsensical or misleading, then I’ll add one or two back in. That, or I might rewrite the title so that it doesn’t include as many stop words to begin with, which usually results in a simpler, more concise slug — and maybe even a better title.

### 4. Leave That Pretty URL Alone

Once you’ve settled on a beautiful URL and published your blog post, product, or page, _leave it alone_, even if a URL that’s ten times better comes to you in a dream that night. Save it for something else.

There’s a reason why they’re called permalinks; they’re supposed to be _permanent_. The web is already [too ephemeral as it is](https://opuszine.us/posts/building-webpages-that-last-lament-absent-websites), with sites disappearing and spreading link rot. If you absolutely must change one of your site’s URLs, then be sure to [add a “301” redirect from the old URL to the new one](https://www.semrush.com/blog/301-redirect-htaccess/). (There are several different types of redirects, but a “301” redirect indicates that it’s a permanent redirect, which alerts search engines to update their indexes.)

---

If you’ve made it this far, then first off, thanks for sticking with me as I ventured into the weeds a bit. Second, you might be thinking that this sounds like a lot of silly, pedantic work. After all, if your CMS is already generating “pretty” URLs, why stress about it? What’s the big deal if your site’s URLs aren’t as concise as they could be?

Functionally speaking, it probably doesn’t matter. But these recommendations are _all part of creating a well-crafted, intentionally designed website_, of taking pride in what you’re putting out onto the web and reducing digital pollution (to use Derek Sivers’ term).

[Optimizing your images](https://opuszine.us/posts/its-2022-yes-you-should-still-optimize-your-websites-images), [using semantic HTML](https://opuszine.us/posts/fellow-web-devs-lets-get-reacquainted-rule-least-power), and [avoiding dark patterns](https://opuszine.us/posts/donald-trumps-dark-patterns) all communicate that you care about your users’ experience, and so can crafting beautifully concise and context-rich URLs. Users may never (consciously) notice such efforts, but they’ll almost certainly notice their absence, even if they can’t quite articulate how or why.

I’ll grant that my penchant for beautiful URLs stems from the fact that I’ve always found URLs quasi-magical. You type `https://` into your browser’s URL bar followed by a string of letters, numbers, dashes, underscores, periods, and slashes, and you’re whisked away to another potential treasure trove of news, information, and resources.

URLs are like map trails, street signs, and incantations, all rolled into one. And if it’s possible to make them more efficient and aesthetically pleasing without sacrificing any utility or functionality, then I can’t really think of any reason why you shouldn’t take a few moments to do so.
