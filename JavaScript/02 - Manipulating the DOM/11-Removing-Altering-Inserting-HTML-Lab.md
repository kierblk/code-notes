# [Removing, Altering, and Inserting HTML Lab](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/removing-altering-and-inserting-html-lab)

## Introduction

In this lab, you will be inserting, altering, and removing DOM nodes. You will be doing the following:

1. Ask the DOM to find an HTML element or elements in the rendered page
2. Remove or insert the selected element(s) and / or
3. Adjust a property of the selected element(s)

## 1. Create DOM elements programmatically

### `document.createElement()`

Creating an element in JavaScript is an easy process. Simply call
`document.createElement('tagName')`, where `tagName` is the name of any valid HTML
tag (e.g., `'p'`, `'div'`, `'span'`, etc.).

Open `index.html` file in your browser and open up the browser's console. In the
console, enter

``` javascript
let element = document.createElement('div')
```

The element doesn't show up on the page. Why not?

## 2. Add elements in the DOM

To get an element to appear in the DOM, we have to `append` it to an existing
DOM node. To go back to our tree metaphor, we have to glue our new leaf onto a
branch that's already there. We can start as high up on the tree as
`document.body`, or we can find a more specific element using any of the
methods we've learned for traversing the DOM.

### `appendChild()`

Let's append `element` to `body` to start:

``` javascript
document.body.appendChild(element)
```

We can continue to update `element`, since we have a reference to it:

``` javascript
let ul = document.createElement('ul')

for (let i = 0; i < 3; i++) {
  let li = document.createElement('li')
  li.innerHTML = (i + 1).toString()
  ul.appendChild(li)
}

element.appendChild(ul)
```

## 3. Update elements using innerHTML

Creating elements and then appending them into the DOM is a multi-step process. It's also the safest and most reliable. Most repeated code can be removed by using functions and loops. It's The Right Way.

That said, there's another route which is commonly used, `Element.innerHTML`. If you can get a node with
`getElementById` or `querySelector` or any of the modes you've learned, you can imagine that you've gotten that node's opening and closing HTML tag. You can update that node's `innerHTML` property with a string of HTML and it will be _just as if_ you changed the HTML source for that node.

```js
let element = document.querySelector("p#greeting");
element.innerHTML = 'Hello, DOM!'
```

If there is a `<p>`aragraph with `id` of `greeting`, our code will grab that and assign it to `element.` What would you write in HTML to put `'Hello, DOM!'` between those `<p>` tags? Why you'd put the plain text `'Hello, DOM!`?

For a slightly more complicated example:

```js
let header = document.getElementById("div#header");
header.innerHTML = "<h1>Poodles!</h1><h3>An Essay into the Pom-Pom as Aesthetic Reconfiguration of the Other from a post-Frankfurt School Appropriationist Perspective</h3><p><em>By: Byron Q. Poodle, Esq., BA.</em></p>";
```

This creates, with JavaScript, in the DOM, the quivalent of:

```html
<div id="header">
  <h1>Poodles!</h1>
  <h3>An Essay into the Pom-Pom as Aesthetic Reconfiguration of the Other from a post-Frankfurt School Appropriationist Perspective</h3>
  <p><em>By: Byron Q. Poodle, Esq., BA.</em></p>
</div>
```

There are dangers with using `innerHTML`, however. If you put user-derived data into the DOM using `innerHTML`, someone could do something nasty. Consider the following code:

```js
content = someTextArea.value
node.innerHTML = `Hi, ${content}!`
```

We might have intended for `someTextArea` to contain something like a person's name that we're going to echo back out to the screen.

But what if the person typing in `someTextArea` is a nasty person and submits:

```js
<a href='#' onclick='doSomethingNastyLikeStealCookies'>Click here to claim your prize!</a>
```

While you're not familiar with events (yet!), it should be clear that `doSomethingNasty` when clicking on a link that promises a prize is probably not what users expected. While it **can** be guarded against, `innerHTML` can accidentally lead to problems in sites. Be careful with it!

## 4. Change properties on DOM nodes

We can change properties on DOM nodes to change their appearance.

``` javascript
element.style.backgroundColor = '#27647B';
```

You've changed what's on the screen!

Feel free to set as many properties as you'd like — this is a good chance to
look around and explore different properties of DOM elements.

Let's adjust the display:

``` javascript
element.style.textAlign = 'center';
ul.style.textAlign = 'left'
```

That's better.

Perhaps the most common way to change how things appear in the DOM is by
changing an element's `class` attribute. As you know from CSS, we often change
the way a bit of rendered HTML appears by changing its `class` attribute:
adding a name or removing a name.

Adding the `.alert` class to a paragraph might make the text turn red, and big
(using the `color` and `font-size` CSS attributes), provided we have created
that CSS rule in the CSS file for our page.

It's very common, therefore, to grab an element with JavaScript and update its
`className` property &mdash; which is the same as setting the `class` property
in the HTML. The `className` property expects a `String` where each class name
is separated by a space:

```javascript
element.className = "dog"
element.className = "pet-listing dog"
```

Sometimes it's easier to add classes programmatically, instead of creating a
long `String` first. JavaScript makes this friendly by having elements provide
a `classList` [property][cl] which has `.add()` and `.remove()` methods.

So, provided the CSS rules for `.this-is-fine` and `.the-room-is-on-fire`
exist, you could change the display of `element` like so:

```javascript
element.classList.remove("this-is-fine");
element.classList.add("the-room-is-on-fire");
```

Why go through the trouble of defining appearance in a stylesheet which is
applied by [`classList`][cl] versus simply using JavaScript to change the
appearance?  Again, this goes back to a fundamental programming concept about
separating concerns between technologies:

* HTML defines the structure of the website (not appearance or functionality)
* JavaScript defines functionality of the website (not structure or styling)
* CSS defines the visualization and style of the website (not structure or functionality)

## 5. Remove elements from the DOM

We know how to add things. What if we want to remove an element from a page?

#### `removeChild()`

Let's really use the power of `querySelector` and method chaining.
The `removeChild()` method requires us to find a parent and tell it to remove
its already-found child:

``` javascript
ul.removeChild(ul.querySelector('li:nth-child(2)'))
```

The second element is gone!

What if we want to remove the whole unordered list (`ul`)?

### `element.remove()`

We can just call `remove()` on the element itself:

``` javascript
ul.remove()
```

And it's gone!
