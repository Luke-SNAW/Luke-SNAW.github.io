---
id: 19132lpvnc3tbkz7ndlrut5
title: Strikethrough Accessibility
desc: ""
updated: 1699599679218
created: 1699599535276
---

> https://www.webaxe.org/strikethrough-html-accessibility/

Strikethrough [`<s>`](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-s-element) is an HTML element to indicate text that is crossed out – usually indicated visually with a line through the middle of the text. The W3C definition is:

> The s element represents contents that are no longer accurate or no longer relevant.

On e-commerce websites, a strikethrough element is often used to indicate a price is no longer valid and often has a reduced price next to it.

> [Screenshot of two similar examples of a product with an active and crossed out price. A red arrow points to each of the crossed out prices.](http://www.webaxe.org/wp-content/uploads/2023/10/ex-price-strike-udemy-1024x608.png)

The problem is that most screen readers don’t output the strikethrough semantics. This can be very problematic to the blind user since they won’t know which price is valid. Most in-line semantic elements such as `<em>` and `<mark>` are not conveyed to screen readers actually. For more on that, reference the article [Screen Readers support for text level HTML semantics](https://www.tpgi.com/screen-readers-support-for-text-level-html-semantics/) by TPGi.

Let’s examine four test cases and the level of support. Note that the strikethrough element is [mapped to the deletion ARIA role](https://w3c.github.io/html-aam/#el-s) which we’ll use in test Scenario 2.

### Test Cases

Four code scenarios were tested against 6 screen reader/browser/OS combinations including VoiceOver, NVDA, JAWS, and TalkBack. The actual test cases used are in the second portion of the CodePen [Negative number and strikethru tests](https://codepen.io/weboverhauls/full/vYvPxOM).

#### Scenario 1: strikethrough element only

Price: ~~$200~~ $100

`Price: <s>$200</s> $100`

The plain old semantic HTML—an S element around the text. This is obviously the ideal code, but support isn’t quite there yet. Only NVDA and TalkBack passed.

#### Scenario 2: strikethrough with ARIA ‘deletion’ role

Price: ~~$200~~ $100

`Price: <s role="deletion">$200</s> $100`

This is similar to Scenario 1, but with the addition of role=”deletion”. The test results were similar to without the role. The only difference is that VoiceOver on iOS also passed.

#### Scenario 3: strikethrough with visually hidden text

Price: original price~~$200~~ sale price$100

`Price: <span class="visually-hidden">original price</span><s>$200</s> <span class="visually-hidden">sale price</span>$100`

This test case uses the old school technique of visually hiding text via CSS. “Original price” outputs before the price with the strikethrough, and “Sale price” outputs before the valid price.

All screen readers passed this scenario.

#### Scenario 4: strikethrough with visually hidden pseudo-content

Price: ~~$200~~ $100

`Price: <s>$200</s> $100`

```css
#pseudo s::before {
  content: " [start of stricken text] ";
}

#pseudo s::after {
  content: " [end stricken text] ";
}

#pseudo s::before,
#pseudo s::after {
  clip-path: inset(100%);
  clip: rect(1px, 1px, 1px, 1px);
  height: 1px;
  width: 1px;
  overflow: hidden;
  position: absolute;
  white-space: nowrap;
}
```

The fourth test case has the same HTML has Scenario 1. But then applies a brilliant method by Adrian Roselli introduced in 2017 in the article [Tweaking Text Level Styles](https://adrianroselli.com/2017/12/tweaking-text-level-styles.html#S). Pseudo-content (creating a textual phrase via CSS) is used to indicate when the strikethrough starts and ends.

There are a couple issues to mention with this approach:

1. Since NVDA now supports the strikethrough tag, it indicates the semantics twice — both the S element semantics (“deleted”) and the pseudo-content (“start of stricken text”) which creates ambiguity for the user.
   1. Oddly, the double semantics is _not_ conveyed by TalkBack which _did_ pass the previous three scenarios.
2. With JAWS, the output is broken up with multiple stops which makes it difficult to follow. (Changing the brackets to parentheses might help.)

This technique technically works for all screen readers, but the user experience is very confusing for NVDA users.

### Test Results

Does screen reader output “deleted”, “stricken”, or similar?

<table style="font-size: .8em; min-width: 44em;"><tbody><tr><td></td><th>iOS + Safari + VO</th><th>MacOS + Safari + VO</th><th>Android + Chrome + TalkBack</th><th>Win + Chrome + NVDA</th><th>Win + Firefox + NVDA</th><th>Win + Chrome + JAWS</th></tr><tr><th style="min-width: 7em;">Scenario 1</th><td>No</td><td>No</td><td>Yes</td><td>Yes</td><td>Yes</td><td>No</td></tr><tr style="background: rgba(239, 239, 239, .7);"><th>Scenario 2</th><td>Yes</td><td>No</td><td>Yes</td><td>Yes</td><td>Yes</td><td>No</td></tr><tr><th>Scenario 3</th><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td></tr><tr style="background: rgba(239, 239, 239, .7);"><th>Scenario 4</th><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td><td>Yes</td></tr></tbody></table>

### Conclusion

NVDA has the best support for `<s>`, the strikethrough element. For now, to best support screen readers overall, we should continue to use Scenario 3 — strikethrough with visually hidden text — to programmatically convey strikethrough semantics. Doing so will ensure that everyone understands strikethrough semantics while browsing the web which often means knowing the correct price of a product or service.

### Further reading

- [Ensuring negative numbers are available for everyone](https://www.deque.com/blog/ensuring-negative-numbers-are-available-for-everyone/) via Deque Systems
- [How To Use Inline-level and Block-level Elements in HTML](https://www.digitalocean.com/community/tutorials/how-to-use-inline-level-and-block-level-elements-in-html) by DigitalOcean
