---
id: QLwJ96mvQQgw8U1verS7k
title: AWS tools
desc: ""
updated: 1667979802872
created: 1645523767783
---

## Collections

- [Cloudcraft](https://www.cloudcraft.co): Visualize your cloud architecture like a pro Create smart AWS diagrams

## [jeffybefffy519](https://news.ycombinator.com/item?id=33525003)

> Does your team do local dev?  
> Every team I've known that adopted Lambda + DynamoDB (or equivalents) gave up on running their app locally, adding a lot of friction to the development process.

I highly recommend using AWS's own Chalice library as it makes local dev _and_ deployment very easy.

If you need more complex cases like deploying docker containers to a Lambda function, take a look at AWS's SAM library. Also supports local dev _and_ makes deployment easy (its essentially a wrapper around Cloudformation so its very powerful).
