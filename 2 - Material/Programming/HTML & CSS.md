 w2024-10-02 21:01

Status: #devoleped 

Tags: [[Web Programming]] 

---
# Roots of HTML file

### 1. **Tag HTML**
The `<html>` tag is the root element of an HTML document. It encapsulates all other HTML elements, and it defines the beginning and end of the document.

Example:
```html
<html>
  <!-- All other HTML code goes here -->
</html>
```

### 2. **Tag Head vs Tag Body**

**`<head>` tag**: The `<head>` section contains metadata and links to external resources, like stylesheets, scripts, and information about the document (such as its title and encoding). It does not display anything directly on the page.
  
  Example:
  ```html
  <head>
    <title>My Page</title>
    <meta charset="UTF-8">
    <!-- Here you are going to add a style file into html file -->
    <link rel="stylesheet" href="style.css">
  </head>
  ```

**`<body>` tag**: The `<body>` section contains all the content that will be displayed to the user in the browser, such as text, images, videos, forms, and any interactive elements.
  
  Example:
  ```html
  <body>
    <h1>Welcome to My Page</h1>
    <p>This is the content displayed in the browser.</p>
  </body>
  ```

### 3. **Tags do Head**

Let's dive into the key elements inside the `<head>` tag:
**`<title>`**: Specifies the title of the HTML document, which is displayed on the browser tab. It is important for SEO and user experience.
  
  Example:
```html
  <title>My Website Title</title>
```

Contains internal CSS (Cascading Style Sheets) to apply styles directly to the webpage. This is an alternative to linking an external stylesheet.

Example:
``` html
<style>
  body { font-family: Arial; background-color: lightgrey; }
</style>
```

Embeds or links to JavaScript, which controls the behavior of the webpage. It can be placed in the `<head>` or `<body>` section, depending on when the script should run.

Example:
```html 
<script>
  alert('Hello, world!');
</script>
```

# How format properly  a HTML document

To avoid problems in future we need to organize our HTML code in the way that in future, we are not going to find any difficulties. For doing that , here some tips that we should follow every time we create a new code.

### 1. Put the best title for make your page meaningful
The `<title>` tag should be easy and friendly to understand, because all the text inside the tags will appears in the Google's search engine and also the user find easier to click on your website after wrote the key words.

```html
<title>Six Revisions - Web Development and Design Information</title>
```

This title is longer to find in the search bar of browser, but it have all the main purpose for understand what is the content inside the website, later we are going to see how to put specifics tags for find easier your website.

# CSS 

## 1. How to implement the style?

### Inline CSS:
Is written directly within an HTML tag, using the style attribute to apply styles to individual elements.

Advantages:
  - Quick and easy for styling a specific element.
  - Does not require a separate CSS file or block.
  - Ideal for testing or small projects where only a few elements need styling.

Disadvantages:
  - Poor maintainability: Hard to manage when dealing with many elements.
  - Duplication of code: Styles are repeated across multiple elements.
  - Violates separation of concerns (mixing content and styling).
  - Cannot take advantage of browser caching like external stylesheets.

### Internal CSS:
Is placed within the `<style>` tag inside the `<head>` section of the HTML document, allowing you to define styles for the entire page.

Advantages:
  - Keeps all styles for the page in one place, making it more organized than inline CSS.
  - Easier to apply the same style to multiple elements within a single HTML file.
  - Suitable for small websites or single-page applications where external CSS may be overkill.

Disadvantages:
  - Not ideal for larger projects or websites with multiple pages, as styles cannot be shared between files.
  - Increases the size of the HTML document.
  - Styles only apply to a single page, requiring duplication for other pages.

### External CSS:
Is written in separate `.css` files and linked to HTML documents using the `<link>` tag in the `<head>` section.

Advantages:
  - Reusability: A single CSS file can be used across multiple HTML pages, reducing duplication.
  - Maintainability: Styles are centralized, making it easier to update and manage.
  - Performance: CSS files can be cached by browsers, reducing load time for subsequent page loads.
  - Separation of concerns: HTML handles structure/content, while CSS manages design and layout, enhancing code clarity.

Disadvantages:
  - Requires additional HTTP requests to load external files, which can increase initial load times (mitigated by caching).
  - Not ideal for small websites or single-page projects due to the overhead of maintaining multiple files.
## 2. Margin vs padding

**Margin** and **padding** are two CSS properties used to create space around elements, but they serve different purposes and behave differently:

| _**Margin**_                                                                                       | _**Padding**_                                                       |
| -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| Space outside the element’s border                                                                 | Space inside the element’s border                                   |
| Creates space between the element and <br>other elements                                           | Creates space between the element’s content and its border          |
| Does not affect the element’s background <br>color or image                                        | Expands the area covered by the element’s background color or image |
| Margins can collapse, meaning adjacent <br>margins may overlap or <br>combine into a single margin | Padding does not collapse; it always maintains its specified size   |
| margin: 10px; adds space outside the element                                                       | padding: 10px; adds space inside, expanding the area for content    |
### Visual example 

![[MarginVsPadding.png | center]]
### Aspects between margin padding
### Margin

- Like creating space between boxes on a page; it pushes elements away from each other.
- is used when you want to control the space between different HTML elements.

### Padding

- Like creating space inside the box; it increases the distance between the content and the edges of the box itself.
- is used when you want to control the spacing within an element, affecting how close the content is to the edges.


![[MarginStats.jpg|center]]


## 3. Elements properties in CSS
--- start-multi-column: ID_xkfm
```column-settings
Number of Columns: 2
Largest Column: standard
```
### Width
Specifies the horizontal size of an element.
```css
  width: 300px; /* Sets the width to 300 pixels */
  width: 50%; /* Sets the width to 50% of the parent container */
```
--- column-break ---

## Height
Specifies the vertical size of an element.
```css
height: 200px; /* Sets the height to 200 pixels */
height: auto; /* Height is automatically adjusted to fit the content */
```


--- end-multi-column
## Float
Positions elements to the left or right of their container, allowing text and other elements to wrap around them.

• float: left; Aligns the element to the left.

• float: right; Aligns the element to the right.

• float: none; The element does not float (default behavior)

## 4. Hierarchy of styles in CSS
### 4.1 Source Order (Cascade)
- **Definition**: When multiple CSS rules have the same specificity, the one that appears **later in the code** wins.

- CSS is called a “Cascading Style Sheet” because of this behavior — styles cascade down and the last rule overrides the previous ones.

```html
<style>
  p {
    color: blue; /* This rule is overridden */
  }
  p {
    color: red; /* This rule wins because it comes later */
  }
</style>
```

### 4.2 Specificity
• **Specificity** is a weight calculation that determines which CSS rule takes precedence over others. It is based on the types of selectors used in the CSS rules.

• Specificity is calculated using a system of scores, with more specific selectors having a higher score. Here’s a general breakdown:

• **Inline styles**: 1000 points (most specific)

• **ID selectors** (#id): 100 points

• **Class, pseudo-class, attribute selectors** (.class, :hover, [type="text"]): 10 points

• **Element and pseudo-element selectors** (div, h1, ::before): 1 point

```css
#header { color: blue; }        /* Specificity score: 100 */
.header { color: green; }      /* Specificity score: 10 */
h1 { color: red; }             /* Specificity score: 1 */
```

### 4.3 !Important rule
• The _!important rule_ overrides all other CSS declarations, regardless of specificity or order.

• It forces the style to be applied to the element, even if there are more specific selectors later in the code.
```css
p {
  color: blue !important; /* Highest priority */
}
p {
  color: red;
}
```

### Animation in CSS without using JS
For adding an animation on CSS without using JS you are going to use the `@keyframe` keyword, in this case we are going to add an example of changing color form red to yellow inside a `<div>`:

```css

@keyframe example {
	from{background-color: red;}
	to{background-color: yellow;}
}

div {
	width: 100px;
	height: 200px;
	background-color: red;
	animation-name: example;
	animation-duration: 6s;
}
```

In this case you are going to start with the color red then with the keyframe we define before, we are going to add the animation  trought the `animation-name: "name of animation"`, in this case we gave as an example like the name of animation.
With `animation-duration: seconds` we are saying how much time we should make the animation working on it .

# References
---
 - How properly format  your html document:
   https://www.webfx.com/blog/web-design/20-html-best-practices-you-should-follow/ 