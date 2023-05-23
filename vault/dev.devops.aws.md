---
id: 7mujc4bw6yz1nfbf03gmqc8
title: Aws
desc: ""
updated: 1684737861642
created: 1646005847772
---

## IAM

### IAM에 필요한 기본 권한

- iam:ChangePassword - 최초 로그인 후 암호변환 (필수 아닐 수 있음. 권한 없을 때 실패 로그로 권한 요청 → 권한 받고 실패 → 특수문자 넣어 성공했기 때문)
- **[IAM: IAM 사용자가 MFA 디바이스를 스스로 관리하도록 허용](https://docs.aws.amazon.com/ko_kr/IAM/latest/UserGuide/reference_policies_examples_iam_mfa-selfmanage.html)**
- iam:GetLoginProfile, iam:UpdateLoginProfile - 계정 사용자가 콘솔 비밀번호 리셋을 스스로 할 수 있도록

## Misc

### [Does anyone else finds AWS and other Amazon services overly complicated?](https://news.ycombinator.com/item?id=33490314)

- [JAMstack walk-through](https://news.ycombinator.com/item?id=33491010)
- [AWS is basically a "construct your own custom infrastructure" service and does that well.](https://news.ycombinator.com/item?id=33491658)
- [We have both tried and are unable to figure out how to tie payment info to our AWS organization.](https://news.ycombinator.com/item?id=33494968)

### GCP has a better serverless offering.

from [adameasterling](https://news.ycombinator.com/item?id=33523507)

I have limited time before my next meeting so I'll type real quick:
GCP Cloud Run is like the best of both worlds between AWS ECS Fargate and AWS Lambda. (Yes, the comment is in the context of containers. Sort of.)

- Like Fargate, Cloud Run hosts containers and takes care of figuring out where they actually live. Unlike Fargate, you don't have to say exactly how many containers you want running at once; GCP will automatically scale the # of containers up and down based on HTTP load and will scale down to 0. This should make Cloud Run cheaper than Fargate. (If you want to hook up Fargate to a webserver and you don't have autoscale figured out, you'll have to keep a lot of workers alive doing nothing.)

- Like Lambda, Cloud Run bills by the amount of time spent processing at least one request. But unlike Lambda, Cloud Run lets one container handle more than one request at a time (it sucks to have to spin up a lot of Lambda invocations that do a bunch of IO). Web servers that are good at concurrency shine here. This should save money.

- Cloud Run has more generous limits in many respects than Lambda. Cloud Run lets you set up SIGTERM hooks, so you can do some cleanup logic in your container (to e.g. write performance data to a timeseries table or whatever).

That's Cloud Run. On the database side: GCP Firestore is very interesting and we're going to build a big feature around it. AWS has nothing like it. On the queue side of things: We're planning to build around GCP Cloud Tasks; We've more or less built Cloud Tasks ourselves using a mix of MySQL and AWS SQS (and it was hard and we haven't done a good job).

I'd love to start a Discord or something to discuss these thoughts more. It's so hard to get good practical information for system architects/CTO types who just need to hammer stuff out.

> A couple of points: 1. Cloud Run is more analogous to AWS App Runner than Fargate. 2. Cloud Run isn't a great analog to lambda. Lambda is built to host functions. Cloud Run is built to host applications. Lambda is more analogous to GCP Functions. 3. Cloud Tasks should probably be built with EventBridge + Lambda or EventBridge + StepFunctions or EventBridge + ECS.  
> I don't profess to be a GCP expert so it's hard for me to make a judgement call on what's better. I can, however, say that most of this post ignores some of the real serverless power provided by AWS. AWS AppSync, AWS API Gateway, DynamoDB, CloudFront Functions, Lambda@Edge. It also makes comparisons that are not very fair.

Huh. I had this long call with our AWS Account Reps (+ Support Engineers) the other day and no one mentioned App Runner! This is the first I've heard of it. Looking at it now.
Ah I see, launched originally in May 2021. That's probably why they weren't aware of it. Yes, this looks cool. Very much what I was looking for.

The differences that I can see are...

- AWS App Runner lacks an advertised free tier. Not a big deal for all but the smallest projects though.

- AWS App Runner bills rounded up to the next second, whereas GCP Cloud Run rounds up to the next 100 millisecond.

- AWS App Runner doesn't charge per request (?!), whereas GCP Cloud Run charges $0.40/1M requests.

- AWS App Runner has fewer CPU/RAM configuration options. The lack of low end options may be a blocker for us.

- It's cheaper than GCP Cloud Run - $51.83 @ vCPU/1GiB, but 2GiB minimum, in Runner vs $69.642 @ 1 vCPU/1GiB (v1) $97.50 @ 1 vCPU/1GiB (v2) in Cloud Run.

- I'm confused by the networking model. In App Runner, you have to make an ENI for your App Runner service to access your VPC? Weird. There's some extra cost there I think.

Things that I can't determine based on the documentation...

- Does App Runner support committed use discounts?

- Does App Runner throw a SIGTERM before shutting the container down? I hope yes but I can't find docs on it.

- Is there a file system accessible on App Runner and is it just in memory or is there actually a disk to write to?

- The quotas & limits page on App Runner feels incomplete and I'm left with a lot of questions about it.

- Is there an SLA?

- In fact the documentation for App Runner just feels a little incomplete.

It looks like AWS definitely wants App Runner to be the answer to Cloud Run, but to me, it feels like it's not quite there yet.

It's also weird, that ECS Fargate lets you run a container without thinking about the server that it runs on, and App Runner does too, just with a few extra things. Why is it a whole separate service? Why didn't they just add it onto Fargate?

Re: Other services. I've only heard of API Gateway, DynamoDB and Lambda@Edge; I'll have to spend time investigating the other ones. Thank you for mentioning them!

## Collections

- [The Guardian Optimizes Mobile Push-Notification Delivery Architecture](https://www.infoq.com/news/2023/05/guardian-push-architecture/)
  - [Guardian Mobile Notifications](https://github.com/guardian/mobile-n10n)
