# [Introduction to the DOM To Get Started](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/introduction-to-the-dom-to-get-started)

## Resources

  1. [CSS Tricks - What is the DOM?](https://css-tricks.com/dom/)
  2. [MDN - The DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)

## Learning Goals

### 1. Identify the Document Object Model (DOM)

  Let's start with a biology metaphor.
  Your DNA represents a code-based version of you.
  The DOM represents a code-based version of a web page. 

### 2. Explain how the DOM is created

  The DOM is created when the page loads from the HTML that the web server provides the browser.

  - The browser reads the HTML of a website, along with the CSS and JavaScript, to create the DOM **inside** the browser. At this point, nothing is displayed on the screen and lasts for such a brief second that our human eyes never really catch it. But its there.
  - The browser then uses the DOM object to create the rendered page.

  >While we often learn that browsers "display HTML" that's not exactly accurate. Browsers use the HTML to create a "middleman" that they, in turn use to display the structured and styled content.

### 3. Identify the DOM as accessed by JavaScript objects

Recall that JavaScript is object-oriented. The DOM is available inside a browser through **two** variables:

  1. `window`
  2. `document`

  #### `window`

  The `window` variable points to an object that represents the browser's information about the browser window.

  It has many functions, but the main one is "its a place where everything is."

  A browser without `window` doesn't exist, its simply nothing.

  Like all objects, `window` has methods. We won't use them too much as we don't want to mess with the container of **everything** or any operating system stuff.

  #### `document`

  When we want to change content we will focus on an object called `document`.

  As an object, `document` has properties:

  ```JavaScript
  document.URL //=> http://www.flatironschool.com
  ```

  As an object, `document` also has methods:

  ```JavaScript
  document.write("Woof!") //=> Removes all existing DOM content, replaces it with "Woof!"
  ```

  The methods and properties that DOM provides via its objects is called the DOM's **Application Programming Interface** or API.

  API is just a programming word that you're likely to see online but it simply means, "the things that these objects know how to do."

## Conclusion

In this lesson we met our partner, the DOM, a JavaScript object that is a representation of the HTML, CSS and JavaScript loaded by the browser when we visit a page. 

We normally interact with it through the `document` object. Because it is the **"source of truth"** for what browsers display, changes to the DOM create changes in the browser screen.
