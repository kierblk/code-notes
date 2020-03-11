# [JS Fundamentals: Scope](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/js-fundamentals-scope)

## Resources

- [MDN: Scope](https://developer.mozilla.org/en-US/docs/Glossary/Scope)
- [MDN: Function Scope](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide

## Introduction

In JavaScript, scope is defined by where declared variables and functions are visible.

### 1. Identify how scope works in JavaScript

_Scope_ is the concept of **where something is available**.

Just as every message on Slack is sent in a channel, every piece of JavaScript code is run in an **execution context**. In a Slack channel, we have access to all of the messages sent in that channel; we can send a message that references any of the other messages posted in the same channel. Similarly, in a JavaScript execution context, we have access to all of the variables and functions declared in that context. Within an execution context, we can write an expression that references a variable or invokes a function declared in the same context.

### 2. Identify different types of scope

#### Global Scope

Up to this point, almost all of the JavaScript code we've written has lived in
the _global execution context_. Variables and functions declared in the global
execution context — in the _global scope_ — are accessible everywhere in your
JavaScript code.

![Execution context and scope](https://curriculum-content.s3.amazonaws.com/web-development/js/principles/scope-readme/execution_context_and_scope_1.png)

Here's a look at what that looks like in JavaScript:

```js
// 'myFunc' is declared in the global scope and available everywhere in your code:
function myFunc () {
  return 42;
}
// => undefined

// 'myVar' is able to reference and invoke 'myFunc' because both are declared in the same scope (the global execution context):
const myVar = myFunc() * 2;
// => undefined

myVar;
// => 84
```

![Execution context and scope](https://curriculum-content.s3.amazonaws.com/web-development/js/principles/scope-readme/execution_context_and_scope_2.png)

***Top Tip***: If a variable or function is **not** declared inside a function or
block, it's in the global execution context.

#### Function Scope

When we declare a new function and write some code in the function body, we're
no longer in the global execution context. The function creates a new execution
context with its own scope. Inside the function body, we can reference variables
and functions declared in the function's scope:

```js
function myFunc () {
  const myVar = 42;

  return myVar * 2;
}
// => undefined

myFunc();
// => 84
```

However, from outside the function, we can't reference anything declared inside
of it:

```js
function myFunc () {
  const myVar = 42;
}
// => undefined

myVar * 2;
// Uncaught ReferenceError: myVar is not defined
```

The function body creates its own scope. It's like a separate channel on Slack —
only the members of that channel can read the messages sent in it.

#### Block Scope

A block statement also creates its own scope... kind of. As of ES2015,
JavaScript has partial support for block scoping.

Variables declared with `var` are **not** block-scoped:

```js
if (true) {
  var myVar = 42;
}

myVar;
// => 42
```

However, variables declared with `const` and `let` **are** block-scoped:

```js
if (true) {
  const myVar = 42;

  let myOtherVar = 9001;
}

myVar;
// Uncaught ReferenceError: myVar is not defined

myOtherVar;
// Uncaught ReferenceError: myOtherVar is not defined
```

This is yet another reason to **never use `var`**. As long as you stick to
declaring variables with `const` and `let`, what happens in block stays in
block.

### 3. Identify best practices in defining scope

In a perfect world, you'd always remember to declare new variables with `const`
and `let`, and you'd never run into any unfortunate scoping issues. However,
it's inevitable that at some point you're going to forget the `const` or `let`
and accidentally do something like:

```js
firstName = 'Ada';
```

Variables created without a `const`, `let`, or `var` keyword are **always
globally-scoped**, regardless of where they sit in your code. If you create one
inside of a block, it's still available globally:

```js
if (true) {
  lastName = 'Lovelace';
}

lastName;
// => "Lovelace"
```

If you create one inside of a function, it's still available globally:

```js
function bankAccount () {
  secretPassword = 'il0v3pupp135';

  return 'bankAccount() function invoked!';
}

bankAccount();
// => "bankAccount() function invoked!"

secretPassword;
// => "il0v3pupp135"
```

Declaring global variables and functions should only be
used as a last resort if you absolutely need access to something **everywhere**
in your program. In general, it's best practice to make variables and functions
available only where they're needed — and nowhere else. Making a variable
available in places that shouldn't have access to it can only lead to bad things
and make your debugging process more complex.