# HTML

HTML is the standard markup language for creating Web pages.

- HTML stands for Hyper Text Markup Language
- HTML describes the structure of Web pages using markup
- HTML elements are the building blocks of HTML pages
- HTML elements are represented by tags
- HTML tags label pieces of content such as "heading", "paragraph", "table", and so on
- Browsers do not display the HTML tags, but use them to render the content of the page

## HTML Documents Boilerplate

```html
<!DOCTYPE html>
<html>
  <head>
    <! -- Our metadata goes here -->
    <title></title>
  </head>
  <body>
    <!-- Our content goes here -->
  </body>
</html>
```

* All HTML documents must start with a document type declaration: `<!DOCTYPE html>`.
* The HTML document itself begins with `<html>` and ends with `</html>` (root of an HTML document).
* One`<head>` element, followed by one `<body>` element.
* The visible part of the HTML document is between `<body>` and `</body>`.

### The <!DOCTYPE> Declaration

The `<!DOCTYPE>` declaration represents the document type, and helps browsers to display web pages correctly.

It must only appear once, at the top of the page (before any HTML tags).

The `<!DOCTYPE>` declaration is not case sensitive.

The `<!DOCTYPE>` declaration for HTML5 is:

```html
<!DOCTYPE html>
```

#### HTML `<head>`

- Not shown on page, only `metadata`
- 

##HTML Elements

https://developer.mozilla.org/en-US/docs/Web/HTML/Element

###HTML Tags

HTML tags are element names surrounded by angle brackets:

```html
<tagname>content goes here...</tagname>
```

- HTML tags normally come **in pairs** like `<p>` and `</p>`
- The first tag in a pair is the **start tag,** the second tag is the **end tag**
- The end tag is written like the start tag, but with a **forward slash** inserted before the tag name

*The start tag is also called the **opening tag**, and the end tag the **closing tag**.*

* 

#### HTML Headings

HTML headings are defined with the `<h1>` to `<h6>` tags.

`<h1>` defines the most important heading. `<h6>` defines the least important heading.

#### HTML Lists

#### Generic Container

#####HTML Divs

The **HTML Content Division element** (**<div>**) is the generic container (group things together) for flow content. It has no effect on the content or layout until styled using CSS.

#####HTML Spans

The **HTML Keyboard Input element** (**<kbd>**) represents a span of **inline** text denoting textual user input from a keyboard, voice input, or any other text entry device.

#### HTML Forms



###HTML Attributes

Elements in HTML have **attributes**; these are additional values that configure the elements or adjust their behavior in various ways.

https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes

#### src

```html
<img src="url">
```

#### href

```html
<a href="url">Link Text</a>
```



