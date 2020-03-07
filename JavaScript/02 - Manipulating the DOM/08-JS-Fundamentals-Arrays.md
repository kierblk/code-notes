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

An `Array` is a list, with the items listed in a particular order, surrounded by
square brackets (`[]`):

```js
['This', 'is', 'an', 'array', 'of', 'strings.'];
// => ["This", "is", "an", "array", "of", "strings."]
```

The _members_ or _elements_ in an `Array` can be data of any type in JavaScript:

```js
['Hello, world!', 42, null, NaN];
// => ["Hello, world!", 42, null, NaN]
```

> **NOTE**: In some other languages `Arrays` _cannot be of multiple types_. In
C, C++, Java, Swift, and others you cannot mix types. JavaScript, Python, Ruby,
Lisp, and others permit this.

Arrays are _ordered_, meaning that the elements in them will always appear in
the same order. The `Array` `[1, 2, 3]` is different from the `Array` `[3, 2, 1]`.

Just like any other type of JavaScript data, we can assign an `Array` to a
variable:

```js
const primeNumbers = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37];

const tvShows = ['Game of Thrones', 'True Detective', 'The Good Wife', 'Empire'];
```

We can find out how many elements an `Array` contains by checking the `Array`'s
built-in `length` property:

```js
const myArray = ['This', 'array', 'has', 5, 'elements'];

myArray.length;
// => 5
```

We defined the above `Array`s using the _array literal_ syntax — that is, we
literally typed out the `Array` that we wanted to create, square brackets and all.
There are other ways to create new `Array`s, but they are only necessary for very
rare circumstances. For now, use `Array` literals.

To get a sense of just how effective `Array`s are at keeping data organized, let's
store some lottery numbers an `Array`:

```js
const winningNumbers = [32, 9, 14, 33, 48, 5];
```

The `Array` provides organization, and we only have to remember _one_ identifier
(`winningNumbers`) instead of six (`firstNumber`, `secondNumber`, and so on).

We call `Arrays` _expressive_ because putting all the winning numbers in a
shared data structure communicates to other programmers "Hey, these things go
together" in a way that naming them individually e.g. `firstNumber`,
`secondNumber`, etc. _does not_.

The one benefit of storing all six lottery numbers separately is that we had a
really easy way to access each individual number. For example, we might want to
assign `powerBall` to the sixth number. Luckily, `Array`s offer a simple syntax
for accessing individual members.

### Access the elements in an `Array`

Every element in an `Array` is assigned a unique index value that corresponds to
its place within the collection. The first element in the `Array` is at index `0`,
the fifth element at index `4`, and the 428th element at index `427`.

To access an element, we use the _computed member access operator_, AKA "square brackets."

```js
const winningNumbers = [32, 9, 14, 33, 48, 5];
// => undefined

winningNumbers[0];
// => 32

winningNumbers[3];
// => 33
```

***NOTE:*** Most people just call it _bracket notation_ or the _bracket operator_,
so don't worry too much about remembering the term _computed member access
operator_.

Let's take a minute to think about how we could access the **last** element in
any `Array`. Remember, the one we want to make the `powerBall`?

If `myArray` contains 10 elements, the final element will be at `myArray[9]`. If
`myArray` contains 15000 elements, the final element will be at
`myArray[14999]`. So the index of the final element is always one less than the
number of elements in the `Array`. If only we had an easy way to figure out how
many elements are in the `Array`...

```js
const alphabet = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z'];
// => undefined

alphabet.length;
// => 26

alphabet[alphabet.length - 1];
// => "z"
```

This is why it's called the ***computed*** _member access operator_. We put an
expression (`alphabet.length - 1`) inside the square brackets, and the
JavaScript engine _computed_ the value of that expression to determine which
element we were trying to access. In this case, `alphabet.length - 1` evaluated
to `25`, so `alphabet[alphabet.length - 1]` became `alphabet[25]`.

### Add elements to an `Array`

JavaScript allows us to manipulate the members in an `Array` in a number of ways.

#### `.push()` and `.unshift()`

With the `.push()` method, we can add elements to the end of an `Array`:
```js
const superheroes = ['Catwoman', "Miss Marvel", 'She-Hulk', 'Jessica Jones'];

superheroes.push('Wonder Woman');
// => 5

superheroes;
// => ["Catwoman", "Miss Marvel", "She-Hulk", "Jessica Jones", "Wonder Woman"]
```

We can also `.unshift()` elements onto the beginning of an `Array`:

```js
const cities = ['New York', 'San Francisco'];

cities.unshift('Los Angeles');
// => 3

cities;
// => ["Los Angeles", "New York", "San Francisco"]
```

Notice that the value returned by both methods is the `length` of the updated
`Array`.

##### Destructive vs. Nondestructive

Both `.push()` and `.unshift()` update or _mutate_ the original `Array`, adding
elements directly to it. Operations that modify the original collection are
_destructive_, and those that leave the original collection intact are
_nondestructive_.

Mutating the original `Array` isn't necessarily a bad thing, but there's also a
way to add elements nondestructively, leaving the original `Array` intact.

#### Spread Operator

ES2015 introduced the _spread operator_, which looks like an ellipsis: `...`.
The spread operator allows us to spread out the contents of an existing `Array`
into a new `Array`, adding new elements but preserving the original:

```js
const coolCities = ['New York', 'San Francisco'];

const allCities = ['Los Angeles', ...coolCities];

coolCities;
// => ["New York", "San Francisco"]

allCities;
// => ["Los Angeles", "New York", "San Francisco"]
```

We created a new `Array` instead of modifying the original one — our `coolCities`
`Array` was untouched. We can also use the spread operator to add a new item to
the end of an `Array` without modifying the original:

```js
const coolCats = ['Hobbes', 'Felix', 'Tom'];

const allCats = [...coolCats, 'Garfield'];

coolCats;
// => ["Hobbes", "Felix", "Tom"]

allCats;
// => ["Hobbes", "Felix", "Tom", "Garfield"]
```

### Remove elements from an `Array`

As complements for `.push()` and `.unshift()`, respectively, we have `.pop()`
and `.shift()`.

#### `.pop()` and `.shift()`

The `.pop()` method removes the last element in an `Array`, destructively updating
the original `Array`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.pop();
// => "Sun"

days;
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

The `.shift()` method removes the first element in an `Array`, also mutating the
original:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.shift();
// => "Mon"

days;
// => [Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

Notice that the return value for the `.pop()` and `.shift()` methods is the
element that was removed.



### Replace elements in an `Array`
### Create non-destructive copies of Arrays
### Identify nested `Array`s
### Destructure Arrays with "Spread" (`...`) Operator