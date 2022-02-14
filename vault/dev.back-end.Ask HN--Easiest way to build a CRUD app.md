---
id: fNDIZetrfDtW7x634bnXD
title: "Ask HN: Easiest way to build a CRUD app?"
desc: ""
updated: 1644799145393
created: 1644797844635
---

https://news.ycombinator.com/item?id=30320837

# Rails

> Rails removes so many questions 'how should i set this up?' 'where should this code go' 'how do i setup a db connection'. It is fast to setup.

# Django

> I would consider Django and just using its Admin framework for building your UI, you can achieve so much very quickly with almost no code.
> I believe it’s a brilliant tool for building internal CRUD type db apps.
>
> Knowing how to use the admin framework well is basically a developer super power.
>
> You won’t need any external libraries, it has brilliant docs and important tools like database migrations are built in.

> My journey: Django -> Flask -> FastAPI

# Elixir/Phoenix/LiveView

> Lots of variables in your question.
> For simple stuff I am a big believer in building backends with tools like Strapi, it's hard to beat for MVP
>
> For more customized stuff I do believe Rails is still the safest choice in terms of ease of use, docs, learning resources, community, available libraries and integrations, etc. etc. Close 2nd/3rd probably something like Django or Express.js based stuff.
>
> For more complex stuff my weapon of choice is Elixir/Phoenix/LiveView - hard to beat for actual web projects that need to handle some traffic. I am actually close to believing that there's probably nothing better suited for web projects than Erlang BEAM.

> it's relatively easy to do simple stuff in Phoenix, too, especially if you're used to "having to learn a lot of the ceremony" around a more heavyweight framework like rails.
>
> What is missing is a good database management system (like Django ships with) but on the other hand, the discipline of Phoenix will in the long run avoid your self/staff learning how to "abuse" Django's control panel to do super dangerous stuff (I have seen this happen in several places I have worked)
>
> In the long run, using elixir the language will have far, far fewer head-bashing-in/tableflip moments than, Python and Ruby, in my experience, so if you value your sanity it may be a good choice

---

> I would go for Ruby on Rails, or a more modern Phoenix Framework (Elixir). With Phoenix you can also use Phoenix LiveView to avoid writing JavaScript. Very stable, scalable and low-hassle once you deploy.

# Laravel

> A similar setup, for those more comfortable with PHP, would be Laravel [^0] in conjunction with Livewire [^1].
>
> Laravel is basically the “Rails of PHP”, and has an absolutely incredible ecosystem to go with it.
>
> Livewire was directly inspired by Phoenix LiveView. I only just recently started using it in my own projects, but it’s invaluable. Backend has always been my speciality, but now I can make real-time UIs just like the cool JS kids can too :)

[^0] https://laravel.com/
[^1] https://laravel-livewire.com/

> LiveView is amazingly productive, and it allows you to make highly interactive webapps much faster than if you make a REST/front-end split, just using regular Elixir.

> I can second this. I am using Elixir/Phoenix/LiveView for a new web app I am launching soon, and I have not written a single line of javascript so far.

# Vaadin

> I'll probably be a minority here, but I'd say: java + Vaadin [^1] + raw jdbc (no ORM nonsense). On Vaadin site, you can use starter [^2] to create an app template. There is no need to write javascript; most Vaadin code looks like good old desktop programming. Due Java stability, that thing will run forever and will be performant.
> If you want to be "cloud native" (or whatever cool name now is) in the future, you can later recompile it with graalvm [3] and produce a single, static binary, like cool kids these days does with golang and rust.

> Vaadin is interesting, and choice of java is ok (though I prefer Kotlin).
>
> But raw jdbc in 2022 is absolutely bonkers. If you don't prefer ORMs that's ok, but a light abstraction like SQLDelight or Spring data jdbc (if you prefer working with SQL) or a query builder like jOOQ (if you like type-safety) can make your life simpler by an order of magnitude.

[^1] https://vaadin.com/
[^2] https://start.vaadin.com/app/

# MS Access

> I’m surprised nobody had said MS Access. You don’t need to learn any programming languages, it comes with everything you need, and every Access app has lasted way longer than anyone wanted it to. ;)

# Etc

If this isn't a business application, ignore this entire comment.
If it is a business application, you probably shouldn't build a CRUD app, at least not the way that's commonly understood. Stick with me for a minute.

First off, you must never delete business data (except per GDPR, retention policies, or other legal requirements). I'm sure someone will pipe in with a contrived use case where you would want to, but in general you must not. Soft-deletes, sure. Hard deletes with immutable history, also ok. Generally the popular frameworks will not help you here.

Second, realize that an update is logically equivalent to a delete followed by an insert (under the hood, Postgres implements `update` precisely thus). So per the above, you should think twice about updates. As with deletes, an immutable history can make updates safe. Alternatively, you can use append-only versioning with a current version pointer. Again, the frameworks are just not going to help you here.

So out of CRUD that leaves just CR that are fully safe, and those are the easiest parts.

I'm sure most folks will think this is ridiculous but that's because "building business software" is 1) not taught in school, 2) considered hopelessly boring, and therefore 3) not valued by developers. Nevertheless, it's generally, y'know, our job. Good business software must keep records. It must track when things happened, who did them, and so on. The typical approach to CRUD, as exemplified by all the frameworks suggested in other comments, does not keep such records, and therefore produces software that is unfit for its purpose.

One common objection will be that you don't need these things, or don't know that you need these things, at the beginning of a project. Yes you do! Imagine telling the IRS "oh I didn't keep very good records this year, after all my business is just getting started". Record-keeping needs to be treated as a hard, non-negotiable requirement for all business software.
