# [JS Fundamentals - Arrays](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/js-fundamentals-arrays)

## Resources

1. [MDN - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
2. [MDN - `.slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
3. [MDN - `.splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

## Learning Goals

### Define "data structure"

A **data structure** is a means for associating and organizing information. Outside of the programming world, we use data structures all the time. For example, we might have a shopping list of the items we need to buy on our next grocery run or an address book for organizing contact information.

### Describe collections and `Array`s

`getElementById()` returns a **singular** element whereas `getElementsByTagName()` and `getElementsByClassName()` return **all elements** that match the tag or class name.

The second two methods hint, with **Elements** being plural, that they can return multiple matches -- a _collection._ This is a collection that we are going to call an `Array`.

>NOTE: These methods don't actually return `Array`s. An `HTMLCollection` is actually returned from the first two methods. This is a major point of confusion in JavaScript! the `HTMLCollection` knows its length like an `Array`. We can iterate across it with a `for...in...` loop. But it's not technically an `Array`. This is definitely one of the "warts" of JavaScript but also shows a really mean-spirited interview question. It is not difficult to turn an `HTMLCollection` into an actual `Array` (using a loop, for example) but for our purposes we can treat it as an Array.

We can ask the DOM to give us a collection by using a method that returns multiple elements.

We can then get a single member of a collection by providing an element a number, or _index_ in the `[]` after the collection, like so:

```JavaScript
    document.getElementsByTagName('main')[0]
```

### Create `Array`s



### Access the elements in an `Array`
### Add elements to an `Array`
### Remove elements from an `Array`
### Replace elements in an `Array`
### Create non-destructive copies of Arrays
### Identify nested `Array`s
### Destructure Arrays with "Spread" (`...`) Operator