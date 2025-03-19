---
id: 7uuid3nck5c8r1ngjm8o254
title: Recommendations for designing magic numbers of binary file formats
desc: ""
updated: 1742255419747
created: 1742255301611
---

> https://hackers.town/@zwol/114155595855705796 — Zack Weinberg

another day, another binary file format with a badly designed magic number

not gonna call it out specifically but here are some RFC2119 MUSTs for magic number design:

- MUST be the very first N bytes in the file
- MUST be at least four bytes long, eight is better
- MUST include at least one byte with the high bit set
- MUST include a byte sequence that is invalid UTF-8
- SHOULD include a zero byte, but you can usually get away with having that be part of the overall version number that immediately follows the magic number (did I mention that you really SHOULD put an overall version number right after the magic number, unless you know and have documented exactly why it's not necessary, e.g. PNG?)

good examples:

- PNG
- ELF

bad examples:

- GIF
- PE
- PDF

---

Here is a template. If you follow this template for your binary file format's magic number, you will be doing it better than a depressingly large number of senior software engineers.

First eight bytes of the file:

```
0xDC 0xDF X X x x (0x01 0x00 | 0x00 0x01)
```

`0xDC 0xDF` are bytes with the high bit set. Together with the next two bytes, they form a four-byte sequence that cannot appear in any valid ASCII, UTF-8, Corrected UTF-8, or UTF-16 (regardless of endianness) text document. This is not a perfectly bulletproof declaration that the file does not contain text, but it should be strong enough except maybe for formats like PDF that can't decide if they're structured text or binary.

`X X x x`: Four ASCII alphanumeric characters naming your file format. Make them clearly related to your recommended file name extension. I'm giving you four characters because we're running out of three-letter acronyms. If you don't need four characters, pad at the end with `0x1A` (aka `^Z`).

The first two of these (the uppercase Xes) must _not_ have their high bits set, lest the "this is not text" declaration be weakened. For the other two (lowercase xes), use of ASCII alphanumerics is just a strong recommendation.

`0x01 0x00` or `0x00 0x01`: This is to be understood as a 16-bit unsigned integer in your choice of little- or big-endian order. It serves three functions. In descending order of importance:

1. It includes a zero byte, reinforcing the declaration that this is not a text file.
2. It demonstrates which byte ordering will be used throughout the file. It does not matter which order you choose, but you need to consciously choose either big- or little-endian and then _use that byte order consistently throughout the file_. Yes, I have seen cases where people didn't do that.
3. It's an escape hatch. If one day you discover that you need to alter the structure of the rest of the file in a totally incompatible way, and yet it is still meaningfully the same format, so you don't want to change the name characters, you can change the `0x01` to `0x02`. We both hope that day will never come, but we both know it might.
