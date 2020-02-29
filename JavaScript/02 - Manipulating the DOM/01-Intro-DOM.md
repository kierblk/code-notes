# [Introducing the DOM and Just Enough JavaScript](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/introducing-the-dom-and-just-enough-javascript)

## Introduction

JavaScript can do many kinds of work, from building web servers, to creating
"infinite scroll" effects, but it was originally designed to do a type of
programming called **Document-Object Model (DOM) programming**. Understanding
DOM programming is the foundation of front-end development.

DOM programming is using JavaScript to:

1.  Ask the DOM to find or `select` an HTML element or elements in the rendered
    page
2.  Remove and/or insert an element(s)
3.  Adjust a property of the selected element(s)

## Learning Goals

1.  Explain the JavaScript / DOM relationship

  JavaScript changes are made through a middle layer called the DOM.

  DOM = Document Object Model

  DOM only knows how to be spoken to in JavaScript.

2.  Explain "sight words"

  Vocabulary that the a person recognizes from memory without the need to decode for understanding.

3.  Explain "just enough JavaScript" concept

  The approach of learning JavaScript sight words as "just enough JavaScript". Meaning, you will learn just a few things to get started without really understanding the full concept.

  [MDN's JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

4.  Write experimental code in Chrome DevTools

  Practicing with a new programming language is exceptionally important. Reading is important, but practice with the code itself is most important.

  As you work through the JS curriculum, you should almost always have a browser console open.

  Every major browser comes with a built-in set of developer tools that you can use to inspect, modify, and debug the content of a web page.

  The console is an environment in the browser where we can type and run arbitrary JavaScript code in the context of the current browser window. The console is sandboxed, meaning the only resources it has access to are those loaded on the current page. Once we start declaring variables and functions in separate JavaScript files, we'll be able to access and play around with them in the console. The console is the single best tool for debugging JavaScript in the browser, so start familiarizing yourself with it now.

5.  Explain that JavaScript has things

  Most programming languages call these "types." For the moment we're going to call them Things.

  - `number` like 2
  - `string` like "Sara" or 'Sara' using either single or double-quotes

6.  Explain that JavaScript has `variables`

  Sometimes you want to hold a String or a Number under another name, this would be called a variable just like any other programming language.

  When JavaScript first came out it had only `var`. Now it has `let` and `const` too. We'll cover the differences between these later. They all tell JavaScript, "Hey! This is a name that I'm going to associate with some bit of information."

7.  Explain that JavaScript can compare things

  

8.  Explain that JavaScript has `collections`
9.  Explain that JavaScript is object-oriented
10.  Explain that JavaScript has `loops`
11. Explain that JavaScript `logs` with `console.log`

