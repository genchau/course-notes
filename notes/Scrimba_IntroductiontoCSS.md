## Scrimba - Introduction to CSS 
##### Lessons 1-20. Date started: 05/15/2018. [Link to course](https://scrimba.com/g/gintrotocss) 
- - -
### Lesson 1.1 Welcome

What is CSS?

CSS stands for Cascading Style Sheets

It is one of the three cornerstones of the web along with HTML and JavaScript.

CSS is the presentation layer of web pages.

HTML = content (bone structure, or skeleton)
CSS = styling (or clothing)
JS = functions (nervous system)

What we'll learn:
- Creating Style Sheets
- The Cascade, Inheritance, Specificity
- CSS Selectors, Properties, Values
- Classes & IDs
- Length Units
- Width & Height
- The Box Model
- Colors
- Visibility
- Margins
- Padding
- Borders
- The Box Model Fix
- Fonts & Typography
- Element Flow, Floats, Position
- and more...

Eric Tirado, Brand Designer & Front End Dev based in the US, @iamtirado on twitter/instagram/medium/scrimba,etc.
- - -
### Lesson 1.2 CSS Documents & The Cascade

Scrimba is an interactive platform.

Applying Styles:
- Inline Styles (in the element)
- Internal Styles (style tag in the head section)
- External Styles (main.css file)

index.html:
```
<head>
  <link rel="stylesheet" href="style.css"> 
</head>
```

style.css:
```
html, body {
    margin: 0;
    padding: 0;
}
body {
    background-color: #bbb;
    color: black;
}
body {
    background-color: black;
    color: white;
}
section {
    padding: 0 25px;
}
```

Pay attention to where you place your styles, as the name implies "cascading" the styles toward the bottom will have precedent as they will be last to be executed in the chain.
- - -
### Lesson 1.3 CSS Selectors, Properties & Values

font-size can take values in px, %, or even small, large.

`section b {}` this will select b tags both children and grandchildren.
`section > b {}` this will only select direct children, no grandchildren.

Use comma to add multiple selectors to a style:
```
section > b, 
div > b {
    color: blueviolet;
}
```
- - -
### Lesson 1.4 Classes & IDs

classes can be applied to multiple elements.
IDs should only be used once.

When should we use classes?
- When you want to apply the same style to multiple elements.
- But not all elements of the same name.
- A class can be used on multiple elements, and an element can have multiple classes.

When should we use IDs?
- When you don't need to apply the same style to multiple elements.
- To have a unique selector to a common element.
- A ID cannot be used on multiple elements, and an element cannot have multiple IDs.

index.css:
```
.box {
    border: 2px solid;
    background-color: white;
}
#classes {
    color: slateblue;
}
#ids {
    color: tomato;
}
#classes > P > b, #ids li > b {
    color: goldenrod;
}
```
- - -
### Lesson 1.5 Specificity

Class will always beat element selectors.
IDs will beat classes.

Specificity refers to having multiple identifiers in the style sheet.
For example:
`html .class` will beat `.class`. 
- - -
### Lesson 1.6 Widths & Heights

naturally inline elements: 
- span
- a
- b
- em

naturally blocky elements:
- div
- nav
- aside
- main

Once we change inline items to `display: inline-block` then we can add a width and height property.
- - -
### Lesson 1.7 Length Units

length units:
- px
- em
- rem
- %

em is relative to the parent and what it inherited as the font-size.
rem is relative to the root, such as the font size set on html.

As a reminder: do not mix min and max-width when calling media queries in the same block.s
- - -
### Lesson 1.8 Colors

There's about 140 colors we can call by name. The rest we access with hex or rgb.

Example:
- #000
- #999999
- rgb(255,0,0)

#000 and rgb(0,0,0) will be black since it's turning off all 3 colors red green and blue.

rgba() can be used for opacity as well, example: rgba(255,0,0,0.5).
- - -
### Lesson 1.9 Padding

`box-sizing: border-box` this changes what `width` means. 

With border box enabled the total width will be defined. So 100px width, with 10px padding means the content is 90px.

With border box off the width will define the content size. So 100px content, 10px padding, 110px total across.

padding can be used in 3 ways, just by the numbers of parameters:
- padding: 10px will put 10px on all 4 sides
- padding: 10px 20px will put 10px top/bottom and 20px left/right.
- padding: 10px 20px 30px 40px will work starting from top moving clockwise. 10px top 20px right 30px bottom 40px left.
- - -
### Lesson 1.10 Borders

Similar to padding but it gives border to padding and content.

Usage is:
border: solid 10px red;
- - -
### Lesson 1.11 Margins

Margins more of the same, just like padding. It just goes around the border.
- - -
### Lesson 1.12 The Box Model

I don't know.
- - -
### Lesson 1.13 Visibility

A couple of ways to hid something:
- display: none
- visibility: hidden
- opacity: 0
- - -
### Lesson 1.14 Fonts

```
@import url('https://fonts.googleapis.com/css?family=Black+Han+Sans');
.font {
    font-family: 'Black Han Sans', arial, sans-serif;
    font-size: 30px;
    font-weight: bold;
    font-style: italic;
    font: italic bold 40px 'Black Han Sans', arial, sans-serif;
}
```
- - -
### Lesson 1.15 Element Flow

Inline elements such as `<a>` will flow and wrap. Block elements will take up 100% of the width, and line up vertically with other block elements.
- - -
### Lesson 1.16 Float & Clear

This is how to control flow of block elements using float and clear:
```
.box {
    height: 200px;
    width: 200px;
    /* float: left; */
}
.tomato {
    float: right;
    height: 80px;
    width: 80%
}
.purple {
    float: left;
    width: 20%;
    height: 600px
}
.gold {
    clear: right;
    float: right;
    height: 440px;
    width: 80%
}
.green {
    float: right;
    height: 80px;
    clear: right;
    width: 80%
}
.clearfix {
    clear: both;
}
```
- - -
### Lesson 1.17 Float Layout Challenge

done
- - -
### Lesson 1.18 Position Property

```
body {
    padding-bottom: 100px;
}

.first {
    position: relative;
    top: -40px;
    margin-bottom: -40px;
}
.second {
    position: relative;
}
.ribbon {
    position: absolute;
    top: 0;
    right: 20px;
}
.toplink {
    position: fixed;
    bottom: 20px;
    right: 20px;
}
footer {
    position: fixed;
    bottom: 0;
}

/*  Extra info on position property
    https://www.w3schools.com/cssref/pr_class_position.asp
    */
    
```
- - -
### Lesson 1.19 Pseudo Classes / Elements

- `ul li:first-child a {}`
- `ul li:last-child a {}`
- `ul li:nth-child(5) a {}`
- `ul li:nth-child(odd) a {}`
- `ul li a:active {}`
- `ul li a:visited {}`
- `ul li a:hover {}`

We can add content using this:
```
ul a:hover::before {
    content: "⇨  "
}
```
- - -
### Lesson 1.20 What's Next

- - -
Return to [Table of Contents](TableOfContents.md)