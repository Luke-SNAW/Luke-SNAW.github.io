
> https://blog.openreplay.com/html-entities-marks-and-emojis/

There is always a need to display special characters as part of your web page content, especially those with pre-defined meanings in HTML. Simply typing these reserved characters within your webpage content will have HTML interpreting them as part of its syntax; hence it will not be rendered as intended. For example, the angular brackets `<>`, commonly known as less than and greater than signs, are part of the syntax for HTML tags.

There is a need to ensure that HTML differentiates between these characters when used as HTML syntax and web content. HTML entities serve this purpose, and this article will show how to use them.

## What are HTML Entities?

HTML Entities refer to the combination of characters/strings/digits that enable special characters, signs, and symbols with special meaning to HTML or not found on the standard keyboard keys to be displayed as web content. HTML Entities are needed in web development to display signs and symbols unavailable in the standard keyboard, such as the copyright symbol, trademark, Greek alphabet, etc. Web developers must observe the correct syntax to embed them within webpage content.

### Examples of HTML Entities

| Symbol | Name                    | Entity name | Entity number | Unicode  | CSS-code |
| ------ | ----------------------- | ----------- | ------------- | -------- | -------- |
| `<`    | Less than sign          | `&lt;`      | `&#60;`       | `U+003C` | `\003C`  |
| `>`    | Greater then sign       | `&gt;`      | `&#62;`       | `U+003E` | `\003D`  |
| `©`    | Copyright sign          | `&copy;`    | `&#169;`      | `U+00A9` | `\00A9`  |
| `®`    | Registered sign         | `&reg;`     | `&#174;`      | `U+00AE` | `\00AE`  |
| `™`    | Trade mark sign         | `&trade;`   | `&#8482;`     | `U+2122` | `\2122`  |
| `½`    | fraction one half       | `&frac12;`  | `&#189;`      | `U+00BD` | `\00BD`  |
| `⅗`    | fraction three quarters | `&frac34;`  | `&#190;`      | `U+00BE` | `\00BE`  |
| `À`    | Capital A, grave accent | `&Agrave;`  | `&#192;`      | `U+00C0` | `\00C0`  |
| `à`    | Small a, grave accent   | `&agrave;`  | `&#224;`      | `U+00E0` | `\00E0`  |

## Six Encoding formats for entities and special characters

To render HTML Entities, web developers may use one of the following encoding formats:

- HTML entities characters or names: text-based and easy to remember.
- HTML entity number/numeric code: number-based and not so easy to remember
- Unicode: number based.
- Hexadecimal or Hex code: number based
- CSS entities: number-based and used when the code to display entities is within the CSS code.
- JS code: number based in octal(base 8) and placed within Javascript code.

### HTML Entities Names and HTML Entities Number

HTML Entities syntax starts with an ampersand (&) and ends with the semicolon (;) as in `&entityName;` or `&#entityNumber;`, as in `&lt;` or `&#060` for the less-than symbol. Every entity has an entity name and corresponding entity number. Therefore, just one is needed to render the required entity. The two HTML codes below give the same result, showing that the HTML entity names and numbers serve the same purpose.

- Text-based entity names are case-sensitive, so always use the correct letter case(upper or lower case).
- Entity names are easier to remember.
- Entity Numbers are greatly supported by most browsers, compared to entity names.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Entities</title>
</head>
<body>
    <p>Less than sign &lt;</p>
    <p>Greater than sign &gt;</p>
    <p>Copyright sign &copy;</p>
    <p>Trademark sign &trade;</p>
    <footer>
        <p>&copy; Nasaski Consults 2022. All rights reserved</p>
    </footer>
</body>
</html
```

Or

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Entities</title>
</head>
<body>
    <p>Less than sign &#60;</p>
    <p>Greater than sign &#62;</p>
    <p>Copyright sign &#169;</p>
    <p>Trademark sign &#8482;</p>
    <footer>
        <p>&copy; Nasaski Consults 2022. All rights reserved</p>
    </footer>
</body>
</html
```

Both will give the same output below:

![1](/images/html-entities-marks-and-emojis/images/image01.png)

A comprehensive table of HTML entities and their corresponding names and numbers [is here.](https://oinam.github.io/entities/)

### Unicode and Hex code

Unicode is the unified and internationally accepted standard for different languages and scripts. It takes into consideration every language possible on Earth and ensures correct interpretation. Every letter, digit, sign, and symbol has assigned unique numeric values applicable across platforms, browsers, and software. For example, the Unicode number, also known as code point, is written thus: U+0398. The U+ signifies Unicode, while the numbers are hexadecimal.

UTF-8 is the most popularly used Unicode encoding system, and it stands for Unicode Transformation Format-8. Its name stems from its ability to translate any Unicode character to its corresponding binary string and vice versa. The eight (8) stems from the fact that UTF-8 represents a character with one byte (8 bits).

It is best practice to specify the encoding system to ensure the correct interpretation and display of strings and entities in the computer memory, files, email, or web page to the user.

In HTML, this is done in the head section, using the meta tag thus:

```html
<head>
  <meta charset="UTF-8" />
</head>
```

The syntax for the use of Unicode for entities starts with an ampersand (&), followed by the letter X, and ends with the semicolon (;) as in `&#XUnicode;`

- The letter X or x is added before the Unicode to denote it is hexadecimal.
- Unicode and Hex Code for HTML entities use the same numbers for each HTML entity.

Provided you use the correct character or code, these all serve the same purpose, as seen in [this comprehensive table.](https://unicode-table.com/en/html-entities/)

The code below illustrates this:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Entities</title>
</head>
<body>
    <p>Less than sign &#X003C;</p>
    <p>Greater than sign &#X003E;</p>
    <p>Copyright sign &#X00A9;</p>
    <p>Trademark sign &#X2122;</p>
    <footer>
        <p>&copy; Nasaski Consults 2022. All rights reserved</p>
    </footer>
</body>
</html
```

Output:

![2](/images/html-entities-marks-and-emojis/images/image02.png)

### CSS Entities

You may use the CSS entity, also called CSS codes, to display HTML entities and special characters. In this case, the code is embedded in CSS script. For instance:

```html
<style>
  h4:after {
    content: " \002122";
  }
</style>
```

The output will be such that all `<h4>` elements will be displayed with the trademark character `™` at the end. Example:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Entities</title>
<Style>
h4:after {
    content: ' \002122';
}
</style>
</Style>
</head>
<body>
    <h4>Written by Chinasa</h4>
    <footer>
        <p>&copy; Nasaski Consults 2022. All rights reserved</p>
    </footer>
</body>
</html>
```

This will produce the output such that all `h4` elements will have the trademark symbol after them.

![3](/images/html-entities-marks-and-emojis/images/image03.png)

Here is the link to a comprehensive table of CSS entities [courtesy of w3school.](https://www.w3schools.com/CSSref/css_entities.php)

### JS code

Developers may use JavaScript code to encode HTML entities. For example, one may achieve this by creating a javascript function that takes the HTML entity name or number as the input parameter and returns the corresponding HTML entity character as output. The code below will return the copyright symbol ©.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>HTML Entity with JS</title>
  </head>
  <body>
    <script>
      //a javascript function that returns html entity
      function htmlentity(input) {
        var parser = new DOMParser().parseFromString(input, "text/html")
        return parser.documentElement.textContent
      }
      // to call the function
      document.write(htmlentity("&copy"))
      //this will return the copyright symbol
    </script>
  </body>
</html>
```

### Diacritical marks

Diacritical marks are little marks, strokes, straight or curvy lines, dots, or a pair of dots added to letters to indicate pronunciation, accent, tone, or stress.

![4](/images/html-entities-marks-and-emojis/images/image04.png)

They are added above or below inside or between two letters. Some language alphabets, such as Latin and French, use diacritical marks, hence the need to render them correctly. For instance, _résumé_ or _resumé_ (career summary) has a different meaning from \*resume (\*to begin again). Words with diacritics in the English language are borrowings from other languages.

You may use the corresponding HTML entity names, numbers, or Unicode to insert Diacritical marks.

| Example | HTML entity name | HTML entity number | Unicode |
| ------- | ---------------- | ------------------ | ------- |
| à       | à                | à                  | \\u00E0 |
| é       | é                | é                  | \\u00E9 |
| î       | î                | î                  | \\u00EE |
| õ       | õ                | õ                  | \\u00F5 |
| ü       | ü                | ü                  | \\u00FC |
| Å       | Å                | Å                  | \\u00C5 |
| ç       | ç                | ç                  | \\u00E7 |

Here is a complete table of diacritical marks and their corresponding [HTML entity names, numbers, and Unicode.](https://www.webatic.com/html-entities-table)

Illustration:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Dicritical Marks</title>
  </head>
  <body>
    <p>&agrave; &eacute; &icirc; &otilde; &uuml; &Aring; &ccedil;</p>
    <p></p>
    <p>&#224; &#233; &#238; &#245; &#252; &#197; &#231;</p>
    <p></p>
    <p>&#x00E0; &#x00E9; &#x00EE; &#x00F5; &#x00FC; &#x00C5; &#x00E7;</p>
    <footer>
      <p>&copy; Nasaski Consults 2022. All rights reserved</p>
    </footer>
  </body>
</html>
```

Output:

![5](/images/html-entities-marks-and-emojis/images/image05.png)

## Emojis

When sending messages electronically or on web pages, conveying emotion, body language, vocal tone, or passing information playfully without using words is necessary. These and more are the jobs of emojis. Examples of emojis are 😃, 🌍, 🚗, 📞 and ❤️. Note that emojis are used and embedded in text fields.

In the 1990s, we had emoticons, made of punctuation marks used to depict jokes/smiley faces :-) and non-jokes/frowning face :-(. Emoticons upgraded to what we now know as Emojis.

Emojis can be embedded in HTML documents using their corresponding HTML entity numbers or Unicode. Here is an emojis table and the corresponding [HTML Entity Number and Unicode.](https://www.w3schools.com/charsets/ref_emoji.asp) and this is a [table of Emoji Smileys](https://www.w3schools.com/charsets/ref_emoji_smileys.asp)

Illustration:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <title>Emojis</title>
  </head>
  <body>
    <h2>Emojis</h2>
    <!--Using HTML Entity Numbers-->
    <p>&#128512; &#9200;</p>
    <!--Using Unicode or Hex-->
    <p>&#x1F618; &#x1F32D;</p>
  </body>
</html>
```

Output:

![6](/images/html-entities-marks-and-emojis/images/image06.png)

### Use of on-screen Keyboard or Emojis Keyboard

An even more convenient way to insert HTML entities and special characters is using the on-screen or emoji keyboard, which is achievable in diverse ways, depending on the operating system.

To launch the emoji keyboard on Mac OS,

- Method 1: use the keyboard shortcut: Command + Control + Space.
- Method 2: Press Option + Command + F5, Select Accessibility Keyboard and Select Done.
- Method 3: In the menu bar, click the Input menu, turn on the Accessibility Keyboard, then select Show Keyboard Viewer.

On Windows 10:

- Method 1: Launch the Emoji keyboard using the keyboard shortcut WIN + full stop(.) or WIN + Semicolon(;)

![12 Emoji keyboard](/images/html-entities-marks-and-emojis/images/image12.png)

- Method 2: Right-click the taskbar and select the Show touch keyboard button from the pull-up menu.

![7](/images/html-entities-marks-and-emojis/images/image07.png)

The on-screen keyboard icon appears on the taskbar.

![8](/images/html-entities-marks-and-emojis/images/image08.png)

Click the icon to open the on-screen keyboard.

![9 On-screen keyboard](/images/html-entities-marks-and-emojis/images/image09.png)

Before the space bar is the emoji button; click this button and select whatever emoji you need to insert at the cursor position.

![10](/images/html-entities-marks-and-emojis/images/image10.png)

Click the Digits/Symbols button just before the Ctrl button for special characters, symbols, diacritics, and Unicode. For example, select the Ohms symbol Ω, and choose the sign you need.
