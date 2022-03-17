---
id: ncyn8xow2x0rfon0mjy0bnc
title: Vs Code
desc: ""
updated: 1647146253402
created: 1646011769978
---

- [Dendron](https://github.com/dendronhq/dendron) - The personal knowledge management (PKM) tool that grows as you do!
- [P42 JavaScript Assistant: Refactoring Hints & Automation](https://marketplace.visualstudio.com/items?itemName=p42ai.refactor#p42refactor)
- Markdown All in One
  - section numbering : Ctrl+Alt+P -> section
  - TOC : Ctrl+Alt+P -> toc
- Git Graph
- Emoji
- Regions With Colors
- Prettier-Standard
- Add jsdoc comments
- [GistPad](https://github.com/lostintangent/gistpad) - VS Code extension for managing and sharing code snippets, notes and interactive samples using GitHub Gists
- [Database Client](https://marketplace.visualstudio.com/items?itemName=cweijan.vscode-database-client2)
- [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) - Open any folder on a remote machine using SSH and take advantage of VS Code's full feature set.

# Testing

- [Live Frame](https://marketplace.visualstudio.com/items?itemName=jevakallio.vscode-live-frame) - Live preview your web application inside VS Code
- [Blockman](https://marketplace.visualstudio.com/items?itemName=leodevbro.blockman) - Mark/Highlight code blocks
- [XState VSCode](https://marketplace.visualstudio.com/items?itemName=statelyai.stately-vscode) - Visual editing, autocomplete and typegen for XState
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)

# Etc

## Default VS Code As The Git Editor

```
git config --global core.editor "code -w"
```

# Co-op

## 필수

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
- axe Accessibility Linter
- Code Spell Checker

## 선택

- Auto Close Tag
- Auto Rename Tag
- Better Comments
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
