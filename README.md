# Coding style guide

Adapted from [Google HTML/CSS Guide](https://google-styleguide.googlecode.com/svn/trunk/htmlcssguide.xml), [Code Guide by @mdo](http://codeguide.co/) and SMACSS.

## General

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
