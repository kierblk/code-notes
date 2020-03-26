# [The DOM Tree](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/the-dom-tree)

## Resources

* [MDN - Document Object Model](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model)

## Learning Goals

### 1. Describe how the DOM works as a tree

  Every tree can contain subtrees, which we can treat independently of their
  parent trees. They repeat the pattern and appearance of the full tree, despite 
  being a smaller part of a tree, like branches.

  Practically speaking, the DOM begins at `<html>`, but for now we should avoid
  changing what's between the `<head></head>` tags. Most of the time, we will look
  at the DOM subtree with its root at `<body>` and only change things that will be
  visible on the page.

### 2. Define the computer science version of "Tree"

  What do we mean when we say that the DOM is a tree? 

  Trees make a good metaphor for the DOM because almost everyone has seen a tree.

  Starting at the bottom, you can climb up the tree and out to the farthest — and smallest — branches. The thicker a branch is, the stronger its connections are: the more it holds within it. Likewise, the thinner a branch is, the less it holds inside.

  The DOM works basically the same way, except we usually talk about the root as
  being at the top of the DOM and the leaves being the most deeply nested HTML
  elements. So basically, we can imagine a tree upside down.

  ![DOM Tree Graphic](https://curriculum-content.s3.amazonaws.com/fewpjs/fewpjs-the-dom-tree/Image_6_DomTree.png)

### 3. Ask the DOM to find or "select" an HTML element or elements in the rendered page

  JS exposes a few ways of finding DOM nodes, either directy or in stages, courtsey of the `document` object.

#### `document.getElementById()`

  This method provides the quickest access to a node, but it requires that we know a very specific piece of information - its `id`.

  This method can return only **one** element since CSS `id`s are expected to be unique.

  Given the following DOM tree:

  ```HTML
<div>
  <h5 id="greeting">Hello World!</h5>
</div>
  ```

  We could find the `h5` element with `document.getElementBy Id('greeting')`.

#### `document.getElementByClassName()`

This one is also very commonly used in DOM programming.

This method finds elements by their `ClassName`. Unlike the previous method, class names do not need to be unique, so this method returns an `HTMLCollection` of all the elements with the given class.

You can iterate over an `HTMLCollection` with a simple `for` loop.

Given the following `DOM` tree:

```HTML
<!-- the `className` attribute is called `class` in HTML  -->
<div>
  <div class="banner">
    <h1>Hello!</h1>
  </div>
  
  <div class="banner">
    <h1>Sup?</h1>
  </div>
  
  <div class="banner">
    <h5>Tinier heading</h5>
  </div>
</div>
```

We could find all the elements with the class name "banner" by calling `document.getElementsByClassName('banne')`.

#### `document.getElementsByTagName()`

If you don't know an elements `id` or `class` but you _do_ know its tag name, this would be the method you would choose.

Since tag names aren't unique, this method also returns an `HTMLCollection` also.

#### Finding a Node Without Knowing Anything About It

What if we know next to nothing about an element? Or what if we're just interested in finding out more about the child nodes of a given element? This is where our knowledge of trees comes in handy!

Given the following DOM tree:

```HTML
<main>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
  <div>
    <div>
      <p>Hello!</p>
    </div>
  </div>
</main>
```

How would we go about changing only the second "Hello!" to "Goodbye!"?

Here we're going to use a mix of different methods to accomplish the goal.

Let's start by getting the <main> element

```JavaScript
const main = document.getElementsByTagName('main')[0]
```

Then we can get the children of `main` using `main.children`, so we can get the
second child with `main.children[1]`.

```javascript
const div = main.children[1]
```

Finally, we can get and update our `<p>` element with

```javascript
// we can call getElementsByTagName() on an _element_
// to constrain the search to its children!
const p = div.getElementsByTagName('p')[0]
```

And lastly we can change an attribute on the node. Let's change one's attribute!

```javascript
p.textContent = "Goodbye!"
```