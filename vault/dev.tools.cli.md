---
id: z8iu36gfcu6tok0rnwtawg0
title: CLI
desc: ""
updated: 1715127496797
created: 1653704390962
---

## Collections

- [The Art of Command Line](https://github.com/jlevy/the-art-of-command-line)
- 🤖 [just](https://github.com/casey/just) is a handy way to save and run project-specific commands.
- [Structured text tools](https://github.com/dbohdan/structured-text-tools) - The following is a list of text-based file formats and command line tools for manipulating each.
- [ls-lint](https://github.com/loeffel-io/ls-lint) - An extremely fast directory and filename linter - Bring some structure to your project filesystem
- [mise-en-place](https://github.com/jdx/mise) - dev tools, env vars, task runner
- [Flox](https://github.com/flox/flox/) is a virtual environment and package manager all in one.
- [chezmoi](https://github.com/twpayne/chezmoi) - Manage your dotfiles across multiple diverse machines, securely.

## Shell

- [Oh My Zsh](https://github.com/ohmyzsh/ohmyzsh) - A delightful community-driven (with 2,000+ contributors) framework for managing your zsh configuration.
- [Powerlevel10k](https://github.com/romkatv/powerlevel10k) - A Zsh theme
- [try](https://github.com/binpash/try) lets you run a command and inspect its effects before changing your live system. `try` uses Linux's [namespaces (via `unshare`)](https://docs.kernel.org/userspace-api/unshare.html) and the [overlayfs](https://docs.kernel.org/filesystems/overlayfs.html) union filesystem.
- [atuin](https://github.com/atuinsh/atuin) - ✨ Magical shell history

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
