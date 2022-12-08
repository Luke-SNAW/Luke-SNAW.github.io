---
id: sifjdlyh7vc7t98zi4y8ydq
title: Tips for typing import statements in JavaScript
desc: ""
updated: 1670459913629
created: 1670459855775
---

> https://2ality.com/2017/08/typing-import-statements.html

This blog post gives tips for typing import statements more quickly, including a helpful text snippet for Visual Studio Code.

---

## Does JavaScript’s `import` statement have the wrong syntax?  [#](https://2ality.com/2017/08/typing-import-statements.html#wrong-import-statement-syntax)

People occasionally complain that JavaScript’s import statement has it backwards. The syntax is:

```js
import { one, two, three } from "./my-module.js"
```

They argue that it should be:

```js
from './my-module.js' import {one, two, three};
```

As an aside, that’s how Python does imports.

Why? It would make auto-expansion easier: We’d first type the module specifier `'./my-module.js'` and then the imported values `{one, two, three}`. During the latter step, the IDE has the necessary context for helping us out.

The reasons for the different order in JavaScript are:

- It’s the same order as variable declarations.
- It’s the same order as using `require()` in Node.js modules.

Given that we only write code once but read it many times, the focus should be on which version is easier to read. And there, I slightly prefer JavaScript’s current syntax.

## Auto-importing  [#](https://2ality.com/2017/08/typing-import-statements.html#auto-importing)

These days, I mostly write TypeScript and I mostly use Visual Studio Code (VSC).

There, auto-importing has gotten really good: If there is a value I want to import, I type its name, auto-expand it (Control-Space on macOS) and VSC imports it for me. I neither have to know the name of the module nor get its relative path right.

Additionally, I use the “Organize Imports” command (which has a keyboard shortcut that you can look up via the Command Palette) to:

- Remove unused imports.
- Show modules and imported values in a consistent order.

## Manually typing `import` statements  [#](https://2ality.com/2017/08/typing-import-statements.html#manually-typing-import-statements)

When typing import statements manually:

1. I import nothing via `{}` and auto-expand the module specifier:

   ```js
   import {} from "█"
   ```

2. I go back and auto-expand the imported values:

   ```js
   import {█} from './my-module.js';
   ```

## A code snippet for faster entry  [#](https://2ality.com/2017/08/typing-import-statements.html#a-code-snippet-for-faster-entry)

To create a snippet for Visual Studio Code that helps with `import` statements, follow these steps:

1. Execute the menu command `File > Preferences > User Snippets` (Mac: `Code > Preferences > User Snippets`).
2. Pick the language “JavaScript”.
3. Add this property to the JSON file:

   ```js
   "import": {
       "prefix": "imp",
       "body": [
           "import ${2:values} from '${1:specifier}';$0"
       ],
       "description": "import statement"
   }
   ```

Explanation:

- Initially, place the cursor after `from` (position `$1`). The placeholder we’ll see at that position is `specifier`.
- The next time we press the `<tab>` key, the cursor will jump to after `import` (position `$2`).
- The last tab stop is after the semicolon (position `$0`).

Now editing works as follows:

1. `imp <tab>`
2. `import values from '█';`
3. Use auto-expansion.
4. `import values from './my-module.js█';`
5. `<tab>`
6. `import █ from './my-module.js';`
7. `import {█} from './my-module.js';`
8. Use auto-expansion.
9. `import {one, two, three█} from './my-module.js';`
10. `<tab>`
11. `import {one, two, three} from './my-module.js';█`

**Update 2017-09-20:** A similar snippet is now built into Visual Studio Code for `.js(x)` files (previously, only TypeScript was supported ([more information](https://github.com/Microsoft/vscode/pull/34682)).

## Further reading  [#](https://2ality.com/2017/08/typing-import-statements.html#further-reading)

- [Creating your own Snippets in Visual Studio Code](https://code.visualstudio.com/docs/editor/userdefinedsnippets)
- [Chapter “Modules”](http://exploringjs.com/es6/ch_modules.html) in “JavaScript for impatient programmers”
