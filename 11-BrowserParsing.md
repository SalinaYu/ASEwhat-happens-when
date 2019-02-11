# HTTP Response Processed by the Browser

_Context: We've received an HTTP response to our initial GET request. The Browser is starting to parse this response as well as subsequent responses._

_OSI Layer(s): 7_

**REWORK THIS SLIDE**

Once the server supplies the resources (HTML, CSS, JS, images, etc.) to the browser it undergoes the below process:

![Render Process](https://cdn-images-1.medium.com/max/1600/1*AnqvS3hEk8_CcnVJFZDFEA.png)

* Parsing content - HTML, CSS, JS
* Rendering content - Construct DOM Tree → Render Tree → Layout of Render Tree → Painting the render tree

## HTML parsing

The rendering engine starts getting the contents of the requested document from the networking layer. This will usually be done in [8kB chunks](https://en.wikipedia.org/wiki/Chunked_transfer_encoding).

The primary job of HTML parser to parse the HTML markup into a parse tree.

The output tree (the "parse tree") is a tree of DOM ("Document Object Model") element and attribute nodes. It is the object presentation of the HTML document and the interface of HTML elements to the outside world (like JavaScript). The root of the tree is the "Document" object.

``Chrome Console: document.*``

### The parsing algorithm

HTML cannot be parsed using the regular top-down or bottom-up parsers.

The reasons are:

* The forgiving nature of the language.
* The fact that browsers have traditional error tolerance to support well known cases of invalid HTML.
* The parsing process is reentrant. For other languages, the source doesn't change during parsing, but in HTML, dynamic code (such as script elements containing `document.write()` calls) can add extra tokens, so the parsing process actually modifies the input.

Unable to use the regular parsing techniques, the browser utilizes a custom parser for parsing HTML. The parsing algorithm is described in detail by the HTML5 specification.

The algorithm consists of two stages: tokenization and tree construction.

### Actions when the parsing is finished

The browser begins fetching external resources linked to the page (CSS, images, JavaScript files, etc.).

At this stage the browser marks the document as interactive and starts parsing scripts that are in "deferred" mode: those that should be executed after the document is parsed. The document state is
set to "complete" and a "load" (``onload()``) event is fired.

Have you ever seen an "Invalid Syntax" error on an HTML page? Browsers just "fix" any invalid content and go on.

### CSS interpretation

* Parse CSS files, ``<style>`` tag contents, and ``style`` attribute values using `"CSS lexical and syntax grammar"`
* Each CSS file is parsed into a ``StyleSheet object``, where each object contains CSS rules with selectors and objects corresponding CSS grammar.
* A CSS parser can be top-down or bottom-up when a specific parser generator is used.

``Chrome Console: document.body.style``

_Demonstration Step:_
* Open Chrome Dev Tools Console.
  * Show ``document.location``
  * Show ``document.body``
  * Shoe ``document.body.style``

[Next: Browser Rendering](./12-BrowserRendering.md)

