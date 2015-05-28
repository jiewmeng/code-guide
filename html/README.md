# HTML

## Doctype

Use HTML5

```html
<!DOCTYPE html>
```

## Encoding

Use UTF-8

```
<meta charset="utf-8">
```

## Attribute quotes

Use double quotes

```html
<!-- Recommended -->
<a href="something.png">Something</a>

<!-- Not recommended -->
<a href='something.png'>Something</a>
```

## Don't omit optional trailing slash or tags

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

## Capitalization

Use lower case tag and attribute names

```html
<!-- Recommended -->
<a href="something.png">Something</a>

<!-- Not recommended -->
<A HREF="something.png">Something</A>
```

## Language attribute

From the HTML5 spec:

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.


```html
<html lang="en-us">
```

## IE compatibility mode

Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered as. Unless circumstances require otherwise, it's most useful to instruct IE to use the latest supported mode with edge mode.

## Boolean attributes

A boolean attribute is one that needs no declared value. XHTML required you to declare a value, but HTML5 has no such requirement.

For further reading, consult the WhatWG section on boolean attributes:

> The presence of a boolean attribute on an element represents the true value, and the absence of the attribute represents the false value.

If you must include the attribute's value, and you don't need to, follow this WhatWG guideline:

> If the attribute is present, its value must either be the empty string or [...] the attribute's canonical name, with no leading or trailing whitespace.

In short, don't add a value.


## Semantics

Use elements (sometimes incorrectly called “tags”) for what they have been created for. For example, use heading elements for headings, p elements for paragraphs, a elements for anchors, etc.

Using HTML according to its purpose is important for accessibility, reuse, and code efficiency reasons.

```html
<!-- Not recommended -->
<div onclick="goToRecommendations();">All recommendations</div>
<!-- Recommended -->
<a href="recommendations/">All recommendations</a>
```

## Multimedia fallbacks/accessibility

For multimedia, such as images, videos, animated objects via canvas, make sure to offer alternative access. For images that means use of meaningful alternative text (alt) and for video and audio transcripts and captions, if available.

Providing alternative contents is important for accessibility reasons: A blind user has few cues to tell what an image is about without @alt, and other users may have no way of understanding what video or audio contents are about either.

(For images whose alt attributes would introduce redundancy, and for images whose purpose is purely decorative which you cannot immediately use CSS for, use no alternative text, as in alt="".)

```html
<!-- Not recommended -->
<img src="spreadsheet.png">
<!-- Recommended -->
<img src="spreadsheet.png" alt="Spreadsheet screenshot.">
```

## Entity References

Do not use entity references.

There is no need to use entity references like `&mdash;`, `&rdquo;`, or `&#x263a;`, assuming the same encoding (UTF-8) is used for files and editors as well as among teams.

The only exceptions apply to characters with special meaning in HTML (like `<` and `&`) as well as control or “invisible” characters (like no-break spaces).

```html
<!-- Not recommended -->
The currency symbol for the Euro is &ldquo;&eur;&rdquo;.
<!-- Recommended -->
The currency symbol for the Euro is “€”.
```

## Type attributes

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

## General Formatting

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

## Reducing markup

Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML. Take the following example:

```html
<!-- Not so great -->
<span class="avatar">
  <img src="...">
</span>

<!-- Better -->
<img class="avatar" src="...">
```
