## __HTML__

- IN `HTML` `hypertext`  refers to links that connect web pages to one another.

- HTML uses `"markup"` to annotate text, images, and other content for display in a Web browser.

- An HTML element is set off from other text in a document by `"tags"`.

- `<!doctype html>`:  Its sole purpose is to prevent a browser from switching into so-called `"quirks mode"` browser makes a best-effort attempt at following the relevant specifications, rather than using a different rendering mode that is incompatible with some specifications.

- `<meta name="viewport" content="width=device-width">`: This viewport element ensures the page renders at the width of the browser viewport, preventing mobile browsers from rendering pages wider than the viewport and then shrinking them down.

- `quirk mode`: When the web standards were made at W3C, browsers could not just start using them, as doing so would break most existing sites on the web. Browsers therefore introduced two modes to treat new standards compliant sites differently from old legacy sites.

Quirks mode means your page is running without a document type declared, the document type is defined at the very top of a page and it denotes how the browser should read the HTML. This is StackOverflow's doctype:

`<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" `


  `refer`: [quirk_mode_and standard_modes](https://developer.mozilla.org/en-US/docs/Web/HTML/Guides/Quirks_mode_and_standards_mode)

 ## XHTML 
 - If you serve your page as `XHTML` using the `application/xhtml+xml` MIME type in the Content-Type HTTP header, you do not need a doctype to enable no-quirks mode, as such documents always use no-quirks mode.

If you serve XHTML-like content using the `text/html` MIME type, browsers will read it as HTML, and you will need the doctype to use no-quirks mode.

In practice, very few "XHTML" documents are served over the web with a `Content-Type: application/xhtml+xml` header. Instead, even though the documents are written to conform to XML syntax rules, they are served with a `Content-Type: text/html header` — so browsers parse those documents using` HTML parsers rather than XML parsers.`

