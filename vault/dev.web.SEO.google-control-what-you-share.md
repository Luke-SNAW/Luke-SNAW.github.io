---
id: 4a11sk1x918a7tk4fgz5xkg
title: Control what you share with Google
desc: ""
updated: 1672098253227
created: 1672098099425
---

> https://developers.google.com/search/docs/crawling-indexing/control-what-you-share

Control what information Google sees on your site and what is shown in search results. There are a few reasons you might want to hide content from Google:

- **To keep data private**
- **To hide content of less value to your audience**
- **To have Google focus on your important content**

## How to block content

### Remove the content

**For all content types**

Removing content from your site is the best way to ensure that it won't appear in Google Search, or anywhere. If the information is already appearing in Google, you might need to [take additional steps](https://developers.google.com/search/docs/crawling-indexing/remove-information) to make your removal permanent.

### Password-protect your files

**For all content types**

If you have confidential or private content that you don't want to appear in Google search results, the simplest and most effective way to block private URLs from appearing is to store them in a password-protected directory on your site server. Googlebot and all other web crawlers are unable to access content in password-protected directories.

**Advanced users:** If you're using Apache Web Server, you can edit your `.htaccess` file to password-protect the directory on your server. There are a lot of tools on the web that can help you do this.

### robots.txt and/or emergency image removal request

**For images**

Use [robots.txt rules to block images](https://developers.google.com/search/docs/crawling-indexing/prevent-images-on-your-page).

[`noindex` directive](https://developers.google.com/search/docs/crawling-indexing/block-indexing)

**For web pages**

`noindex` is a technique that tells Google not to read your page or let it appear in Google search results. Your pages can still be linked to and visited through other web pages, or directly visited by users with a link, but the pages will not appear in Google search results. This method requires technical savvy, and may not be available if you use a content management system to host your site.

[Opt out of specific Google properties](https://support.google.com/webmasters/answer/3035947)

**For web pages**

You can tell Google not to include content from your site in specific Google properties, rather than all Google properties.

### [`nosnippet` meta tag](https://developers.google.com/search/docs/appearance/snippet#nosnippet)

**For Search result snippets**

Add the `<meta name="robots" content="nosnippet">` tag to your page's HTML `head` section to prevent a snippet from appearing in Search. However, note that this can generate a confusing message in search results ("No information is available for this page").
