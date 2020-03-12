# [JS Fundamentals: Scope Chain](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/js-fundamentals-scope-chain)

## Resources

- [MDN: Functions — Name conflicts](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#Name_conflicts)

## Introduction

Every function in JavaScript has access to a _scope chain_, which includes
references to the function's outer scope (the scope in which the function was
declared), the outer scope's outer scope, and so on. In this lesson, we'll
discuss how the scope chain allows us to access variables and functions declared
in outer scopes within an inner function. We'll also talk about what's happening
under the hood when we run JavaScript code and how that impacts _identifier
resolution_ and the _scope chain_.

### 1. Define a scope chain

For a function declared at the top level of our JavaScript file (that is, not
declared inside of another function), its outer scope is the _global scope_.
That means it can access all of the variables and functions declared in the
global scope. When that new function is invoked, it creates a new scope and
**retains a reference to the _outer scope_ in which it was declared**. Inside
the new function's body, in addition to variables and functions declared in that
function, **we also have access to variables and functions declared in the outer
scope**. Let's see that in action:

```js
const globalVar = 1;

function firstFunc () {
  const firstVar = 2;

  return firstVar + globalVar;
}

firstFunc();
// => 3
```

`firstVar` is declared inside the function, and `globalVar` is declared in the
outer scope, but we have access to **both** inside `firstFunc()`.

When we invoke `firstFunc()`, the first line of code inside the function, `const
firstVar = 2;`, runs first, creating a new local variable. When the JavaScript
engine reaches the function's second line, it sees the reference to `firstVar`
and says, "Great, I know what that means: it's a local variable!" Then, the
engine encounters the reference to `globalVar` and says, "What the heck is
this?! That's not declared locally!"

When the engine can't find a local match, it then goes looking in the outer
scope and finds a match there. Because of the way functions can look up
variables declared in outer scopes, we say they have access to a _scope chain_.
Through the scope chain, a function has access to all variables and functions
declared in its outer scope.

***Top Tip***: What matters for the scope chain is where the function is declared —
not where it is invoked.

### 2. Identify how to create nested functions

We can think of JavaScript scopes as a nested system:

![Scope chain](https://curriculum-content.s3.amazonaws.com/web-development/js/principles/scope-chain-readme/scope_chain.png)

All variables and functions declared in outer scopes are available in inner
scopes via the scope chain. This can go on forever, with functions nested in
functions nested in functions, each new level creating a new scope that can
reference functions and variables declared in its outer scopes through the scope
chain.

***NOTE***: The scope chain only goes in _one_ direction. An outer scope **does not
have access to things declared in an inner scope**. In the previous code
snippet, `firstFunc()` **cannot access `secondVar`**. In addition, two
functions declared in the same scope do not have access to anything declared
in the other's scope.

```js
const fruit = 'Apple';

function first () {
  const vegetable = 'Broccoli';

  console.log('fruit:', fruit);
  console.log('vegetable:', vegetable);
  console.log('legume:', legume);
}

function second () {
  const legume = 'Peanut';

  console.log('fruit:', fruit);
  console.log('legume:', legume);
  console.log('vegetable:', vegetable);
}
```

Both `first()` and `second()` have access to `fruit`, but `first()` cannot
access `legume` and `second()` cannot access `vegetable`.

### 3. Describe what happens during the execution phase

Okay, now we have an idea of what the scope chain is, but how does it actually
work underneath the surface?

#### Identifiers

Remember that when we declare a variable or a function, we provide a name that
allows us to refer back to it:

```js
const myVar = "myVar refers to the variable that contains this string";
// => undefined

function myFunc () {
  return "myFunc refers to this function that returns this string";
}
// => undefined
```

We call those names _identifiers_ because they allow us to **identify** the
variable or function we're referring to.

#### The JavaScript Engine

When our JavaScript code is run in the browser, the JavaScript engine actually
makes two separate passes over our code:

##### Compilation Phase

The first pass is the _compilation phase_, in which the engine steps through our
code line-by-line:

1. When it reaches a variable declaration, the engine allocates memory and sets
up a reference to the variable's identifier, e.g., `myVar`.

2. When the engine encounters a function declaration, it does three things:

    - Allocates memory and sets up a reference to the function's identifier,
      e.g., `myFunc`.

    - Creates a new execution context with a new scope.

    - Adds a reference to the parent scope (the outer environment) to the scope
      chain, making variables and functions declared in the outer environment
      available in the new function's scope.

##### Execution Phase

The second pass is the _execution phase_. The JavaScript engine again steps
through our code line-by-line, but this time it actually runs our code,
assigning values to variables and invoking functions.

One of the engine's tasks is the process of matching identifiers to the
corresponding values stored in memory. Let's walk through the following code:

```js
const myVar = 42;

myVar;
// => 42
```

During the compilation phase, a reference to the identifier `myVar` is stored in
memory. The variable isn't yet assigned a value, and the second line (`myVar;`)
is skipped over entirely because it isn't a declaration.

During the execution phase, the value `42` is assigned to `myVar`. When the
engine reaches the second line, it sees the identifier `myVar` and resolves it
to a value through a process known as _identifier resolution_. The engine first
checks the current scope to see if `myVar` has been declared in it. If it finds
no declaration for `myVar` in the current scope, the engine then starts moving
up the scope chain, checking the parent scope and then the parent scope's parent
scope and so on, until it finds a matching declared identifier or reaches the
global scope. If the engine traverses all the way up to the global scope and
still can't find a match, it will throw a `ReferenceError` and inform you that
the identifier is not declared anywhere in the scope chain.

## Conclusion

We covered a lot of details that might seem unnecessary, but they're critical to
understanding how identifier lookups happen in JavaScript. That is, when the
JavaScript engine encounters a variable or function, how it knows what value or
function to retrieve from memory. If the engine finds the identifier declared
locally, it uses that value. However, if it doesn't find a local match, it then
looks up (or down, depending on your perspective) the scope chain until it
either finds a match in an outer scope or throws an `Uncaught ReferenceError`.