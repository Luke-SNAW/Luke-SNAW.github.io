---
id: spatdqam58ssnwn2dfx4tox
title: Google Apps Script
desc: ""
updated: 1667289194068
created: 1667286051672
---

## Sheet - Apps script

> https://thenewstack.io/how-to-convert-google-spreadsheet-to-json-formatted-text/

You’ve added your data into the spreadsheet, the next step is to create an [Apps Script](https://developers.google.com/apps-script), a Google Cloud  JavaScript tool to integrate and automate tasks. To do this, click _Extensions > Apps Script_. In the resulting window, paste the following script found in [this Gist](https://gist.githubusercontent.com/pamelafox/1878143/raw/6c23f71231ce1fa09be2d515f317ffe70e4b19aa/exportjson.js).

After pasting the script, click Untitled Document and then name it something like JSON EXPORT. Next, click the _Save_ button to save your work so far. Once it’s saved, click the Run button (**Figure 1**).

**Figure 1:** The run button is the small right-pointing arrow directly to the left of Debug.

When you click Run, you’ll be prompted that the script needs permissions to continue (**Figure 2**).

**Figure 2:** Permissions are always an issue.

Make sure you walk through handing over the proper permissions for the account in question. Curing this process you’ll get a warning that Google hasn’t verified the app. Go ahead and okay that by clicking Advanced and then Go to JSON (unsafe). Finish up the permissions and you’ll be directed back to the Apps Script window.

If you now go back to the spreadsheet and reload it, you should see a new menu entry, labeled Export JSON (**Figure 3**).

**Figure 3:** Our new menu entry for the conversion to JSON.

### Sheet -> i18n JSON

> https://stackoverflow.com/questions/66308153/download-google-sheet-data-as-json-from-browser-through-custom-menu  
> https://stackoverflow.com/a/66308417/5163033

#### Sheet data

| Key                          | ko       | ja     | en      | zh_hant |
| ---------------------------- | -------- | ------ | ------- | ------- |
| company.desc.offices-seoul   | 서울     | ソウル | Seoul   | 首爾    |
| company.desc.offices-fukuoka | 후쿠오카 | 福岡   | Fukuoka | 福岡    |

#### Google Apps Script side:

```js
// Code.gs
const INDEX_LANGUAGE_COLUMNS = {
  ko: 1,
  ja: 2,
  en: 3,
  zh_hant: 4,
};

function onOpen() {
  SpreadsheetApp.getUi()
    .createMenu("JSON")
    .addItem("Export", "download")
    .addToUi();
}

function download() {
  const html = HtmlService.createHtmlOutputFromFile("index");
  SpreadsheetApp.getUi().showModalDialog(
    html,
    "Wait for a while -> 10 seconds +"
  );
}

function downloadFile(language) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const [header, ...values] = sheet.getDataRange().getValues();

  const INDEX_KEY = 0;
  const INDEX_COLUMN = INDEX_LANGUAGE_COLUMNS[language];
  const obj = {};
  values.forEach((raw) => (obj[raw[INDEX_KEY]] = raw[INDEX_COLUMN]));

  const filename = `${sheet.getSheetName()}-${header[INDEX_COLUMN]}.json`;
  const blob = Utilities.newBlob(
    JSON.stringify(obj),
    MimeType.PLAIN_TEXT,
    filename
  );
  return {
    data: `data:${MimeType.PLAIN_TEXT};base64,${Utilities.base64Encode(
      blob.getBytes()
    )}`,
    filename,
  };
}
```

#### HTML&Javascript side:

```html
<!--index.html-->
<script>
  function downloadJsons(languages, indexProcessing) {
    google.script.run
      .withSuccessHandler(({ data, filename }) => {
        if (data && filename) {
          const a = document.createElement("a");
          document.body.appendChild(a);
          a.download = filename;
          a.href = data;
          a.click();
        }
        if (++indexProcessing < languages.length)
          downloadJsons(languages, indexProcessing);
        else google.script.host.close();
      })
      .downloadFile(languages[indexProcessing]);
  }

  downloadJsons(["ko", "ja", "en", "zh_hant"], 0);
</script>
```
