---
id: flxrnqq70hujy04l6g64vwh
title: 6 Best Practices to Manage Pull Request Creation and Feedback
desc: ""
updated: 1664437703920
created: 1664437491654
---

> https://doordash.engineering/2022/08/23/6-best-practices-to-manage-pull-request-creation-and-feedback/

## Why bad PRs slow down the development cycle

## PR basics

## Write descriptive and consistent names

## Create a clear PR title and description

While many people think only about the code when they create a PR, context is essential for understanding and reviewing that PR.

Reviewers must know what the fundamental problem is before they can understand if it’s been resolved. Don’t force a reviewer to read through 600 lines of code. Instead, provide a descriptive PR title and high-level summary at the top of the PR.

This is why it's good practice to create and enforce the use of PR templates, such as:

- Problem
- Solution
- Impact
- Testing plan

## Keep PRs short (same with files and functions)

## Manage PR disagreements through direct communication

Why does direct communication help?

- Feedback will be faster.
- Verbal communication leads to fewer misunderstandings.
- 10 minutes of verbal communication is a much more thorough review than a few back and forth GitHub comments.
- Direct conversation prevents constant context switching between other work and checking the PR comment section.

## Avoid rewrites by getting feedback early

## Request additional reviewers to create dialogue

Sometimes we want our code merged in quickly, so we seek an approval instead of a proper review and dialogue. However, shallow reviews defeat the purpose of code review.

One step that can help open up a dialogue is to request more reviewers.

Why does requesting more reviewers help?

- It adds more perspectives. If only one approval is required, and only one review requested, other teammates will never get a chance to disagree.
- People are available at different times. Requesting more reviewers increases the likelihood that eyes get on the PR sooner.
- If there’s a more general coding style/design disagreement in the PR, others have a chance to weigh in or at least become aware of it.
- Standups are by nature more status updates than working in the weeds. When someone is requested on a PR, they can read exactly what a teammate is working on and can reference that code if they encounter a similar issue.
