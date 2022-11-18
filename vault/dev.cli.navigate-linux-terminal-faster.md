---
id: lptq5mubxtlhliuzn2k56t8
title: My favorite tricks for navigating the Linux terminal faster
desc: ""
updated: 1668642334697
created: 1668641971357
---

> https://opensource.com/article/22/11/navigate-linux-terminal-faster

## Navigate without the arrow keys

**Shortcuts:**

- Instead of *Left arrow, left, left, left*, use **CTRL+A** to go to the start of the line or **Alt+B** to move back one word.
- Instead of *Right arrow, right, right, right*, use **CTRL+E** to move to the end of the line, or **Alt+F** to move forward a word.

## Don't use the backspace or delete keys

Use **CTRL+U** to erase everything from the current cursor position to the beginning of the line. Similarly, **CTRL+K** erases everything from the current cursor position to the end of the line.

**Shortcuts:**

- Instead of *Backspace*, use **CTRL+U**.
- Instead of *Delete*, use **CTRL+K**.

## Execute multiple commands in a single line

**Shortcuts:**

- Instead of:

  ```shell
  $ git add .
  $ git commit -m "message"
  $ git push origin main
  ```

  Use:

  ```shell
  $ git add .;git commit -m "message";git push origin main
  ```

- Use the `;` symbol to concatenate and execute any number of commands in a single line. To stop the sequence of commands when one fails, use `&&` instead:
  ```shell
  $ git add . && git commit -m "message" && git push origin main
  ```

## Alias frequently used commands

To create an alias, open your `.bashrc` file in your favorite editor and add an alias:

```shell
alias gpom= "git push origin main"
```

Try creating an alias for anything you run regularly.

Note: The `.bashrc` file is for users using the Bash shell. If your system runs a different shell, you probably need to adjust the configuration file you use and possibly the syntax of the alias command. You can check the name of the default shell in your system with the `echo $SHELL` command.

After creating the alias, reload your configuration:

```shell
$ . ~/.bashrc
```

And then try your new command:

```shell
$ gpom
```

## Search and run a previous command without using the arrow keys

**Shortcuts:**

- Instead of *Up arrow, up, up, up, Enter*, type `history`, and then look for the `history-number` of the command you want to run:

  ```shell
  $ !{history-number}
  ```

- You can also perform this task a different way: Instead of: *Up arrow, up, up, up, Enter*, use **CTRL+R** and type the first few letters of the command you want to repeat.
