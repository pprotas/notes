---
id: browsers
aliases:
  - Browsers
tags: []
---

# Browsers

Browsers are some of the most widely used software. Their main function is to fetch the user's chosen resource from a server, and present it in the browser window.

The most common browsers today are Chrome (and its derivatives), Firefox and Safari.

## Displaying Resources

Usually, the displayed resource is an HTML document, but it can also be a PDF, image, or some other type of document. The location of the resource is specified by the user using a Uniform Resource Identifier (URI).

The browser interprets and displays HTML files according to specifications maintained by the World Wide Web Consortium (W3C). This is the standards organization for the web, and browsers conform to these specifications in varying degrees.

## Interface

Most browser have some kind of search bar, the actual browser window, a way to manage different tabs, and other tools like bookmarks, history or downloads managers. The most common browsers are very similar in their interface and features, with some differences here and there that may be important to different types of users.

The browser's interface is not specified in any formal specifications, so browser vendors are free to create their browser interface as they like, and companies like Arc create browsers with unique interfaces.

## Main Components

The browser's main components are:

1. _The user interface_: this includes every part of the browser display except the window where you see the requested page.
2. _The browser engine_: this marshals actions between the UI and the rendering engine.
3. _The rendering engine_: this displays the requested content. For example, if the requested content is HTML, the rendering engine parses HTML and CSS, and displays the parsed content on the screen.
4. _Networking_: this handles network calls, such as HTTP requests, using different implementations for different platforms behind a platform-independent interface.
5. _UI backend_: used for drawing basic widgets like combo boxes and windows. This backend exposes a generic interface that is not platform specific. Underneath it uses operating system user interface methods.
6. _JavaScript interpreter_: used to parse and execute JavaScript code.
7. _Data storage_: this is a persistence layer. The browser needs to save all sorts of data on the user's disk, such as cookies, bookmarks, and history.

![Browser components](/public/images/browser-components.png "Browser components")
