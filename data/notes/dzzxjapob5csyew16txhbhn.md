
> https://www.rdegges.com/2015/why-i-love-basic-auth/

It’s a _bad thing_ because OAuth (_as popular as it is_) is a huge pain in the ass – for both the people building the API services as well as the developers consuming them.

OAuth is complex, misunderstood, widely misused, and lacking universal implementations. It most definitely has its uses, but in many cases feels burdensome.

Basic Auth, on the other hand, is simple, very well understood, and has been well supported in every language and framework since the 1990’s.

## How Basic Auth Works

Let’s talk about Basic Auth:

- It’s a well and clearly defined [specification](http://tools.ietf.org/html/rfc2617 "HTTP Basic Auth / Digest Auth Spec").
- It’s been around since ~1996.
- It’s super simple.

Here’s the short version of how it works.

- You are a developer.
- You have an API key pair: an _API Key ID_ and an _API Key Secret_. Each of these is a randomly generated string (_usually a [uuid](http://en.wikipedia.org/wiki/Universally_unique_identifier "UUID on Wikipedia")_).
- To authenticate against an API service, all you need to do is put your credentials into the [HTTP Authorization header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html "HTTP Headers Spec").

## It’s Simple

My favorite thing about Basic Auth is that it’s _simple_.

Unlike OAuth, there’s no intermediary steps you need to go through to get an access token: all you need are your API keys.

This makes a _huge_ difference in development speed.

Instead of spending a lot of time figuring out what permissions and scopes you need granted, setting up redirect URIs, web servers, and all this crap that only serves to complicate matters – all you need to do is put your damn API keys into the HTTP Authorization header and _BAM_, shit works.

Because it’s so simple, you can get a lot of work and testing done faster.

You also don’t need to worry about things like:

- Token expiration. _Cough, cough OAUTH!_
- Providers changing their implementations. _Just about every single OAuth provider has changed their implementations numerous times, breaking thousands of developer applications._
- Complex workflows for getting access to your data. _OAuth2 has 4 different grant types, each of which is used in a different way and for different purposes._

Every time I use a service like [Twilio](https://www.twilio.com/ "Twilio"), I’m reminded how convenient Basic Auth is to use: it’s truly a pleasure to be able to:

- Generate and destroy API keys on command.
- Easily throw API keys into whatever apps I’m currently hacking on.
- Easily test my API requests out via the command line or an API explorer like [Runscope](https://www.runscope.com/ "Runscope").

I just love it.

## It’s Secure

Basic Auth gets a bad reputation for being _“insecure”_, but this isn’t necessarily true.

There are several things you can do to ensure that your API service (_secured by Basic Auth_) is as secure as possible:

- Always run all requests over HTTPs. If you’re not using SSL, than no matter what authentication protocol you use, you’ll never be secure. Unless you’re using HTTPs, all of your credentials will be sent in plain-text over the wire: _a horrible idea_.
- Give your developers the ability to generate as many API key pairs as they’d like. This makes it easy for developers to _isolate_ their usage of an API key pair to a single application or service.
- Give your developers the ability to revoke API key access when they need to. For instance: if a developer accidentally leaks his API keys on Github, he should be able to revoke that API key pair, thereby guaranteeing it can’t be used by anyone else.
- Generate random API key pairs using [uuids](http://en.wikipedia.org/wiki/Universally_unique_identifier "UUID on Wikipedia"). This ensures API key pairs aren’t _guessable_.

Furthermore, for developers _using Basic Auth_, there are a few things you should always keep in mind:

- Store your API keys securely. If you’re using an API service that supports Basic Auth, be sure to not do things like store your API keys in your public Github repo.
- Don’t use an API service that isn’t run over HTTPs – you’re guaranteed to have problems in the future.
- Use a unique API key pair for each application you write. This way, if you accidentally lose an API key or leak it publicly, you only need to revoke _that specific API key_, and you only need to update _a single codebase that relied on that API key_. This will make your life much easier in the long run.

If you’re looking for a good example of an API company that handles API keys the right way, check out [AWS](http://aws.amazon.com/ "Amazon Web Services").

## Universally Supported

Another great thing about Basic Auth is that there’s only one implementation everyone uses – this means that there’s never any ambiguity about how to craft requests or server-side components: it’s always the same.

The way it works is like this:

- You take the API Key ID and the API Key Secret, and you put them into a colon-separated string like so: `'xxx:yyy'`.
- You then prepend the word `'Basic '` to the string, so that you have: `'Basic xxx:yyy'`.
- You then [base64](http://en.wikipedia.org/wiki/Base64 "Base64 on Wikipedia") encode the API key portion of the string, so you end up with: `'Basic eHh4Onl5eQ=='`.
- Lastly, you set this value as your HTTP Authorization header when you make your HTTP requests.

When the web server receives your request, it then:

- base64 decodes the header value.
- Splits the string by the colon character.
- The left-hand portion is the API Key ID, the right hand portion is the API Key Secret.
- The server then validates these credentials, and either allows you access or returns an _HTTP 401 UNAUTHORIZED_ response.

There’s nothing ambiguous about Basic Auth. This means every programming language has top-notch support for the standard, and it’s easy to find well audited libraries for using Basic Auth as both a producer and consumer.
