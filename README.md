# Orus HTML Style Guide

This is a part of Orus fronted guidelines.

## HTML


Accessibility shouldn't be an afterthought. You don't have to be a [Web Content Accessibility Guidelines (WCAG)](https://www.w3.org/WAI/intro/wcag) expert to improve your website, you can start immediately by fixing the little things that make a huge difference.

### General formatting

- Use soft-tabs with a two space indent.
- Paragraphs of text should always be placed in a `<p>` tag.
- Never use multiple `<br>` tags.
- Items in list form should always be in `<ul>`, `<ol>`, or `<dl>`. Never use a set of `<div>` or `<p>`.
- Every form input that has text attached should utilize a `<label>` tag. Especially radio or checkbox elements.
- Even though quotes around attributes is optional, always put quotes around attributes for readability.
- Avoid writing closing tag comments, like ` <!-- /.element --> `. This just adds to page load time. Plus, most editors have indentation guides and open-close tag highlighting.
- Avoid trailing slashes in self-closing elements. For example, ` <br> `, ` <hr> `, ` <img> `, and ` <input> `.
- Don’t set ` tabindex ` manually—rely on the browser to set the order.
- Learn to use the ` alt ` attribute properly
- Make sure your links and buttons are marked as such (no `<p class=button>` atrocities)
- Do not rely exclusively on colors to communicate information
- Explicitly label form controls
- Whenever possible, avoid superfluous parent elements when writing HTML. Many times this requires iteration and refactoring, but produces less HTML
- Many attributes don’t require a value to be set, like disabled or checked, so don’t set them.
- Make use of `<thead>`, `<tfoot>`, `<tbody>`, and `<th>` tags (and scope attribute) when appropriate. (Note: `<tfoot>` goes above `<tbody>` for speed reasons. You want the browser to load the footer before a table full of data.)


```html
<!-- Not so good -->
<h1>
  <span class=avatar>
    <img src=avatar.png />
  </span>
</h1>
<!-- /h1 -->
<input type=text disabled=disabled>
 
<!-- Better -->
<img class="avatar" alt="John Doe" src="avatar.png">
<input type="text" disabled>
```

or...

```html
<!-- Not so good -->
<table summary="This is a chart of invoices for 2016.">
  <thead>
    <tr>
      <th scope=col>Table header 1</th>
      <th scope=col>Table header 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Table data 1</td>
      <td>Table data 2</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Table footer 1</td>
      <td>Table footer 2</td>
    </tr>
  </tfoot>
</table>
 
<!-- Better -->
<table summary="This is a chart of invoices for 2016.">
  <thead>
    <tr>
      <th scope="col">Table header 1</th>
      <th scope="col">Table header 2</th>
    </tr>
  </thead>
  <tfoot>
    <tr>
      <td>Table footer 1</td>
      <td>Table footer 2</td>
    </tr>
  </tfoot>
  <tbody>
    <tr>
      <td>Table data 1</td>
      <td>Table data 2</td>
    </tr>
  </tbody>
</table>
```

### Forms
For better readability, keep your form as simple and descriptive as possible by following theses rules :
- Lean towards `radio` or `checkbox` lists instead of `select` menus.
- Wrap `radio` and `checkbox` inputs and their text in `label` s. No need for `for` attributes here — the wrapping automatically associates the two.
- Form buttons should always include an explicit type. Use primary buttons for the `type="submit"` button and regular buttons for ` type="button"`.
- The primary form button must come first in the DOM, especially for forms with multiple submit buttons. The visual order should be preserved with `float: right;` on each button.

### Semantics
HTML5 come along with lots of semantics elements made to describe precisely the content. Make sure you profit from its well designed vocabulary.

```html
<!-- Not so good -->
<div class="wrap">
  <div class="post">
    <div class="head">
      <h1>Post title</h1>
      <p>Published: <small>April, 06 2017</small></p>
    </div>
    <p>...content</p>
  </div>
</div>

<!-- Better -->
<section>
  <article>
    <header>
      <h1>Post title</h1>
      <p>Published: <time datetime="2017-04-06 12:36:09">April, 06 2017 at 12:36</time></p>
    </header>
    <p>...content</p>
  </article>
</section>
```

Be sure to understand the semantics of the elements you are using. Better stay neutral than using semantics elements in the wrong way.

```html
<!-- Not so good -->
<h1>
  <figure>
    <img alt="Mercedes Benz" src="car.png">
  </figure>
</h1>

<!-- Better -->
<h1>
  <img alt="Mercedes Benz" src="car.png">
</h1>
```

### Brevity

Keep your code as simple and bref as you can.

```html
<!-- Not so good -->
<!doctype html>
<html lang="en">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Contact</title>
    <link rel="stylesheet" href="style.css" type="text/css" />
  </head>
  <body>
    <h1>Contact me</h1>
    <label>
      Phone number:
      <input type="tel" placeholder="99999999" required="required" />
    </label>
    <script src="main.js" type="text/javascript"></script>
  </body>
</html>

<!-- Better -->
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Contact</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>Contact me</h1>
    <label>
      Phone number:
      <input type="tel" placeholder="99999999" required>
    </label>
    <script src="main.js"></script>
  </body>
</html>
```

### Language

While language and character encoding is optional, we recommend you to always declare both of them at the document level. Always prefer UTF-8 over any other character encoding.

```html
<!-- Not so good -->
<!doctype html>
<html>
  <head>
    <title>Document title</title>
  </head>
</html>

<!-- Better -->
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Document title</title>
  </head>
</html>
```

### Performance

Never block the rendering of your page unless you have a very strong reason. If your stylesheet is heavy then isolate the absolutely important styles and defer the loading of the rest in a separate file. Yes two  HTTP requests is slower than one, but the perception of speed is the most important here.

```html
<!-- Not so good -->
<!doctype html>
<html lang="en">
  <head>
    <meta charset=utf-8>
    <script src=analytics.js></script>
    <title>Hello, world.</title>
    <link rel="stylesheet" href="build/main.css">
  </head>
  <body>
    <p>...</p>
  </body>
</html>


<!-- Better -->
<!doctype html>
<html lang="en">
  <head>
    <meta charset=utf-8>
    <title>Hello, world.</title>
    <link rel="stylesheet" href="build/layout.css">
    <link rel="stylesheet" href="build/ui.css">
  </head>
  <body>
    <p>...</p>
    <script src=analytics.js></script>
  </body>
</html>

```
