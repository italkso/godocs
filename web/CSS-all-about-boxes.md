# CSS

## 1. What is CSS?

**CSS (Cascading Style Sheets) is the code that styles web content. It's a style sheet language** which you can use to selectively style HTML elements. CSS layout is mostly based on the **box model**. 

### 1.1 Anatomy of a CSS ruleset

<img src="images/css-declaration-small.png" alt="CSS p declaration color red"  />

### 1.2  Usage of CSS

- Edit the `style.css`

  Create a new CSS file  in a text editor，and save the file as `style.css` in a directory named `styles`.

  You can also select multiple elements and apply a single ruleset to all of them.

  ```css
  p{
    color: red;
    border: 1px solid black;
  }
  
  p, li, h1 {
    color: orange;
  }
  ```

- Add the following code in your `index.html` file. 

  ```css
  <head>
  	<link href="styles/style.css" rel="stylesheet">
  </head>
  ```

- Save this `index.html` file and load it in a browser.

### 1.3 Selector

| Selector name                             | What does it select                                          | Example                                                      |
| ----------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Element selector (a tag or type selector) | All HTML elements of the specified type.                     | p <br />selects `<p>`                                        |
| ID selector                               | The element on the page with the specified ID. On a given HTML page, each id value should be unique. | `#my-id`    <br />selects `<p id="my-id">` or `<a id="my-id">` |
| Class selector                            | The element(s) on the page with the specified class. Multiple instances of the same class can appear on a page. | `.my-class`  <br />selects `<p class="my-class">` and `<a class="my-class">` |
| Attribute selector                        | The element(s) on the page with the specified attribute.     | `img[src]`<br /> selects `<img src="myimage.png">` but not `<img>` |
| Pseudo-class selector                     | The specified element(s), but only when in the specified state. (For example, when a cursor hovers over a link.) | `a:hover`     <br />selects `<a>`, but only when the mouse pointer is hovering over the link. |

See the MDN [Selectors guide](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors).

### 1.4 Fonts and text

```html
<link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet">
```

### CSS: all about boxes

CSS layout is mostly based on the **box model**. 

![three boxes sat inside one another. From outside to in they are labelled margin, border and padding](images/box-model.png)

Each box taking up space on your page has properties like:

- `padding`, the space around the content(eg.the space around the paragraph text).

- `border`, the solid line that is just outside the padding.

- `margin`, the space around the outside of the border.

- `width` (of an element).

- `background-color`, the color behind an element's content and padding.

- `color`, the color of an element's content (usually text).

- `text-shadow` sets a drop shadow on the text inside an element.

- `display` sets the display mode of an element. (keep reading to learn more)





***Reference***

[1]:https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics
[ 2 ]:https://caniuse.com

