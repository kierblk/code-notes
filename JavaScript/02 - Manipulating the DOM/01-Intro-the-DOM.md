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

### 1.  Explain the JavaScript / DOM relationship

  JavaScript changes are made through a middle layer called the DOM.

  DOM = Document Object Model

  DOM only knows how to be spoken to in JavaScript.

### 2.  Explain "sight words"

  Vocabulary that the a person recognizes from memory without the need to decode for understanding.

### 3.  Explain "just enough JavaScript" concept

  The approach of learning JavaScript sight words as "just enough JavaScript". Meaning, you will learn just a few things to get started without really understanding the full concept.

  [MDN's JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)

### 4.  Write experimental code in Chrome DevTools

  Practicing with a new programming language is exceptionally important. Reading is important, but practice with the code itself is most important.

  As you work through the JS curriculum, you should almost always have a browser console open.

  Every major browser comes with a built-in set of developer tools that you can use to inspect, modify, and debug the content of a web page.

  The console is an environment in the browser where we can type and run arbitrary JavaScript code in the context of the current browser window. The console is sandboxed, meaning the only resources it has access to are those loaded on the current page. Once we start declaring variables and functions in separate JavaScript files, we'll be able to access and play around with them in the console. The console is the single best tool for debugging JavaScript in the browser, so start familiarizing yourself with it now.

### 5.  Explain that JavaScript has things

  Most programming languages call these "types." For the moment we're going to call them Things.

  - `number` like 2
  - `string` like "Sara" or 'Sara' using either single or double-quotes

### 6.  Explain that JavaScript has `variables`

  Sometimes you want to hold a String or a Number under another name, this would be called a variable just like any other programming language.

  When JavaScript first came out it had only `var`. Now it has `let` and `const` too. We'll cover the differences between these later. They all tell JavaScript, "Hey! This is a name that I'm going to associate with some bit of information."

### 7.  Explain that JavaScript can compare things

  Just like with Ruby we can compare things. With JS `=` is assignment also while `==` and `===` are equality comparison operators.

  With the ability to compare things, we are able to build logic into our code using if statements.

### 8.  Explain that JavaScript has `collections`

  Sometimes a variable might point to a Thing which actually has multiple Things inside of it. In programming vocabulary, these collection-Things are called Arrays.

  In JavaScript, arrays start at 0.

  ```JavaScript
    slytherins[0]; //=> "Salazar Slytherin"
    slytherins[1]; //=> "Bellatrix Black"
    slytherins[2]; //=> "Draco Malfoy"
  ```

### 9.  Explain that JavaScript is object-oriented

  When working with the DOM in JavaScript, many of the Things you encounter are objects. Objects are bits of code you can talk to that know state and behavior. Objects should round out our universe of JavaScript Things along with arrays, strings, and numbers.

  When talking to an object you can ask it for a bit of state by using a . and then that state's name. You can trigger behavior by using a . and then the behavior's name followed by (). Due to the . being the separator between the object-name and the state or behavior name, we call writing code this way "dot-notation."

  The thing that holds a bit of state is known as a property. 

  This all sounds a bit confusing, but it's a bit simpler than it sounds. To ask, say, an adorable poodle its name state, you would do it like so:

  ```JavaScript
  poodle.name; //=> "Byron"
  ```

If you ask an object for a property it doesn't have, JavaScript says undefined

```JavaScript
poodle.favoritePainter; //=> undefined
```

When asking an object to do something (a behavior), you use a . and a behavior-name (usually a verb) followed by (). Behaviors on objects are called methods.

```JavaScript
poodle.bark(); //=> An ear-splitting bark is heard
```

Objects' methods have access to all of that object's properties.

```JavaScript
poodle.introduceYourselfFormally(); //=> "Hello, my name is Byron the poodle"
```

In this case, the method introduceYourselfFormally presumably looks at poodle's name property and adds some text around it. We might imagine that it's making "Hello, my name is " + this.name + " the poodle". As it turns out, that is entirely valid JavaScript and it is probably what's happening!

Finally, methods can take arguments. Arguments change the method's operation.

```JavaScript
poodle.eat(1); //=> "Byron eats 1 can of food"
poodle.eat(2); //=> "Byron eats 2 cans of food"
```

Methods can take multiple arguments.

```JavaScript
poodle.eyeEnviously('Shack Burger', '$', 9.57);
// ==> "Byron eyes your Shack Burger enviously, hoping you will drop some,
// ==> not caring the least that it cost you $9.57."
```

Here we can imagine JavaScript doing some calculations to turn the Number 9.57 and String $ into the new string $9.57. We can also imagine it using the property of name to supply Byron.

**A very important object when working with the DOM is called document.**

### 10.  Explain that JavaScript has `loops`

  Sometimes you don't want to manually type something out multiple times, but you want to perform some action "for each" element in a collection. That's where looping comes in.

  The `for` loop.

  Let's pull together several of the concepts of this lesson by coding:

>"for each" character in the slytherin collection (or "Array"), we would like the harry_potter object to invoke its expelliarmus method on the wizard or witch who is passed in as an argument:

```JavaScript
for (let i = 0; i < slytherins.length; i = i + 1) {
  harry_potter.expelliarmus(slytherins[i]);
}
```

  The important thing to take away is the ability to "sight read" that for invokes the idea of doing some repeating action for each element in a collection.

### 11. Explain that JavaScript `logs` with `console.log`

  In the examples that follow, and in much of the technical documentation of JavaScript, you will see the following method used: console.log(). This method is used to print something. Often it's used to print out a variable or some bit of data to make a point or to debug something.

  Let's build on the loop example. Let's say we want to know who harry_potter is defending against:

  ```JavaScript
  for (let i = 0; i < slytherins.length; i = i + 1) {
    console.log(`Harry is about to disarm ${slytherins[i]}`);
    harry_potter.expelliarmus(slytherins[i]);
    console.log(`${slytherins[i]} is defenseless!`);
  }
  ```

  We'll discuss this method in more detail later, but it's a way to get JavaScript to "talk to our screen."