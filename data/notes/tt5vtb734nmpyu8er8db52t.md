
> https://www.propelauth.com/post/i-love-building-a-startup-in-rust-i-wouldnt-pick-it-again

For almost two years now, the vast majority of our backend code was written in Rust (aside from a little bit of Python). I love Rust, it’s by far my favorite language. I find myself missing `match` in pretty much every other language I go to.

However, if I was doing it over, I wouldn’t choose Rust.

This advice is primarily for early startups (pre-product/pre-seed/seed). But first, it’s important to ask why we went with Rust in the first place.

## Why did we choose Rust initially?

**Safety++.** I’m a big believer that even the best developers get slowed down by silly mistakes. Types are obviously important to combat that, but Rust feels like it goes above and behind here. Runtime issues are easy to avoid. You’d have to go out of your way to cause a memory leak. Crates like sqlx exist which can do compile time checking of your SQL queries against the DB. Rust, and the ecosystem around it, has a lot of tools to stop you from shooting yourself in the foot.

**Readability / Expressiveness**. There are so many things about Rust’s syntax that make me happy. For one specific example, the `?` operator is just a great approach to error handling. It keeps the code focused on the happy path.

We frequently write code like:

```rust
// fetch_user returns a Result<Option<User>, sqlx::Error>
// In other words "It can return a user, nothing, or a DB error"

// The first question mark propagates unexpected DB errors
// The second one propagates a not found error
let user = fetch_user(&user_id, &pool).await?
    .ok_or(NotFound)?;
```

which is just really succinct for what it does, while still being flexible. If you also include algebraic types, match, type conversions (From, Into, TryFrom, etc), and more - Rust lets us write very succinct, readable code.

## Why would we not choose Rust again?

If we were starting the company over from scratch, there are a few more things to consider.

**Slower iterations.** When you first start with Rust, you’ll end up fighting the compiler a bit. This is natural and gets easier over time. However, at a new startup, one of the core problems is to figure out if you are building something useful.

[example](https://users.rust-lang.org/t/error-with-lifetimes-on-impl-fn/58706)

A quick MVP can be invaluable in determining if you are on the right path or lost in the woods. All that time spent making readable, performant code might be wasted.

Additionally, every new employee that isn’t familiar with Rust will run into this. You’ll either need to prioritize Rust experience when hiring or get good at training people.

**Perf is easy when you have AWS credits.** One reason that you might pick Rust is for overall performance.

As a startup, when you start to scale, you are met with an interesting alternative: take the free money that every infra company offers and scale vertically/horizontally. AWS has [Activate](https://aws.amazon.com/activate/). GCP has a [startup program](https://cloud.google.com/startup). If you search for startup deals, you’ll find so many more. There’s a whole network of products that offer these deals as a side-benefit too.

[AWS credits offered](https://cdn.getmidnight.com/a1241f0fcb8d83a4c0387f234e241914/2023/02/Screen-Shot-2023-02-16-at-3.43.47-PM.png)

You can postpone dealing with scale by making a bigger k8s cluster or a larger ASG and spend that time on more important things.

## When would we use Rust?

What it really boils down to is that Rust is a great language for building performant production systems. If you are prototyping, iterating with customers, or just unsure in the product direction - you are probably going to waste valuable time with Rust.

Once you have that clarity, and you’ve shifted to “It’s time to scale” mode or “Perf actually is really important here” mode or even “We have a solid direction/roadmap and we don’t want too much tech debt” mode, Rust is a fantastic choice.

## Are you rewriting everything?

It would be really funny if we combat the trend of people rewriting their products in Rust by going in the opposite direction… but no, we’re not.

Rust has provided us with an incredibly solid foundation and we’ve invested a lot in the developer experience internally.

We have [extractors](https://docs.rs/actix-web/latest/actix_web/trait.FromRequest.html) for different user requirements to make adding APIs very straightforward. We have middleware for scoping requests per customer. In most languages, this is pretty standard, but in Rust, for our use case, they both require at least a rough understanding of [pinning](https://rust-lang.github.io/async-book/04_pinning/01_chapter.html).

Now that we’re here, and we have all these utilities to build on top of and domain knowledge built up, we’re able to move both quickly and safely. But if I look back at it, as much as I love Rust, I absolutely would not choose Rust again.

---

## [zeroxfe](https://news.ycombinator.com/item?id=34836164)

If you're thinking about building something in Rust, a good question to ask is, "what would I use if Rust didn't exist?"
If your answer is something like Go or Node.js, then Rust is probably not the right choice.

If your answer is C or C++ or something similar, then Rust is very likely the right choice.

Obv, there are always exceptions here, but this helps you work through things a bit more objectively. Rust can be a fantastic language for many purposes, but it has a very high development cost.
