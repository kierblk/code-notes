# [DOM Editing Lab](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/dom-editing-lab)

## Resources

1. [HTML Block Elements](https://developer.mozilla.org/en/docs/Web/HTML/Block-level_elements)
2. [HTML Inline Elements](https://developer.mozilla.org/en-US/docs/Web/HTML/Inline_elements)

## Learning Goals

  1. Identify that DOM nodes are written as HTML

When viewing the DOM we see HTML that is a clone of the HTML found in the source HTML file. However, DOM nodes represent all components that make up a web page.

DOM nodes most often have a starting tag and an ending tag. Because of this, something else could nest inside. This inner node is called a child node. The outer node is called a parent node.

To nest items in a normal tag, we simply add the child node HTML element content between its parent's starting and ending tags:

```HTML
  <body>
    <main>
      <p>I am a nested paragraph, inside the main element, inside the body!</p>
    </main>
  </body>
```

Some nodes only have a starting tag. Those are called self-closing elements. These elements do not have any content nested inside of them. More technically, they are called void elements. Void elements cannot be parent nodes.

An example of a self-closing tag is an image:

```HTML
  <img src="https://media.giphy.com/media/3o6MbkZSYy4mI3gLYc/giphy.gif" alt="A policeman">
```

In self-closing tags, the trailing / is optional. This is valid too:

```HTML
  <img src="https://media.giphy.com/media/3o6MbkZSYy4mI3gLYc/giphy.gif" alt="A policeman" />
```

Every HTML element has a display value. Since these are known by modern browsers, you don't have to worry about specifying the value unless you want to change it. This value can be many things (including none, which hides the elements), but the default value for most elements is either block or inline. For the images above, the value is inline. 

  2. DOM Tree

  When you expand out a DOM node and all its children, this is called a DOM Tree.