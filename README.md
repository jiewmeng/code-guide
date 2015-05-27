# Coding style guide

Adapted from [Google HTML/CSS Guide](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml) and [Code Guide by @mdo](http://codeguide.co/).

## Tooling

**[EditorConfig](http://editorconfig.org/)** is very useful to ensure the entire team uses consistent coding styles/format. eg. soft or hard tabs. The size of tabs etc.

(sample `.editorconfig`)

```
root = true

[*]
charset = utf-8
end_of_line = lf
insert_final_newline = true
indent_style = tab
indent_size = 2
trim_trailing_whitespace = true
```

The following can validate HTML/CSS respectively but maybe less useful since frameworks/transcompilers tend to be used instead.

- [HTMLHint](https://github.com/yaniswang/HTMLHint) - linter for HTML5
- [CSSLint](https://github.com/CSSLint/csslint) - linter for CSS

## General

### Don't omit optional trailing slash or tags

```html
<!-- not recommended -->
<br>

<!-- recommended -->
<br />

<!-- not recommended -->
<li>testing 1
<li>testing 2

<!-- recommended -->
<li>testing 1</li>
<li>testing 2</li>
```

### Protocol

Omit the protocol portion (http:, https:) from URLs pointing to images and other media files, style sheets, and scripts unless the respective files are not available over both protocols.

Omitting the protocol—which makes the URL relative—prevents mixed content issues and results in minor file size savings.

```html
<!-- Not recommended -->
<script src="http://www.google.com/js/gweb/analytics/autotrack.js"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

```css
/* Not recommended */
.example {
  background: url(http://www.google.com/images/example);
}
/* Recommended */
.example {
  background: url(//www.google.com/images/example);
}
```

### Indentation

Use tabs (enforced via EditorConfig)

## HTML

### Capitalization

Use lower case tag and attribute names

```html
<!-- Recommended -->
<a href="something.png">Something</a>

<!-- Not recommended -->
<A HREF="something.png">Something</A>
```

### Encoding

Use UTF-8

```
<meta charset="utf-8">
```

### Attribute quotes

Use double quotes

```html
<!-- Recommended -->
<a href="something.png">Something</a>

<!-- Not recommended -->
<a href='something.png'>Something</a>
```

### Doctype

Use HTML5

```html
<!DOCTYPE html>
```

### Semantics

Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc.

Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.

```html
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>
<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

### Multimedia fallbacks/accessibility

For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without @alt, and other users may have no way of understanding what video or audio contents are about either.

(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt="".)

```html
<!-- Not recommended -->
<img src="spreadsheet.png">
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

### Entity References

Do not use entity references.

There is no need to use entity references like `&mdash;`, `&rdquo;`, or `&#x263a;`, assuming the same encoding (UTF-8) is used for files and editors as well as among teams.

The only exceptions apply to characters with special meaning in HTML (like `<` and `&`) as well as control or “invisible” characters (like no-break spaces).

```html
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
<!-- Recommended -->
The currency symbol for the Euro is “€”.
```

### Type attributes

Omit type attributes for style sheets and scripts.

Do not use type attributes for style sheets (unless not using CSS) and scripts (unless not using JavaScript).

Specifying type attributes in these contexts is not necessary as HTML5 implies text/css and text/javascript as defaults. This can be safely done even for older browsers.

```html
<!-- Not recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css"
  type="text/css">
<!-- Recommended -->
<link rel="stylesheet" href="//www.google.com/css/maia.css">

<!-- Not recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"
  type="text/javascript"></script>
<!-- Recommended -->
<script src="//www.google.com/js/gweb/analytics/autotrack.js"></script>
```

### General Formatting

Use a new line for every block, list, or table element, and indent every such child element.

Independent of the styling of an element (as CSS allows elements to assume a different role per display property), put every block, list, or table element on a new line.

Also, indent them if they are child elements of a block, list, or table element.

(If you run into issues around whitespace between list items it’s acceptable to put all li elements in one line. A linter is encouraged to throw a warning instead of an error.)

```html
<blockquote>
  <p><em>Space</em>, the final frontier.</p>
</blockquote>
<ul>
  <li>Moe</li>
  <li>Larry</li>
  <li>Curly</li>
</ul>
<table>
  <thead>
    <tr>
      <th scope="col">Income</th>
      <th scope="col">Taxes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>$ 5.00</td>
      <td>$ 4.50</td>
    </tr>
  </tbody>
</table>
```

### Language attribute

From the HTML5 spec:

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.


```html
<html lang="en-us">
```

### IE compatibility mode

Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IE to use the latest supported mode with edge mode.

### Boolean attributes

A boolean attribute is one that needs no declared value. XHTML required you to declare a value, but HTML5 has no such requirement.

For further reading, consult the WhatWG section on boolean attributes:

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.

If you must include the attribute's value, and you don't need to, follow this WhatWG guideline:

> If the attribute is present, its value must either be the empty string or [...] the attribute's canonical name, with no leading or trailing whitespace.

In short, don't add a value.

### Reducing markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML. Take the following example:

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```

## CSS

### ID and class names

Use lower case with dashes separating words. Use meaningful names eg. `.btn` instead of `.b`

```css
.btn-success { }
```

### Valid CSS

Use valid CSS where possible.

Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

Use tools such as the W3C CSS validator to test.

Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

### Hacks

Avoid user agent detection as well as CSS “hacks”—try a different approach first.

It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.

### Indentation

Indent all block content with more than one line.

```css
@media screen, projection {

  html {
    background: #fff;
    color: #444;
  }

  h1 { font-size: 10px; }

}
```

### Semicolons

Use a semicolon after every declaration.

```css
/* Not recommended */
.test {
  display: block;
  height: 100px
}

/* Recommended */
.test {
  display: block;
  height: 100px;
}
```

### Property Name Stops

Use a space after a property name’s colon.

```css
/* Not recommended */
h3 {
  font-weight:bold;
}

/* Recommended */
h3 {
  font-weight: bold;
}
```

### Declaration Block Separation

Use a space between the last selector and the declaration block.

The opening brace should be on the same line as the last selector in a given rule.

```css
/* Not recommended: missing space */
#video{
  margin-top: 1em;
}

/* Not recommended: unnecessary line break */
#video
{
  margin-top: 1em;
}

/* Recommended */
#video {
  margin-top: 1em;
}
```

### Selector and Declaration Separation

Separate selectors and declarations by new lines.

```css
/* Not recommended */
a:focus, a:active {
  position: relative; top: 1px;
}

/* Recommended */
h1,
h2,
h3 {
  font-weight: normal;
  line-height: 1.2;
}
```

### Rule Separation

Separate rules by new lines.

```css
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}
```

### CSS Quotation Marks

Use double quotation marks for attribute selectors and property values.

```css
html {
  font-family: "open sans", arial, sans-serif;
}
```

### 1 declaration per line

Each declaration should appear on its own line for more accurate error reporting.

```css
/* not recommended */
body {
    background: #fff; color: #000;
}

/* recommended */
body {
    background: #fff;
    color: #000;
}
```

### Space after commas

Comma-separated property values should include a space after each comma (e.g., box-shadow).

```
/* not recommended */
box-shadow: box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF;

/* recommended */
box-shadow: box-shadow:0px 1px 2px #CCC, inset 0 1px 0 #FFFFFF;
```

### Lowercase all hex values

```
// not recommended
#FFF

// recommended
#fff
```

### Use shorthand hex values where available

```
// not recommended
#ffffff

// recommended
#fff
```

### Quote attribute values in selectors

```css
/* not recommended */
input[type=text] { }

/* recommended */
input[type="text"] { }
```

### 0 and units

Avoid specifying units for zero values, e.g., margin: 0; instead of margin: 0px;.

```css
/* not recommended */
font-size: 0px;

/* recommended */
font-size: 0;
```

### Don't use `@import`

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

Use concatenation or multiple `<link>` elements

### Media query placement

Place media queries as close to their relevant rule sets whenever possible. Don't bundle them all in a separate stylesheet or at the end of the document. Doing so only makes it easier for folks to miss them in the future. Here's a typical setup.

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

### Shorthand notation

Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values. Common overused shorthand properties include:

- padding
- margin
- font
- background
- border
- border-radius

Often times we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. Excessive use of shorthand properties often leads to sloppier code with unnecessary overrides and unintended side effects.

### Nesting in Less and Sass

Avoid unnecessary nesting. Just because you can nest, doesn't mean you always should. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

### Operators in Less and Sass

For improved readability, wrap all math operations in parentheses with a single space between values, variables, and operators.

```
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

### Comments

Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name.

Be sure to write in complete sentences for larger comments and succinct phrases for general notes.

```css
/* Bad example */
/* Modal header */
.modal-header {
  ...
}

/* Good example */
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
  ...
}
```
