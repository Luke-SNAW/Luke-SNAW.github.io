
## Collection

- [Parallelism](https://playwright.dev/docs/test-parallel)
  > [`test.describe.configure({ mode: 'parallel' });`](https://playwright.dev/docs/api/class-test#test-describe-configure)

## Snippets

### Wait

```js
// wait for 1 second https://playwright.dev/docs/api/class-page#page-wait-for-timeout
await page.waitForTimeout(1000)
```

### [Create tests via a CSV file](https://playwright.dev/docs/test-parameterize#create-tests-via-a-csv-file)

The Playwright test-runner runs in Node.js, this means you can directly read files from the file system and parse them with your preferred CSV library.

See for example this CSV file, in our example `input.csv`:

```csv
"test_case","some_value","some_other_value"
"value 1","value 11","foobar1"
"value 2","value 22","foobar21"
"value 3","value 33","foobar321"
"value 4","value 44","foobar4321"
```

Based on this we'll generate some tests by using the [csv-parse](https://www.npmjs.com/package/csv-parse) library from NPM:

```ts
// test.spec.ts
import fs from "fs"
import path from "path"
import { test } from "@playwright/test"
import { parse } from "csv-parse/sync"
const records = parse(fs.readFileSync(path.join(__dirname, "input.csv")), {
  columns: true,
  skip_empty_lines: true,
})
for (const record of records) {
  test(`foo: ${record.test_case}`, async ({ page }) => {
    console.log(record.test_case, record.some_value, record.some_other_value)
  })
}
```

## Performance

### [Why "page.goto()" is slowing down your Playwright tests](https://www.checklyhq.com/blog/why-page-goto-is-slowing-down-your-playwright-test/)

```js
// Wait until the HTML starts loading.
await page.goto("/", { waitUntil: "commit" })

// Wait until the HTML is parsed
// and deferred scripts (`<script deferred>` and `<script type="module">`) are loaded.
await page.goto("/", { waitUntil: "domcontentloaded" })

// Wait until all initially included resources are loaded.
await page.goto("/", { waitUntil: "load" })

// Wait until every resource is loaded and the network is silent for 500ms.
await page.goto("/", { waitUntil: "networkidle" })
```
