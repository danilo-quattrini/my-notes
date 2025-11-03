 2024-10-02 21:01

Status: #devoleped 

Tags: [[Web Programming]] [[Full Stack]] [[Front-end]]

---
# Roots of HTML file

We start our journey with the first and foremost thing to add into our HTML file is the: 

```html
<!DOCTYPE html>
```

Where we say to the browser that we are open an HTML with a specific vesion.
# 0. Attribute and element in HTML
The attribute inside the HTML tag is useful when we want to set a behavior to our tag, the sintax is the following one:
```html
<element attribute="value"></element>
```

# 0.1 hyperlink 
This attribute `href` is useful when we want to include a link of a URL inside the element of our html tag:
```html
<a href="https://www.example-website.com">Visit our website</a>
```
without this one, we cannot link the text to its link, in this case we use the tag `<a>` when we want to use a text a link connector

we can use the attribute `target` we use it to identify where we want to open the link, into a new tab or in the same tab?

List of attributes of `target` and their behaviors:
- `_self`: The current browsing context. (Default)
- `_blank`: Usually a new tab, but users can configure browsers to open a new window/tab instead.
- `_parent`: The parent browsing context of the current one. If no parent, behaves as `_self`.
- `_top`: The topmost browsing context. To be specific, this means the "highest" context that's an ancestor of the current one. If no ancestors, behaves as `_self`.
### 0.1.1 paths for the links
The path is the location, where we find your file, image or other resources we want to use in our webpage, we have two different types of path:
- **absolute path**: the absolute path it starts from the root of the directory into the file we want to use, it's used with links that starts with, `http`, `https`  and `file` it's used to refer the location of the file inside our directory, let's see this example below:
  ```html
  <a href="```html
https://design-style-guide.freecodecamp.org/img/fcc_secondary_small.svg
```"> Fcc Logo </a>
  ```
  Here we are using the **absolute path** and we know that, because I wrote the entire location of where the file it's from the `design-style-guide.freecodecamp.org` into the file `fcc_secondary_small.svg`.
  
  In case we are workin with a file inside our local machine, that's the same but we need to refer all the paths, from the very beginning
```html
<p>
  Read more on the
  <a
    href="/Users/user/Desktop/fCC/script-code/absolute-vs-relative-paths/pages/about.html"
    >About Page</a
    >
</p>
```
Here's what the absolute URL looks like in the browser address bar:

```sh
file:///Users/user/Desktop/fCC/script-code/absolute-vs-relative-paths/pa
```

>[!warning] **WACH OUT**
>When we see the `file://` protocol, it means that we are are using a file into our system.

- **relatives paths**: the easiest way to use a file into our HTML code, we just need to write the name of the file we want to use. Here we have this HTML page, `about.html`, we want to link this page to our element, we just write the name:
  ```html
  <a href="about.html">About Us</a>
  ```

>[!question] When we use the **Absolute** and the **Relative**?
>- **Absolute:** external resources and documents that we want to keep them that work consistently.
>- **Relative**: Maintenance of the code, because it's easier to read and edit 
>- **Relative**: when we want to work locally inside our machine, without any problems with server or broken links.

### 0.1.2 path order
Let's see an example on how we can access to your elements inside these file tree:
```sh
my-app/
├─ public/
│  ├─ favicon.ico
│  ├─ index.html
├─ src/
│  ├─ index.css
│  ├─ index.js
```

- if we want to use the `favicon.ico` file and we are inside the `index.html` we can just refer to the path `./favicon.ico`.
- if we want to use the `index.css`, first of all we need to specify the root directory where it's contained the file `src` then we say with the `..` that we are moving outside of the directory we are rnw (remember that we are staying in the `index.html` file) and at the end we just refer the file we want to use.
```bash
../src/index.css
```
## 0.2 `src` and `alt` attributes
We use the `src` attribute inside and `<img />` element, because we need to specify the path or the URL, where we will pick the image/file, the `alt` attribute is not mandatory, but it's necessary if we want to create an accessible web page.
```html
<img src="dog.png" alt="This image show a dog on the sofa"/>
```

>[!info] **Note**
>The `alt` attribute is necessary to explain what are we going to show in the image, helpful for the screen reader to increase the accessibility of our website.

## 0.3 `input`  elements
The `input` element has a attribute `type`, where we specify which type of input we want to show inside our webpage. In this example below we are going to use the `checkbox` type that's a sort of todo list, like this:

Where we add an attribute that doesn't require a valute, we call it a boolean attribute, for instance, we are use the `checked` attribute where we want to
see that the checkbox is checked and when is not there it's unchecked.

```html
<input type="checkbox" checked />
```

## 1. **Tag HTML**
The `<html>` tag is the root element of an HTML document. It encapsulates all other HTML elements, and it defines the beginning and end of the document.

Example:
```html
<html lang="en">
  <!-- All other HTML code goes here -->
</html>
```

We should **specify the language of your page** wit the `lang` type.
## 2. **Tag Head vs Tag Body**

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

## 3. **Tags do Head**

Let's dive into the key elements inside the `<head>` tag:

### 3.1 `<title>` element
Specifies the title of the HTML document, which is displayed on the browser tab. It is important for SEO and user experience.
  
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

### 3.2 `link` element 
We use the `link` element when we want to link an external CSS file or an icon we want to insert in our HTML file. Here an example on how we upload an CSS file inside the HTML file, we can see this properly when we talk about [[CSS#External CSS|external css]], here we see how to do that:

```html
<link href = "./style.css" rel = "stylesheet"/>
```

The `rel` means **relations** and is necessary to specify the relationhsip that we have between the file and the HTML document, in this case the linked resource is a stylesheet.

We can use either to link external resources from other websites like [Google Fonts](https://fonts.google.com/), if we want to use some fonts from other website we do the same technique as before, just we replace the href from the path to the URL:

```html
<link rel="preconnect" href="https://fonts.googleapis.com" />
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
<link
  href="https://fonts.googleapis.com/css2?family=Playwrite+CU:wght@100..400&display=swap"
  rel="stylesheet"
/>
```

The `rel="preconnect"` is an interesting way to handle time management, in this way we say that before we import the font inside our HTML document, we **pre-load** the google font page and the browser  create an early connection to the value specified in the `href="https://fonts.googleapis.com"`, **increasing the speed up times**.

Last we can use the `<link>` element when we want to use a [favicon](https://en.wikipedia.org/wiki/Favicon), that't the icon you can see thought the tab of your webpage, you can do that in this way:
```html
<link rel = "icon" href = "favicon.ico" />
```

>[!warning] **.ico** File format
>It's better to use the **.ico** image format for the icons you are going to display inside the browser tab.
### 3.3 `meta` element
This element is necessary when we want to define the type of [[Programming Knowledge#Character Encoding|character encoding]] we want to use for our webpage:
```html
<meta charset="UTF-8" />
```

We can either use the `meta`  element to say for example, how we are going to show your webpage into a preview of any Social media like Twitter.

```html
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
```
>[!info] **WHY WE USE THIS?**
>In this way we are able to make our webpage look the same in all devices.

We can use the `meta` element for [^1]SEO or Search Engine Optimization purpose, for instance if we want to describe our webpage, and improve our web page to optimize our search ranking, and rank higher on the search engines, we can use to describe our web page, for instance:
```html
<meta
	name="description"
	content="This is an example of where we are going to describe our webpage in a few words."
/>
```
By setting the `name` attribute to `description`, it ensures that browsers, search engines, and other web tools correctly interpret this metadata. The `content` attribute is where you will place your description. 
>[!warning] **IMPORTANT**
>It is recommended that you keep your descriptions short and concise.

### 3.3.1 OG protocol with `<meta>`
The open graph protocol is useful to handle, how we are going to show our website thought the social media, this is a way to engage the user to click over your content, and interact with it.

Let's see the basics OG protocol we can use for our webpage, we should declare the `<meta>` element and inside of it, we are use the attributes `property` and `content`:
```html
<meta property="og:title" content="Obsidian.com"/>
```
In the `property`  we declare which type of `og` we want to use in this case we are declare the title, so we use the property `og:title`, and inside `content`, we write the content we want to show, in this case the title of our web page.

We should declare the basics property for our web page, at least: `og:type`, `og:url` and `og:image`, now for each of them we are going to see what they do.

```html
<meta property="og:type" content="website" />
```

The `type` property is used to represent the type of content being shared on social media. Examples of this content include articles, websites, videos, or music.
# 4.0 How format properly  a HTML document

To avoid problems in future we need to organize our HTML code in the way that in future, we are not going to find any difficulties. For doing that , here some tips that we should follow every time we create a new code.

### 4.1 Use the boilerplate (template)
The best way to start your HTML page is just follow a boilerplate, that's a template we use the first time we create our HTML file in this case the boilerplate has this format:
```html
<!DOCTYPE html>
<html>
	<head>
	    <meta charset="utf-8" />
	    <meta
	       name="viewport"
	       content="width=device-width, initial-scale=1.0" />
	    <title>freeCodeCamp</title>
	    <link rel="stylesheet" href="./styles.css" />
	</head>
	<body>
	</body>
</html>
```

>[!warning] **INDENTATION**
>It's important for the readability of the HTML code to indent each element of the file for at least **2 spaces**
### 4.2 Put the best title for make your page meaningful
The `<title>` tag should be easy and friendly to understand, because all the text inside the tags will appears in the Google's search engine and also the user find easier to click on your website after wrote the key words.

```html
<title>Six Revisions - Web Development and Design Information</title>
```

This title is longer to find in the search bar of browser, but it have all the main purpose for understand what is the content inside the website, later we are going to see how to put specifics tags for find easier your website.

### 4.3 Use the `main` element 
For the SEO (Search Engine Optimization) and Accessibility it's better to divide each content of your web page in a way that everyone can understand what it's.

We can use the `<main>` element to identify a part of the `<body>` element, that's **unique** and **should not be repeated** inside the HTML document.

### 4.4 Use the `section` element
It's good practise to use the `section` element to separate each content of the page inside the main, in this case if we want to add a new part of the page we use another `section` element.

it's used to define sections in a **document, such as chapters, headers, footers, or any other sections of the document**. It is a semantic element that helps with SEO and accessibility.

### 4.5 Use the `figure` element
The `figure` element is used as semantic tag outside images, diagrams, code snippets, etc.., in this case the difference with the `<img>` is that we can define a new element inside the `<figure>` that's `<figcaption>` where we can insert the caption under the image.
```html
<figure>
  <img
    src="/shared-assets/images/examples/elephant.jpg"
    alt="Elephant at sunset" />
  <figcaption>An elephant at sunset</figcaption>
</figure>
```

### 4.6 Use the `footer` element
The `footer` element is the last part of an HTML document, where we save the author of the page, social medias, other pages inside the website, and so on.
```html
<footer>
	<p>© 2018 Gandalf</p>
</footer>
```

A footer typically contains information about the author of the document, copyright data, links to terms of use, contact information, and more.
### 4.7 Use the `nav` element 
We use the `nav` element if we want to refer a section where we are going to use several navigation links.

This is an example of a `header` element that contains a navigation section element:

```html
<header>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</header>
```
>[!warning] **REMEMBER**
>It's important to know that these elements should not be used for presentational purposes only. If you need to display the text in italics `<i>` and has a meaning , but the text doesn't have a special purpose `<em>`, style, or meaning in the paragraph, you should use CSS instead.

### 4.8 `strong` vs `b`
The element `<b>` mean "bring to attention" and it doesn't have any **semantic meaning**, it's used to highlight keywords inside summaries or describe products.
```html
<p>
  We tested several products, including the <b>SuperSound 3000</b> for audio
  quality, the <b>QuickCharge Pro</b> for fast charging, and the
  <b>EcoClean Vacuum</b> for cleaning. The first two performed well, but the
  <b>EcoClean Vacuum</b> did not meet expectations.
</p>
```

Whereas we use the `<strong>` element if we want to give a meaning to the word we want to evidence, means that the word is crucial urgent.
```html
<p>
  <strong>Warning:</strong> This product may cause allergic reactions.
</p>
```

## 5.0 List in HTML
To create a new unordered list inside the HTML file we use the element `<ul>` and inside each element of the list is identified with the `<li>` element before:
```html
<ul>
	</li> bread </li>
	</li> apple </li>
	</li> orange </li>
</ul>
```

Instead to create a ordered list we use the element `<ol>` that means ordered list, it works as the `<ul>` but in this case we have numbers instead of dots.

### 5.1 Description Lists in HTML
In HTML we have the descriptive list element, we use when we want to show a termi with its definition, for instance if we want to give a term `HTML` and `CSS` a definition  we can do that with the `<dl>` element:
```html
<dl>
	<dt>HTML</dt>
		<dd>HyperText MarkupLanguage<dd>
	<dt>CSS</dt>
		<dd>Cascadian Style Sheet</dd>
</dl>
```

The elements of the Descriptive List are the followed one:
- `<dl>`: it's the container of the element we want to describe that contains
- `<dt>`: *description term*, it's the term we want to explain in the example above it's the acronymous of HTML and CSS.
- `<dd>`: *description details* this element it's used to describe the term we define with the `<dt>` tag element.
>[!info] **When use them?**
>**product specifications,** **frequently asked questions**, contact information, and metadata. Essentially, when you have **two related pieces of information in a key-value pair format,** where one acts as a label, the key, and the other acts as additional related information, the value, you can use a description list.
## 6.0 `<div>` elements
The `div` element is also called *Content Divisor Element*, is where we can place everything we want, we can style with everything we want, we can. give a `height` a `width` or a background with [[CSS]] and so on.

We can use it either, if we don't want to do anything with the element it self, for instance, let's see this example:
```html
<div>
	<h1>I'm a header</h1>
	<p>I'm a paragraph</p>
</div>
```

But wait!!! It is not the same thing as the `<section>` element we have seen [[#4.4 Use the `section` element|before]]? 

YES, but in this case the `<section>` element is better for it's semantic, what does it mean semantic? 

Semantic it's the meaning of the words or the phrases in a language. The semantic in HTML is necessary if we want to create an accessible web-page, because each element inside HTML have it's own meaning, pc, phones and tablet are going to understand that the element `<section>` it's a page section, where we are display some stuff.

We will dive into this topic further later on. For now, just know that the `div`, does not have this. It's like a mysterious ghost. Let's see what else we can do to a `div`, in the next lecture.

## 7.0 `id` and `class` attributes
In this section we are going to discuss about the differences between the `id` attribute and the `class` one.

--- start-multi-column: ID_w3fp
```column-settings
Number of Columns: 2
Largest Column: standard
```
### `class`
---
- You **can use it different elements** inside the HTML file.
- You can use the spaces when we call a class attribute.
  ✅`<h1 class="text color">  <h1/>`
- **Declaration with the dot** inside the [[CSS]] file.
```css
.button{
	border-color: black;
}
```
- We can give more class values inside the element
```html
<h1 class="button border-animation padding-style">hello</h1>
```
--- column-break ---

### `id`
---
- You **can use it in only one element**.
- You **can't use any space**.
  ❌`<h1 id="text color"> </h1>`
- Declaration with the # inside the [[CSS]] file.
```css
#title{
	color: red
}
```
- We **cannot give more than one value** of the id attribute

--- end-multi-column
So at the end we use the `id` attribute inside the **element we want to be the only one who is gonna be change** inside the HTML document, whereas the `class` attribute is helpful if **we want to give the style or something else to more elements** inside the HTML code

## 8.0 Entities in HTML
The entities in HTML are special character that we want to show inside a HTML, element, for instance let's see an example below:
```html
<p>This is an <img /> element</p>
```
When we are going to see into te browser, the `</img>` element would be ignore, that's because the browser parse that string as an HTML element and not as a string to show inside the `<p>` element. 

We solve this problem with the entity `&lt;` that means `less than` and with the `&gt;` means greater than, as we can see here:
```html
<p>This is an &lt; img /&gt; element</p>
```
Now we can see the element `<img />` as we wanted before.

We have either other ways to declare the entity, we can use the decimal notation:
```html
&#60;
```
this is the decimal reference for the character `<` and we have the hex value to, with the `#x` and more ASCII hex digits and ends with a semicolon.
```html
&#x3C;
```
## 9.0  `<script>` element
The `<script>` element is useful, if we want to embed a JavaScript code inside our HTML file, we use [[JavaScript]], as a way to interact dynamically with our web page, we can create real-time checks, into the users' form, also we can use it to create new animation inside our webpage, Here is an example of using the `script` element in an HTML document:
 ```html
 <body>
	 <script>
		  alert("Hello, World!")
	 </script>
 </body>
 ```
The best way to include a JavaScript code inside our HTML file,  is to use an external file, where we can use it whenever we want and in every HTML we want to implement that JS code, for instance:
```html
<script src="error-alert.js"></script>
```
Now we are able to use this JS code in different HTML pages, and without copy and paste the same code in each HTML file.

## 10.0 Audio/Video elements in HTML
We can use the element `<audio>` if we want to include an audio element inside the HTML page, the format of the audio should be: MP3, WAV and OGG, instead if we want to include video we use the `<video>` element with a specific type of video format such as: MP4, MOV WEBM and so on.

Here an an example of where we can use is:
```html
<audio src="AudioSource.mp3"></audio>
```
When we run our HTML, at the first glance, we don't see the audio inside your webpage, but if we use the analyzer, we are able to see the element that's inside the page, if we want to play the audio element we need some `controls` and that's the `control` attribute that comes up to us:
```html
<audio src="AudioSource.mp3" controls></audio>
```
NOW WE CAN PLAY THE AUDIO, but we have other attribute we can use inside the audio element:
- `loop`: we are going to play the audio in loop.
- `muted`: we are going to mute the audio.

Unfortunately not all the browsers support all the audio format that we have said before, to handle this problem, we can use the `source` element tag that we add inside the `audio` element:
```html
<audio controls>
	<source src="audio.wav" type="audio/wav" />
	<source src="audio.ogg" type="audio/ogg" />
	<source src="audio.mp3" type="audio/mp3" />
</audio>
```

With the `video` element is the same, we can use the same attributes `muted`, `controls`, `loop`, but we can declare an additional attribute that's the `poster` where we can assign an image that will be shown wile the video is still downloading.
```html
<video
src="https://archive.org/download/BigBuckBunny_124/Content/big_buck_bunny_720p_surround.mp4"
loop
controls
muted
poster="https://peach.blender.org/wp-content/uploads/title_anouncement.jpg?x11217"
width="620"
>

<video/>
```

## 11.0 Image format and type
We don't use anymore the image format as JPG or PNG, but now we are working with more optimized formats like, WEBP or AVIF. We can use some compress algorithms to reduce the size of a JPG or PNG image, but with the JPG one is useless, because we are going to downgrade the quality of the image, so the best choice is the WEBP and the AVIF forma

Raster images are all the formats like PNG or JPEG, JPG that means we are working with images that have pixels, so if we are going to resize the image, it'll be blurry, the best choice for us is the SVG 

### 11.1 SVG types
SVG stands for Scalable Vector Graphic, that means we are working with images that can be scaled without lose the quality of them, instead of the raster images like, JPEG or PNG, we are able to incorporate them as HTML inside the website.

SVGs specifically have the added benefit of storing data in XML. This means you can use them directly in your code as raw HTML with the `svg` element. It also means you can programmatically change the color of the image..
```html
<svg width="100" height="100" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
  <circle cx="50" cy="50" r="45" stroke="black" stroke-width="4" fill="yellow" />
  <circle cx="35" cy="40" r="5" fill="black" />
  <circle cx="65" cy="40" r="5" fill="black" />
  <path d="M35 65 Q50 80 65 65" stroke="black" stroke-width="4" fill="transparent" />
</svg>
```
This SVG code is for drawing a smile face.
- The `svg` element means that we are working with the svg image, and it's the space where we work on it, like square, circle, rectangles and so on.
- `circle` element is the circle we are going to use to show the face, with they attributes position `cx-cy` radius `r` and the `stroke` with the `fill` we fill the color of the circle, same as the other elemnts down
- The `path` element is used to draw the smile. It creates a curved line for the mouth.
- Each SVG element has attributes that control its appearance and position within the drawing area.
## 12.0 Replaced elements
Replaced elements are all elements where we are able to change the content of the embedded element without using CSS, for instance if we use the `img` element:
```html
<img src="file.jpg" alt="hello"/>
```
we can edit this image only change its width, height or the position inside the web-page, but if we want to change the image itself we use the `iframe` element.
```html
<iframe src="https://www.example.com" title="some-title"></iframe>
```
>[!info] **Where we use it?**
>Common examples for using the `iframe` element would be to embed Maps or YouTube videos onto the page

There are some other replaced elements, such as `video`, and `embed`. And some elements behave as replaced elements under specific circumstances. Here's an example of an `input` element with the `type` attribute set to `image`:

Example Code

```html
<input type="image" alt="Descriptive text goes here" src="example-img-url">
```

This type of `input` is considered to be a replaced element, but other ==`input` types like `text`, or `email` are not replaced elements.==

### 12.1 `iframe` element
`iframe` is the acronymous of inline frame, and it's used to add elements inside the HTML document that we want to include, such as video, maps or other webpages.

The sintax of the `iframe`
```html
<iframe
	src="video-url"
	heigth="300"
	widht="200"
	allowfullscreen
>
</iframe>
```

We already know the others attribute what they do, but the attribute `allowfullscreen`, it helps to show the video in full-screen.

>[!warning] **Good Practice**
>It's a good practice to add the `title` attribute inside the `iframe` elements that's important for accessibility.

We can embed everything inside the `iframe` element, either a map from openstreet, like this example:
```html
<iframe
  width="425"
  height="350"
  src="https://www.openstreetmap.org/export/embed.html?bbox=3.006134033203125%2C6.150112578753815%2C3.6357879638671875%2C6.749850810550778&amp;layer=mapnik"
  style="border: 1px solid black"
>
</iframe>
```
We just add a border with the attribute `style` nothing else it's important, and we can either embed HTML pages, the only thing we need to do it's to use the `srdoc` instead of `src`.

# References
---
 - How properly format  your html document:
   https://www.webfx.com/blog/web-design/20-html-best-practices-you-should-follow/ 
 - Free images website
   [PixaBay](https://pixabay.com/) or [Unsplash](https://unsplash.com/)

[^1]: https://en.wikipedia.org/wiki/Search_engine_optimization
