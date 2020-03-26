# [Eventing Master](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/you-re-an-eventing-master)

## Reflect

Remember our "Simple Liker" program? In it we saw that front-end web programming
is using three "pillars" working together:

[x] Manipulating the DOM
[x] Recognizing JavaScript events
[ ] Communicating with the server

Now you've conquered this section, you've learned all the fundamentals of the
second pillar, recognizing JavaScript events. You used JavaScript events to
invoke actions, created JavaScript functions and implemented event listeners.

----

# [Quiz: Reviewing JavaScript Events](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/quiz-reviewing-javascript-events)

?: Choose the best definition of scope in JavaScript.

( ) the functions that the browser 'knows about' by default 
( ) variables and functions get 'hoisted' to the top
( ) the value of the variables defined inside a function
(X) where declared variables and functions are visible

?: Variables declared with \_\_\_ are block-scoped:

( ) `var`
(X) `let`
( ) `function`

?: Through its scope, a function:

(X) has access to all variables and functions declared in its enclosing scope.
( ) has access to all variables and functions declared only in its inner scope.
( ) has access to variables and functions declared anywhere.
( ) continues to move up the scope chain when it finds a matching identifier in the current scope.

?: In the code example below, what will `myVar` equal when `function2()` is run? That is, what will be logged?

```javascript
const myVar = "Foo";
function function1() {
  const myVar = "Baz";
  console.log(myVar);
}
function function2() {
  const myVar = "Bar";
  function1();
}
function2();
```

(X) "Baz"
( ) "Foo"
( ) "Bar"
( ) undefined

?: How can a JavaScript event be defined on any DOM node?

(X) `addEventListener()`
( ) `getElementById()`
( ) `querySelector()`
( ) `click()`

?: Which of these is NOT an example of a JavaScript event?

( ) Submitting a form
(X) Calling a javascript function in the global scope
( ) Pressing a key
( ) Scrolling in the browser window

?: Which variable keyword will be hoisted?

( ) `let`
( ) `const`
( ) `def`
(X) `var`

?: Which of the following is NOT true about functions?

( ) functions contain a sequence of JavaScript statements.
( ) functions can be executed multiple times.
(X) functions are always executed first.
( ) functions are objects.

?: Choose the version of this function that is the best example of generalization.

(X)

```javascript
function volunteerTShirtOrder(name = "Unknown", size = "Any") {
  console.log(`${name} ordered a size ${size}`);
}
```

( )

```javascript
function volunteerTShirtOrder(name, size) {
  let name = "Octavius";
  let size = "Large";
  console.log(`${name} ordered a size ${size}`);
}
```

( )

```javascript
function volunteerTShirtOrder(x, y) {
  console.log(`${x} ordered a size ${y}`);
}
```

( )

```javascript
function volunteerTShirtOrder(name, size) {
  let name = "Unknown";
  let size = "Any";
  console.log(`${name} ordered a size ${size}`);
}
```

?: The `DOMContentLoaded` event fires when:

( ) the CSS & JavaScript have finished loading.
(X) the page's DOM is fully parsed.
( ) the page has begun loading.
( ) there is an error during the page load.