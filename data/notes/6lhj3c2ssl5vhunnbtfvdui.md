
> https://www.akshaykhot.com/base64-encoding-explained/
>
> Base64 encoding converts binary data like images and files into standard ASCII text for easy storage and transmission. It represents binary data in a reduced set of 64 characters to prevent corruption. Every 6 bits of binary data is represented by a single Base64 character, with padding added as needed. Data URLs allow embedding Base64 encoded images and files directly into HTML.

Base64 is an elegant way to convert binary data to text, making it easy to store and transport. This article covers the basics of Base64 encoding, including what it is, how it works and why it's important.

## What is Base64 Encoding?

Base64 encoding takes binary data and converts it into text, specifically ASCII text. The resulting text contains only letters from `A-Z`, `a-z`, numbers from `0-9`, and the symbols `+` and `/`.

As there are 26 letters in the alphabet, we have `26 + 26 + 10 + 2` characters. Hence this encoding is named **`Base64`**. These 64 characters are considered "safe", that is, they cannot be misinterpreted by legacy computers and programs unlike characters such as `<`, `>`, `\n` and many others.

> 💡 Here's what the text "Ruby on Rails" looks like when Base64 encoded: **UnVieSBvbiBSYWlscw==**.

**It's important to remember that we are not encrypting the text here.** Given Base64 encoded data, it's very easy to convert it back (decode) to the original text. We are only changing the representation of the data, i.e. encoding.

In its essence, Base64 encoding uses a specific, reduced set of characters to encode binary data, to prevent against data corruption.

[The Base64 Alphabet](https://www.akshaykhot.com/content/images/2023/10/base64_encoding.png)

As there are only 64 characters available to encode into, we can represent them using only 6 bits, because `2^6 = 64`. Every Base64 digit represents 6 bits of data. There are 8 bits in a byte, and the closest common multiple of 8 and 6 is 24. So 24 bits, or 3 bytes, can be represented using four 6-bit Base64 digits.

_(If that last paragraph totally went over your head, **don't worry**. Hopefully it should be clear by the end of this post.)_

## Why Base64?

You must have included an image in your HTML document using the `<img src="nature.jpeg">` tag. **Did you know you can embed the image data directly into the HTML without linking to the external image file?** [Data URLs](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs?ref=akshaykhot.com) let you do this, and they use Base64 encoded text to embed files inline.

```html
<img src="data:image/gif;base64,xxxxbase64encodedtextxxxx" />

data:[<mime type
  >][;charset=<charset>][;base64],<encoded data></encoded></charset
></mime>
```

Historically it has been used to encode binary data in email messages where the email server might modify line-endings. A more modern example is the use of Base64 encoding to [embed image data directly in HTML source code](http://www.sweeting.org/mark/blog/2005/07/12/base64-encoded-images-embedded-in-html?ref=akshaykhot.com). Here it is necessary to encode the data to avoid characters like '<' and '>' being interpreted as tags.

From: [Why do we use Base64?](https://stackoverflow.com/questions/3538021/why-do-we-use-base64?ref=akshaykhot.com)

Another common use case is when we have to store or transmit some binary data over the network that's supposed to handle text, or US-ASCII data. This ensures data remains unchanged during transport. Base64 can also be used for passing data in URLs when that data includes non-URL friendly characters.

Base encoding is also used in many applications simply because it makes it possible to manipulate objects with text editors.

You can also transfer files as text, using Base64 encoding. First, get the file's bytes and encode them as Base64. Then transfer the Base64 encoded string, and then decode it back to the original file content on the receiving side.

Let's take a deeper look into this algorithm in the next section.

## Base64 Encoding Algorithm

Here's the simple algorithm that converts some text into Base64.

1. Convert the text to its binary representation.
2. Divide the bits into groups of 6 bits each.
3. Convert each group to a decimal number from 0-63. It cannot be greater than 64 as there are only 6 bits in each group.
4. Convert this decimal number to the equivalent Base64 character using the Base64 alphabet.

That's it. You have a Base64 encoded string. If there're insufficient bits in the final group, you can use `=` or `==` as padding.

Sounds confusing? Don't worry, the following example should make it pretty clear. Let's convert my name "Akshay" to its Base64 equivalent string.

- Convert the text "Akshay" to binary by first converting each character to its corresponding [ASCII number](https://www.ascii-code.com/?ref=akshaykhot.com) and then converting that decimal number to binary (or just use [this tool](https://www.rapidtables.com/convert/number/ascii-to-binary.html?ref=akshaykhot.com)):

```text
01000001 01101011 01110011 01101000 01100001 01111001

   A        k        s        h        a        y
```

- Divide the bits into groups of 6 bits:

```text
010000 010110 101101 110011 011010 000110 000101 111001
```

- Convert each group to a decimal number between 0 to 63:

```text
010000 010110 101101 110011 011010 000110 000101 111001

  16     22     45     51     26     6      5      57
```

- Now use the Base64 alphabet (see above image) to convert each decimal number to its Base64 representation:

```text
16  22  45  51  26  6  5  57

Q   W   t   z   a   G  F  5
```

And we're done. The name "Akshay" is represented in Base64 as `QWtzaGF5`.

At first glance, the benefit of Base64 encoding is not quite obvious. **What exactly did we achieve by converting "Akshay" to "QWtzaGF5"?**

Imagine, instead of my name, you had an image or a sensitive file (PDF, text, video, anything, really), and you wanted to store it as text. You could first convert it to binary, and then Base64 encode it to get corresponding ASCII text.

Now you could send or store that text anywhere and anyhow you like, without worrying whether some legacy device, protocol or software won't misinterpret the raw binary data to corrupt your file. Makes sense?
