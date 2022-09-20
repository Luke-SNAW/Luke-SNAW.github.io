---
id: sztm6rsffq1plexpw79y1s7
title: Why Your Website Should Be under 14kb in Size
desc: ""
updated: 1663543455041
created: 1663543270676
---

> https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/

Having a smaller website makes it load faster — that's not surprising.

What is surprising is that **a `14kB` page can load much faster than a `15kB` page** — maybe `612ms` faster — while the difference between a `15kB` and a `16kB` page is trivial.

This is because of the **TCP slow start** algorithm. **This article will cover what that is, how it works, and why you should care.** But first we'll quickly go over some of the basics.

## [What is TCP slow start?](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#what-is-tcp-slow-start)

TCP slow start is an algorithm used by servers to find out how many packets it can send at a time.

When a browser first makes a connection to your server — the server has no way of knowing the amount of **bandwidth** between them.

_Bandwidth is how much data can be transmitted over a network per unit of time. Usually it's measured in bits per second (`b/s`). Plumbing is a common analogy — think of bandwidth as how much water can come out of a pipe per second._

Your server doesn't know how much data the connection can handle — so it starts by sending you a small and safe amount of data — usually 10 TCP packets.

If those packets successfully reach your site's visitor, their computer sends back an acknowledgement (ACK) saying the packets have been received.

Your server then sends more data back, but this time it doubles the amount of packets.

This process is repeated until packets are lost and your server doesn't receive an ACK. (At which point the server continues to send packets but at a slower rate).

That's the gist of TCP slow start — in real life the algorithm varies, but that's essentially how it works.

## [So where does 14kB come from?](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#so-where-does-14kb-come-from)

Most web servers TCP slow start algorithm starts by sending 10 TCP packets.

The maximum size of a TCP packet is `1500 bytes`.

_This maximum is not set by the TCP specification, it comes from the [ethernet standard](https://en.wikipedia.org/wiki/Ethernet_frame)_

Each TCP packet uses **40 bytes** in its header — [16 bytes for IP](https://en.wikipedia.org/wiki/IPv4#Packet_structure) and an additional [24 bytes for TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol#TCP_segment_structure)

That leaves **1460 bytes** per TCP packet. `10 x 1460 = 14600 bytes` or roughly 14kB!

So if you can fit your website — or the critical parts of it — into 14kB, you can save visitors a lot of time — the time it takes for one round trip between them and your website's server.

## [How bad can one round trip be?](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#how-bad-can-one-round-trip-be)

...

## [Now that you know about the 14kB rule, what can you do?](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#now-that-you-know-about-the-14kb-rule-what-can-you-do)

Of course, you should make your website as small as possible — **you love your visitors and you want them to be happy**. Aiming for each page to fit in under 14kB is good target.

**That 14kB includes compression — so it could actually be more like ~50kB of uncompressed data** — which is generous. [_Consider that the Apollo 11 guidance computers only had 72kB of memory._](https://www.computerhistory.org/timeline/1969/)

Once you lose the autoplaying videos, the popups, the cookies, the cookie consent banners, the social network buttons, the tracking scripts, javascript and css frameworks, and all the other junk nobody likes — you're probably there.

But, assuming you've tried your very best to fit everything into 14kB, and can't — the 14kB rule is still useful.

If you **Make sure the first 14kB of data you send to your visitors can be used to render something useful** — for instance some critical CSS, JS and the first few paragraphs of text explaining how to use your app.

_Note — The 14kB rule includes **HTTP headers** — which are uncompressed (even with HTTP/2 on the first response) — it also includes **Images**, so load only what's above the fold and keep them very small, or use placeholders so your visitors know they're waiting for something good._

### [Some caveats to the rule](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#some-caveats-to-the-rule)

The 14kB rule is more like a rule of thumb, than a fundamental law of computing:

- Some servers have increased the TCP slow start initial window to 30 packets instead of 10
- Sometimes the server knows it can start with a larger number of packets because it's used the TLS handshake to establish a larger window can be used.
- Servers can cache how many packets a route can manage, and send more next time it connects.
- There's other caveats too — [here's a more in depth article about why the 14kB rule isn't always the case](https://www.tunetheweb.com/blog/critical-resources-and-the-first-14kb/)

#### HTTP/2 and the 14kB rule

There is an idea that the 14kB rule no longer holds true when using HTTP/2. I've read all I can about this without boring myself to death — but I haven't seen any evidence that servers using HTTP/2 have stopped using TCP slow start beginning with 10 packets.

#### HTTP/3 and QUIC

Similarly to HTTP/2, there is a notion that HTTP/3 and QUIC will do away with the 14kB rule — this is not true. [QUIC recommends the same 14kB rule.](https://datatracker.ietf.org/doc/id/draft-ietf-quic-recovery-26.html)

## [Further reading](https://endtimes.dev/why-your-website-should-be-under-14kb-in-size/#further-reading)

Much of the content of this post comes from the following resources:

- [High performance browser networking _by Ilya Grigorik_](https://hpbn.co/)
- [Increase HTTP Performance by Fitting In the Initial TCP Slow Start Window _by Simon Hørup Eskildsen_](https://sirupsen.com/napkin/problem-15)
- [Critical Resources and the First 14 KB - A Review](https://www.tunetheweb.com/blog/critical-resources-and-the-first-14kb/)
- [HTTP3 performance improvements](https://www.smashingmagazine.com/2021/08/http3-performance-improvements-part2/)
