---
id: TN3SWriksRFA35jnzNKzy
title: Tools
desc: ""
updated: 1666137821834
created: 1645523891283
---

## Collections

- [Dragonfly](https://github.com/dragonflydb/dragonfly) is a modern in-memory datastore, fully compatible with Redis and Memcached APIs. Dragonfly implements novel algorithms and data structures on top of a multi-threaded, shared-nothing architecture. As a result, Dragonfly reaches x25 performance compared to Redis and supports millions of QPS on a single instance.
  - https://news.ycombinator.com/item?id=31560547
- [mkcert](https://github.com/FiloSottile/mkcert) is a simple tool for making locally-trusted development certificates. It requires no configuration.

## API

- [Insomnia](https://insomnia.rest/) - Build APIs that work.
- [Learn Apollo](https://github.com/learnapollo/learnapollo) - Learn Apollo - A hands-on tutorial for Apollo GraphQL Client (created by Graphcool)
- [Mock Service Worker (MSW)](https://github.com/mswjs/msw) - Seamless REST/GraphQL API mocking library for browser and Node.js.
- [MeCallApi](https://www.mecallapi.com/)
- [API Platform](https://github.com/api-platform/api-platform) - Create REST and GraphQL APIs, scaffold Jamstack webapps, stream changes in real-time.
- [directus](https://github.com/directus/directus) - Open-Source Data Platform 🐰 — Directus wraps any SQL database with a real-time GraphQL+REST API and an intuitive app for non-technical users.
- [API Hub - Free Public & Open Rest APIs](https://rapidapi.com/hub) - Discover and connect to thousands of APIs
- [PostgREST](https://github.com/PostgREST/postgrest) serves a fully RESTful API from any existing PostgreSQL database. It provides a cleaner, more standards-compliant, faster API than you are likely to write from scratch.
- [mitmproxy2swagger](https://github.com/alufers/mitmproxy2swagger) - A tool for automatically converting [mitmproxy](https://mitmproxy.org/) captures to [OpenAPI 3.0](https://swagger.io/specification/) specifications. This means that you can automatically reverse-engineer REST APIs by just running the apps and capturing the traffic.

## Low code

- https://www.appsmith.com/
- https://tooljet.com/

## Framework

- [PocketBase](https://pocketbase.io/) is an open source Go backend, consisting of:
  - embedded database (_SQLite_) with **realtime subscriptions**
  - built-in **files and users management**
  - convenient **Admin dashboard UI**
  - and simple **REST-ish API**

## Service

- [Ask HN: So you moved off Heroku, where did you go?](https://news.ycombinator.com/item?id=33077118)
- [appwrite](https://github.com/appwrite/appwrite) - Secure Backend Server for Web, Mobile & Flutter Developers 🚀 AKA the 100% open-source Firebase alternative.

### [Why we’re moving away from Firebase](https://koptional.com/article/why-we%E2%80%99re-moving-away-from-firebase)

We’ve developed a few small projects on Supabase recently as a part of our prospecting process. The developer experience has been delightful, particular [Row Level Security](https://supabase.com/docs/guides/auth/row-level-security), the more powerful analog to Firestore Rules. That Supabase is betting on [Deno](https://deno.com/deploy) for their [serverless function suite](https://deno.com/blog/supabase-functions-on-deno-deploy) indicates to us that they are serious about great technology.

We love [PostgreSQL](https://www.postgresql.org/) which Supabase utilizes. We plan to do more research on scalability, since SQL databases can’t grow as big as their NoSQL counterparts. Nonetheless, Supabase came at the right time.

#### [Hacker news](https://news.ycombinator.com/item?id=33215770)

It's from Google, they deprecate things every 6 months including APIs your app is using, if you don't follow your app will be down pretty quickly. AWS nearly never do breaking changes.

##### [jamest](https://news.ycombinator.com/user?id=jamest)

[Firebase founder]

I no longer work at Firebase / Google, but two points:

1. There may be issues with the GCP integrations & UX/DX, but GCP integration is good for many customers and necessary for the future of the business.

   One of the common failure modes for the 2011-2014 crop of Backend-as-a-Service offerings was their inability to technically support large customers. The economics of developer tooling are a super-power-law. So, if you hope to pay your employees you'll need to grow with your biggest customers.

   Eventually, as they become TheNextBigThing, your biggest customers end up wanting the bells and whistles that only a Big Cloud Platform provide.

   This was a part of the reason we chose to join Google, and why the Firebase team really really really pushed hard to integrate with GCP at a project, billing, and product level (philosophy: Firebase exposed the product from the client, GCP from the server) despite all the organizational/political overhead.

2. I'm excited to see the current crop of app platforms emerge. It has been 10 years since [we launched](https://news.ycombinator.com/item?id=3832877) and there are now some great innovations in the space. I like the way [Supabase](https://supabase.com/) has exposed Postgres and [InstantDB](https://www.instantdb.com/) graphdb+realtime is really promising.
