# [Functions in JS](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/functions-in-javascript)

## Resources

- MDN
  + [Functions — reusable blocks of code](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Functions)
  + [Function return values](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Return_values)
  + [Function declaration](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/function)

## Introduction

Functions are the single most important unit of code in JavaScript.

Functions serve as ways to group together related bits of JavaScript code.

Grouped code is easier to read, debug, and improve.

## 1. Define abstraction

Abstraction comes from Latin roots which mean "to pull away." It's the
"take-away" or "impression" of a whole thing.  As humans, we often take sets of
single actions or things and _abstract them_ into another word.

**Examples:**

| Single Units | Abstraction |
|-------------|--------------|
|John, Paul, George, Ringo | The Beatles |
|Get two pieces of bread, put jam on ... | Make a peanut butter and jelly sandwich |
|Hermione, Harry, Ron | Troublesome Gryffindors |
| visit site, make userid, make password... | Sign up for Flatbook|
| get in the lift, hit "G" button, exit elevator, walk to subway... | Go home|

We create abstractions to make it easier to shorten our sentences.

We also use abstractions to decide
what doesn't fit or what should fit. "Mozart" doesn't belong with The Beatles,
but he does fit with "Baroque Masters."

Abstractions help us think about complex activities. Humans brought the pattern of
"abstracting work" to JavaScript. Abstractions that hold work are called
_functions_.

## 2. Explain that functions are abstractions

Functions combine series of steps under a new name. That's why they're
_abstractions_. We'll call that the _function name_.

More formally:
**A function is an object that contains a sequence JavaScript
statements.  We can execute or _call_ it multiple times.**

## 3. Explain how to _call_ a function

To _call_ a function means to run the independent pieces that make it.
Synonyms to _call_ that you might see are _execute_ and _invoke_.

To "execute" or "call" a function you add `()` after its name.

Example function:

```javascript
function exerciseByronThePoodle() {
  console.log("Wake Byron the poodle");
  console.log("Leash Byron the poodle");
  console.log("Walk to the park Byron the poodle");
  console.log("Throw the fribsee for Byron the poodle");
  console.log("Walk home with Byron the poodle");
  console.log("Unleash Byron the poodle");
}
```

To execute the function we just defined in JavaScript, you run: `exerciseByronThePoodle()`.

That `()` is also known as the _invocation operator_ because
it tells JavaScript to...invoke the function.

A _function_ must be _declared_ before it can be called. Calling
`exerciseByronThePoodle()` before the function has been declared causes an
error for JavaScript.

## 4. Define "Generalization"

Looking at our abstraction, `exerciseByronThePoodle()`, it's pretty concrete, the
opposite of abstract. It's concrete because it only works for Byron the Poodle.
Our function would be more _abstract_ if it were written for _all dogs_ and it
just-so-happened that Byron the Poodle was one of the eligible things to
undergo the function's processes. The process of moving from _concrete_ to
_abstract_ is called "generalization" (or "abstraction," by some).

## 5. Demonstrate "Generalization" by using _parameters_ and _arguments_

Let's make `exerciseByronThePoodle()` more general.

Looking at the `console.log()` statements, we repeatedly refer to a dog's name and a dog's breed.

Both of these are `Strings`. If we were to write them as JavaScript
variables inside the function we might write `dogName` and `dogBreed`.

Let's use `String` interpolation to generalize the _body_ of our function

```javascript
function exerciseByronThePoodle(dogName, dogBreed) {
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park ${dogName} the ${dogBreed}`);
  console.log(`Throw the fribsee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
}
```

Using interpolation, we've declared parameters for this function.

 _Parameters_ are locally-scoped variables that are usable ("scoped") to inside the function.

In our example, our variables `dogName` and `dogBreed` should become _parameters_.  They're defined inside of the _function declaration's_ `()`.

```javascript
function exerciseDog(dogName, dogBreed) {
...
...
```

JavaScript will assign the _arguments_ of "Byron" and "poodle" to the
_parameters_ `dogName` and `dogBreed` when this function is called like so:

```javascript
function exerciseDog("Byron", "poodle");
```

When the function is _called_, it assigns `dogName = "Byron"` and `dogBreed =
"poodle"`. The parameters are usable inside the function body _as if_ they had
been set with `let` inside the function.

Because our function is now more _general_, we can:

```javascript
exerciseDog("Boo", "puggle");
exerciseDog("Jojo", "mutt");
exerciseDog("Emmeline", "bernedoodle");
```

If expected arguments aren't given, the parameters won't be set. The
parameters' values will be `undefined`.  This is just like non-initialized
variables; set them else they're `undefined`.  **This will not cause an error
in JavaScript**. This can lead to humorous bugs like:

```text
"Wake undefined the undefined"  // From: console.log("Wake ${dogName} the ${dogBreed}");
```

We can assign default arguments to our parameters. While it's not as attention-
grabbing as a real error, it's a helpful signal that we've run off the rails.

```javascript
function exerciseDog(dogName="ERROR the Broken Dog", dogBreed="Sick Puppy") {
...
```

## 6. Demonstrate _return values_

Sometimes it's helpful to send something _back_ to the place where the function
was _called_. 

It's like a "summary" of what happened in the function. 

In real life, we expect the function "bake a cake" to return a "cake". Or we expect
"Visit the ATM" to return paper money. Functions in JavaScript can also return
things.  Consider:

```javascript

let weatherToday = "Rainy";

function exerciseDog(dogName, dogBreed) {
  if (weatherToday === "Rainy") {
    return `${dogName} did not exercise due to rain`;
  }
  console.log(`Wake ${dogName} the ${dogBreed}`);
  console.log(`Leash ${dogName} the ${dogBreed}`);
  console.log(`Walk to the park ${dogName} the ${dogBreed}`);
  console.log(`Throw the fribsee for ${dogName} the ${dogBreed}`);
  console.log(`Walk home with ${dogName} the ${dogBreed}`);
  console.log(`Unleash ${dogName} the ${dogBreed}`);
  return `${dogName} is happy and tired!`
}

let result = exerciseDog("Byron", "poodle");
console.log(result); // => "Byron did not exercise due to rain"
```

In JavaScript, when a function is _called_, when it encounters a `return`
statement it "returns" the value of the thing that appears to the right of the word.

The thing could be a `String`, a `Number` or an _expression_ like `1 + 1` (which returns, `2`, sensibly enough).

When a `return` is reached in the code, no further code behavior happens.

Above, if `weatherToday` is `truthy` **the only thing that happens** is the
evaluation of the `String`.

Return values can be saved to variables. Or they can be used as inputs to other
functions.
