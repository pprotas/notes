---
id: parsing
aliases:
  - Parsing
tags: []
---

# Parsing

Once the browser receives its first chunk of data, it can start parsing the HTML. Parsing means that the browser is turning HTML into a DOM and a CSSOM, which is used by the renderer to paint a page on the screen.

The DOM is the internal representation of the markup for the browser. JavaScript can also interact with and manipulate the DOM through various APIs.

The initial window size in TCP is usually around 14KB. Because of this, the first chunk of data received will only be of that size. Even if the initial page is bigger than that, the browser will already start parsing at the first chunk of data. For web performance optimization, it is important that this first 14 KB chunk of data includes everything the browser needs to start rendering the page.

## Building the DOM tree

First, the HTML markup is processed into the DOM tree. The tree is constructed from the HTML elements, which are tokenized. These HTML tokens include start and end tags, as well as attribute names and values.

The DOM tree describes the content of the document. The `<html>` element is the first element and root node of the DOM tree. Since the tree reflects the hierarchy between different elements, child nodes of the tree represent HTMLi elements nested within other elements.

Parsing can be interrupted by `<script>` tags without `async` or `defer` attributes. Non-blocking operations, like parsing CSS, do not interrupt the parsing.

## Preload scanner

As the browser is parsing the HTML, it will also start downloading the linked resources, for example images. We don't have to wait for the entire HTML to be parsed, and we don't have to wait for the parser on the main thread to come across these resources either. This is because the preload parser looks ahead in the document, and looks for resources that will have to be downloaded. This could be `<link>` tags with stylesheets, `<img>` tags, `<script>` tags, etc.

## Building the CSSOM tree

The CSS object model is similar to the DOM. They are both trees. They are independent data structures. The browser converts the CSS stylesheets into a map of styles it can work with. The browser goes through each CSS rule set and creates a tree of nodes with parent, child and sibling relationships based on the CSS selectors.

The browser styles an element on the page by applying the most general rule first, and then cascading down the CSSOM tree to the most specific rule possible. That's where the word "cascading" comes from in CSS.
