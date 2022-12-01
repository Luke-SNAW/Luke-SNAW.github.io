---
id: wmzx1yfzzgam5vwrbmbwsak
title: "As a Front-End Engineer: 8 Useful Npm Coding Techniques That You Should Use"
desc: ""
updated: 1669794069958
created: 1669793940060
published: false
---

> https://javascript.plainenglish.io/as-a-front-end-engineer-8-useful-npm-coding-techniques-that-you-should-use-bc30b8503ba4

## Open a package’s documentation page

My friends, it would have saved me a lot of time if I had known this trick earlier.

In the past, when I wanted to query the usage documentation of `lodash`, I always searched for its address through `google`.

In fact, npm can help you achieve this goal quickly. You only need to run `npm docs xxx` to quickly open `xxx`'s documents

```shell
npm docs [package-name] // npm docs lodash
```

## Open a package’s GitHub repo

As a programmer, I guess you also like `github`, which is a treasure base for programmers.

Sometimes I want to know the source code of a package, can I only search for the package name on `github`?

The answer is no, `npm` can help you quickly open a package's GitHub repo

```shell
npm repo [package-name] // npm repo lodash
```

## Check packages for outdated dependencies

Run the `npm outdated` command in your project and it will check all packages for the current version, the required version and the latest version.

```shell
npm outdated
```

## View all historical versions of a package

Do you know how to view all historical versions of a package?

Yes, we can do this through npm’s online site.

That’s like this link below…

[https://www.npmjs.com/package/lodash?activeTab=versions](https://www.npmjs.com/package/lodash?activeTab=versions)

Is there another way? It’s amazing, all you need is this one-line command.

```shell
npm v [package-name] versions // npm v lodash versions
```

## Find risky packages in your project

[from npm](https://docs.npmjs.com/cli/v9/commands/npm-audit) The audit command submits a description of the dependencies configured in your project to your default registry and asks for a report of known vulnerabilities. If any vulnerabilities are found, then the impact and appropriate remediation will be calculated. If the fix argument is provided, then remediations will be applied to the package tree.

```shell
npm audit
```

## View details of a package

Well! Maybe this command is not very useful, but you can use it to learn a lot about a package, such as its author, contact information, etc.

```shell
npm v [package-name] // npm v lodash
```

## npm xmas

I never thought npm would be so interesting, haha!

When you run `npm xmas`, you will see a Christmas tree.

```shell
npm xmas
```

## npm visnup

My friends, if you know the reason, please tell me. Why does a person appear.

```shell
npm visnup
```
