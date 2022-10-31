---
id: z8iu36gfcu6tok0rnwtawg0
title: CLI
desc: ""
updated: 1666824991400
created: 1653704390962
---

## Collections

- [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)

## Shell

- [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) - A delightful community-driven (with 2,000+ contributors) framework for managing your zsh configuration.
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k) - A Zsh theme

## Script

- [zx](https://github.com/google/zx) - A tool for writing better scripts using javascript

## Features

- [Fig](https://github.com/withfig/autocomplete) adds autocomplete to your terminal
- [Watchexec](https://github.com/watchexec/watchexec) - Executes commands in response to file modifications

### [Reflex](https://github.com/cespare/reflex)

Run a command when files change

> I have been using reflex https://github.com/cespare/reflex for the same thing in some of our docker projects

> +1 for reflex, love being able to have a config for development  
> Example .reflex.conf to run one command when an openapi spec changes and another when any go files change:

```shell
-g "spec.yaml" -- bash -c 'make'
-sr "\.go$" -- go run cmd/app/main.go
```

Then run it with:

```shell
reflex -d fancy -c .reflex.conf
```

#### Why you should use reflex instead

- Reflex has no dependencies. No need to install Ruby or anything like that.
- Reflex uses an appropriate file watching mechanism to watch for changes efficiently on your platform.
- Reflex gives your command the name of the file that changed.
- No DSL to learn -- just give it a shell command.
- No plugins.
- Not tied to any language, framework, workflow, or editor.

## Viewer

- [fx](https://github.com/antonmedv/fx) - Terminal JSON viewer
- Write reducers in your favorite language: [JavaScript](https://github.com/antonmedv/fx/blob/master/doc/js.md) (default), [Python](https://github.com/antonmedv/fx/blob/master/doc/python.md), or [Ruby](https://github.com/antonmedv/fx/blob/master/doc/ruby.md).

```

```
