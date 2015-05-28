# CSS

## SMACSS

Use [SMACSS](https://smacss.com/book/) to organize CSS. As suggested by SMACSS, styles are categorized into 5 types:

- Base
- Layout
- Module
- State
- Theme

### Base

Mainly refers to element/tag selectors for example: `body`, `p` etc. Could be thought as a default style for a type of element.

### Layout

Layout rules divides page into sections housing modules and typically defines width, height, positioning, etc of elements. Prefix layout classes with `l-` for example `.l-flipped`

```css
header, #article, #footer {
    width: 960px;
    margin: auto;
}

article {
    border: solid #CCC;
    border-width: 1px 0 0;
}

.l-flipped #article {
    float: right;
}

.l-flipped #sidebar {
    float: left;
}
```

### Module

A module refers to a reusable component on a page. For example, modals, dropdowns etc.

```
.modal { }

/* avoid element selectors */
.modal div {  }

/* unless you really want all such elements to have that style everytime its used in the module */
.modal p {  }

/* use selectors with semantics */
.modal-header { }
```

#### Subclassing modules

Modules can be subclassed when we want to apply different styles to them depending on the context.

```css
/* default styles for all pods */
.pod {  }

/* styles for "headless" pod */
.pop-headless {  }
```

Usage in HTML

```html
<div class="pod pop-headless">...</div>
```

### States

For styles related to states of components. For example `is-error`, `is-success` etc. Prefix with `is-`

```
.is-error { color: red; }
```

### Theme

Theme style affects the look and feel of the site and typically include styles like `color`, `background`, `font-family` etc

```css
body {
    background: white;
    color: #333;
    font-family: helvatica, arial, sans-serif;
}

.modal-header {
    padding: 10px;
    color: orange;
    font-weight: bold;
    font-style: italic;
}
```

### SMACSS Concepts

#### Depth of applicability

Higher depth tends to mean higher dependency to a particular HTML structure

```css
/* not so great: imagine what happens when instead of using h2 we want to use a h1 */
body .module header h2 .title {  }

/* better */
.module .title { }
```

#### How CSS is evaluated

##### From right to left

- So right-most selector should not refer to too many elements on the page. For example, `.module span` can be very slow if there are alot of spans on the page
- Single selector is faster than a string of selectors `.list-link` vs `#nav ul ul ul li .list-link`

##### On element creation

As browser parses HTML it evaluates styles for the element.

## ID and class names

Use lower case with dashes separating words. Use meaningful names eg. `.btn` instead of `.b`

```css
.btn-success { }
```

## Indentation

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

## Semicolons

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

## Property Name Stops

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

## Declaration Block Separation

Use a space between the last selector and the declaration block.

The opening brace should be on the same line as the last selector in a given rule.

```css
/* Not recommended: missing space */
video{
  margin-top: 1em;
}

/* Not recommended: unnecessary line break */
video
{
  margin-top: 1em;
}

/* Recommended */
video {
  margin-top: 1em;
}
```

## Selector and Declaration Separation

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

## Rule Separation

Separate rules by new lines for better error reporting

```css
html {
  background: #fff;
}

body {
  margin: auto;
  width: 50%;
}

/* except for styles with only one rule */
h1 { font-size: 12px; }
```

## CSS Quotation Marks

Use double quotation marks for attribute selectors and property values.

```css
html {
  font-family: "open sans", arial, sans-serif;
}
```

## Space after commas

Comma-separated property values should include a space after each comma (e.g., box-shadow).

```
/* not recommended */
box-shadow: box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF;

/* recommended */
box-shadow: box-shadow:0px 1px 2px #CCC, inset 0 1px 0 #FFFFFF;
```

## Lowercase all hex values

```
// not recommended
FFF

// recommended
fff
```

## Use shorthand hex values where available

```
// not recommended
ffffff

// recommended
fff
```

## Quote attribute values in selectors

```css
/* not recommended */
input[type=text] { }

/* recommended */
input[type="text"] { }
```

## 0 and units

Avoid specifying units for zero values, e.g., margin: 0; instead of margin: 0px;.

```css
/* not recommended */
font-size: 0px;

/* recommended */
font-size: 0;
```

## Don't use `@import`

Compared to `<link>`s, `@import` is slower, adds extra page requests, and can cause other unforeseen problems. Avoid them and instead opt for an alternate approach:

Use concatenation or multiple `<link>` elements

## Media query placement

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

## Shorthand notation

Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values. Common overused shorthand properties include:

- padding
- margin
- font
- background
- border
- border-radius

Often times we don't need to set all the values a shorthand property represents. For example, HTML headings only set top and bottom margin, so when necessary, only override those two values. Excessive use of shorthand properties often leads to sloppier code with unnecessary overrides and unintended side effects.

## Nesting in Less and Sass

Avoid unnecessary nesting. Just because you can nest, doesn't mean you always should. Consider nesting only if you must scope styles to a parent and if there are multiple elements to be nested.

## Operators in Less and Sass

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

## Comments

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

## Valid CSS

Use valid CSS where possible.

Unless dealing with CSS validator bugs or requiring proprietary syntax, use valid CSS code.

Use tools such as the W3C CSS validator to test.

Using valid CSS is a measurable baseline quality attribute that allows to spot CSS code that may not have any effect and can be removed, and that ensures proper CSS usage.

## Hacks

Avoid user agent detection as well as CSS “hacks”—try a different approach first.

It’s tempting to address styling differences over user agent detection or special CSS filters, workarounds, and hacks. Both approaches should be considered last resort in order to achieve and maintain an efficient and manageable code base. Put another way, giving detection and hacks a free pass will hurt projects in the long run as projects tend to take the way of least resistance. That is, allowing and making it easy to use detection and hacks means using detection and hacks more frequently—and more frequently is too frequently.
