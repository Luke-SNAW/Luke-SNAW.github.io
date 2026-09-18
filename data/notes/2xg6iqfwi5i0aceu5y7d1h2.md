
> https://blog.turso.tech/what-the-heck-is-the-edge-anyway-a159a12f2412

Last week, we announced a new product, [Turso](http://chiselstrike.com/), that we described as “SQLite\* on the edge”. Although we tried our best to touch on the subject briefly in the [announcement post](https://blog.chiselstrike.com/announcing-chiselstrike-turso-164472456b29), one common question we still hear is “but what the heck is the edge anyway?”

Let’s face it: our industry has a penchant for buzzwords. As people try to differentiate themselves and establish their own relevance, oftentimes they try to do this by inventing and capturing terms that may or may not mean something.

I am old enough to remember when people tried to push things like [grid computing](https://en.wikipedia.org/wiki/Grid_computing) and [fog computing](https://en.wikipedia.org/wiki/Fog_computing). (Note that I am leaving NFT out of this because I have standards and won’t beat a dead horse.).

Ok, I will beat this one dead horse. But they deserve it.

So you would be forgiven for thinking that “The Edge” is just yet another such buzzword. Especially because the term’s confusion is made worse by the fact that:

- Two different slices of the industry mean two completely different things by edge.
- Oftentimes people conflate it with serverless (which had its own misconceptions).

In this article, I’ll explain what the edge is, and why you should care.

## The definition

Wikipedia defines [Edge Computing](https://en.wikipedia.org/wiki/Edge_computing) as _“a distributed computing paradigm that brings computation and data storage closer to the sources of data. This is expected to improve response times and save bandwidth”_

We spot the reason for the first confusion in this very definition: closer to _what?_ If it brings computation and data storage _closer_ to the sources of data, that is a comparison. If I have a database in us-east-1 and replicate it to us-west-1, is that the edge?

## The “far edge”, or “offline edge” (IoT)

When we started talking about a product for the edge, an old colleague of mine immediately sent me a message, questioning that what we were doing was not really the edge. This person has been working with “the edge” for years, and when talking to him, the confusion immediately became clear.

Developers working on IoT, mobile devices, point of sales, telecom, see “the edge” as something as close as possible to the devices themselves, potentially _inside_ the devices. When they talk about “pushing compute to the edge”, they are likely talking about compute that happens _inside_ the device.

One immediate characteristic of those deployments is that internet connectivity is either slow, intermittent, or barely existent (think airplanes, industrial controllers, etc). Compute and storage resources are not just reduced, in comparison with the cloud, but they are _severely_ reduced.

Because of these characteristics, this can be referred to as the “far edge”. A term I personally prefer is “offline edge”. This is the domain where [offline-first](https://offlinefirst.org/) solutions shine.

## The “near edge” or “online edge” (Web)

I could never convince my friend that there is “another edge”, and to this day he likely just thinks I have no idea what I am talking about. And in all fairness, as far as I know, the IoT folks got there first. So if they want to claim that theirs is the true edge, there’s very little I can do.

But the reality is that there is a growing and strong segment of the industry that uses the term edge to mean something else entirely. Those are web developers, deploying their applications to platforms like Cloudflare, Vercel or Netlify.

While “the cloud” may offer you a region “in Europe”, the edge will offer you multiple cities spread across Europe. Those edge locations are not as powerful and capable as cloud data centers, but they are still data centers. Technically they _could_ be as powerful as any other cloud datacenter, but this wouldn’t be economical.

[A map of the world showing big datacenters (the cloud), connected to smaller ones (the web edge)](https://miro.medium.com/v2/resize:fit:700/0*N1mjKP_w1Jaf4Zs3)

The Web edge: lowering response times to applications, but still mostly online

## The missing piece: The Data Edge

For the IoT edge, each terminal device will bring its own local storage. But for the Web Edge, things are different. Bringing data to the edge presents its own challenges.

Compute and storage are both present in the definition of edge computing, but they are very different in nature. Compute is nimble, and can be easily moved anywhere. Data is heavy, and moving it has a cost. Compute is unencumbered by regulations, and can happen anywhere. Data is protected, and has to be treated differently depending on the jurisdiction.

For this reason, companies targeting the edge have so far focused most of their efforts on compute, like edge _functions. But bringing compute to the edge only solves half the problem, especially if you’re making calls to a centralized database somewhere in a far away cluster. You end up with as much, or potentially more, latency than if you had just hosted all your compute in a traditional centralized cloud hosted location._

One way that developers move data to the edge is to cache it on end users’ devices. This works well for offline use, but caching and synchronization are hard things to get right, and it doesn’t solve many cases where fast access is required.

These data edge problems are exactly the ones that [Turso](http://chiselstrike.com/) aims to address.

## Is edge the same as serverless?

When companies like Vercel, Netlify and Cloudflare talk about the edge, they usually refer to “edge functions”. This leads developers to conflate “edge” and “serverless” as if they were similar or the same. With serverless, although there are servers somewhere, developers don’t think in terms of servers that need to be configured, scaled up, and scaled down. They think in terms of _functions_ that get executed — they are just deploying code and expecting the cloud provider to handle the rest.

This paradigm goes very well with edge computing: since we are assuming there are fewer resources available, allowing potentially wasteful general purpose compute is less enticing. Constraining what the developers can do (through functions and massive multi-tenancy) allows for better utilization and resource packing.

Another reason is historical: those platforms were initially simple CDNs, handling static assets. Over time, those CDNs started to increase in functionality, and become _programmable CDNs_.

[The evolution of CDNs, with programmability giving rise to the edge. Data edge is the next frontier](https://miro.medium.com/v2/resize:fit:700/0*O3_FtfNQjSYe5P1r)

CDNs are gaining functionality, effectively evolving into the Edge. The data edge is the next frontier.

But companies like Fly.io are also edge companies, and they operate on a different model. You can deploy a container abstraction with a long-lived application of your choice, and because they make that application available in many regions, they are also an edge player.

## Is the edge “just X”?

Every time a new term comes along, people get too far in the weeds about whether something is truly “novel” or not. When the cloud was born, lots of people didn’t see value because it was “just renting servers”. It was not: the ability to rent those servers in seconds instead of weeks and give them back just as easily changed how businesses operated.

I will always remember a coworker of mine that didn’t see any value on slack because “it was just IRC”, and my favorite to this day is still this timeless Hackernews [comment](https://news.ycombinator.com/item?id=9224) about Dropbox:

[A screenshot of Hackernews, where a user complains that Dropbox is nothing new, listing a host of technologies that can be put together to implement it “at home”](https://miro.medium.com/v2/resize:fit:700/0*RB4E65IOQVXNZAsp)

I used Dropbox because I stopped reading after “curlftpfs”.

So is there something really transformative about the online edge? Yes!

Before the online edge, you could build applications that span multiple locations, the same way you could have built elastic applications before the cloud, by being painfully precise about geographical provisioning, routing, placement and execution.

What the edge allows you to do now is _code as if none of that matters_, as if the world is one, and set policies about what is allowed to happen where. The edge allows truly global applications to be built transparently, without investing time and money in explicitly setting up and managing a global presence.

## The second criteria for relevance

The edge fits the first criteria of whether or not something is “just X” or a new concept that is here to stay: it does transform the way in which developers architect their applications. The second criteria is whether it solves a distinct business problem.
