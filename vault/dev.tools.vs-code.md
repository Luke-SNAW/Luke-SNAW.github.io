---
id: ncyn8xow2x0rfon0mjy0bnc
title: Vs Code
desc: ""
updated: 1715648821849
created: 1646011769978
---

## Collections

- [VS Code Shortcuts To Code Like You’re Playing a Piano](https://betterprogramming.pub/vs-code-shortcuts-to-code-like-youre-playing-a-piano-e5db7b272d1)
- [Change the default terminal in Visual Studio Code](https://stackoverflow.com/a/45899693/5163033) - Terminal: Select Default Profile

## Dev

- [P42 JavaScript Assistant: Refactoring Hints & Automation](https://marketplace.visualstudio.com/items?itemName=p42ai.refactor#p42refactor)
- Markdown All in One
  - section numbering : Ctrl+Alt+P -> section
  - TOC : Ctrl+Alt+P -> toc
- Git Graph
- Emoji
- Regions With Colors
- Prettier-Standard
- Add jsdoc comments
- [Preview.js](https://github.com/fwouts/previewjs) - Get instant previews of your UI components, directly in your IDE
- [GistPad](https://github.com/lostintangent/gistpad) - VS Code extension for managing and sharing code snippets, notes and interactive samples using GitHub Gists
- [Database Client](https://marketplace.visualstudio.com/items?itemName=cweijan.vscode-database-client2)
- [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) - Open any folder on a remote machine using SSH and take advantage of VS Code's full feature set.
- [JSON Hero](https://marketplace.visualstudio.com/items?itemName=JSONHero.jsonhero-vscode) - a beautiful JSON viewer.
- [Increment Selection](https://marketplace.visualstudio.com/items?itemName=albymor.increment-selection)
- [Headwind](https://marketplace.visualstudio.com/items?itemName=heybourn.headwind) to order Tailwind classes automatically
-

## Testing

- [Live Frame](https://marketplace.visualstudio.com/items?itemName=jevakallio.vscode-live-frame) - Live preview your web application inside VS Code
- [Blockman](https://marketplace.visualstudio.com/items?itemName=leodevbro.blockman) - Mark/Highlight code blocks
- [XState VSCode](https://marketplace.visualstudio.com/items?itemName=statelyai.stately-vscode) - Visual editing, autocomplete and typegen for XState
- [7 Unnecessary VSCode Extensions You Should Uninstall Now](https://codingbeautydev.com/blog/unnecessary-vscode-extensions/)
- [Better Align](https://marketplace.visualstudio.com/items?itemName=Chouzz.vscode-better-align)

## Etc

- [Front Matter](https://github.com/estruyf/vscode-front-matter) a CMS running straight in Visual Studio Code

### Default VS Code As The Git Editor

```
git config --global core.editor "code -w"
```

## Co-op

### 필수

- ESLint, Prettier, Vetur
  - Settings> save 검색
    - Editor: Format On Save 활성화
    - Edit in settings.json 클릭하여 편집하여 다음 내용을 추가
      ```json
      "eslint.format.enable" : true,
      "[vue]" : {
        "editor.defaultFormatter" : "esbenp.prettier-vscode"
      },
      "[javascript]" : {
        "editor.defaultFormatter" : "esbenp.prettier-vscode"
      },
      "eslint.validate" : [
        "javascript"
      ],
      "editor.defaultFormatter" : "esbenp.prettier-vscode",
      ```
- [axe Accessibility Linter](https://marketplace.visualstudio.com/items?itemName=deque-systems.vscode-axe-linter)
- Code Spell Checker

### 선택

- Auto Close Tag
- Auto Rename Tag
- [Better Comments](https://marketplace.visualstudio.com/items?itemName=aaron-bond.better-comments)
- Emmet JSS
- ES7 React/Redux/GraphQL/React-Native snippets
- Git Graph
- GitLens
- HTML CSS Support
- HTML End Tag Labels
- Indent-Rainbow
- JavaScript (ES6) snippets
- JavaScript Booster
- P42 JavaScript Assistant
- Regions with Colors
- Surround
- Todo Tree
- Turbo Console Log
- Vue Snippets StandardJS
- Vue VSCode Snippets
- [Blockman - Highlight Nested Code Blocks](https://marketplace.visualstudio.com/items?itemName=leodevbro.blockman)

## Personal knowledge management

- [Foam](https://github.com/foambubble/foam) is a personal knowledge management and sharing system inspired by [Roam Research](https://roamresearch.com/), built on [Visual Studio Code](https://code.visualstudio.com/) and [GitHub](https://github.com/).

### [Dendron](https://github.com/dendronhq/dendron)

The personal knowledge management (PKM) tool that grows as you do!

- [awesome-dendron: A Dendron awesome list of extensions, vaults, and more](https://github.com/dendronhq/dendron/discussions/2118)

## Apply Font

```shell
system_profiler -json SPFontsDataType | grep \"family | sort | uniq # https://stackoverflow.com/a/67132993/5163033
```

Or

In Desktop view, Press “⌘ + Space” to start Spotlight, then type in “font book”
