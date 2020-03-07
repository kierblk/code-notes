# [JS Fundamentals - Arrays](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/js-fundamentals-arrays)

* [Arrays Lab](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/js-fundamentals-arrays-lab)

## Resources

1. [MDN - Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
2. [MDN - `.slice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
3. [MDN - `.splice()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)

## Learning Goals

### 1. Define "data structure"

A **data structure** is a means for associating and organizing information. Outside of the programming world, we use data structures all the time. For example, we might have a shopping list of the items we need to buy on our next grocery run or an address book for organizing contact information.

### 2. Describe collections and `Array`s

`getElementById()` returns a **singular** element whereas `getElementsByTagName()` and `getElementsByClassName()` return **all elements** that match the tag or class name.

The second two methods hint, with **Elements** being plural, that they can return multiple matches -- a _collection._ This is a collection that we are going to call an `Array`.

>NOTE: These methods don't actually return `Array`s. An `HTMLCollection` is actually returned from the first two methods. This is a major point of confusion in JavaScript! the `HTMLCollection` knows its length like an `Array`. We can iterate across it with a `for...in...` loop. But it's not technically an `Array`. This is definitely one of the "warts" of JavaScript but also shows a really mean-spirited interview question. It is not difficult to turn an `HTMLCollection` into an actual `Array` (using a loop, for example) but for our purposes we can treat it as an Array.

We can ask the DOM to give us a collection by using a method that returns multiple elements.

We can then get a single member of a collection by providing an element a number, or _index_ in the `[]` after the collection, like so:

```JavaScript
    document.getElementsByTagName('main')[0]
```

### 3. Create `Array`s

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

### 4. Access the elements in an `Array`

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

### 5. Add elements to an `Array`

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

#### Destructive vs. Nondestructive

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

### 6. Remove elements from an `Array`

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

### 7. Create non-destructive copies of Arrays

#### `.slice()`

To remove elements from an `Array` nondestructively (without manipulating the
original `Array`), we can use the `.slice()` method. Just as the name implies, the
`.slice()` method returns a portion, or **slice**, of an `Array`.

##### With No Arguments

If we don't provide any arguments, `.slice()` will return a copy of the original
`Array` with all elements intact:

```js
const primes = [2, 3, 5, 7];

const copyOfPrimes = primes.slice();

primes;
// => [2, 3, 5, 7]

copyOfPrimes;
// => [2, 3, 5, 7]
```

Note that the `Array` returned by `.slice()` has the same elements as the
original, but it's a copy — **the two `Array`s point to different objects in
memory**. If you add an element to one of the `Array`s, it does **not** get added
to the other:

```js
const primes = [2, 3, 5, 7];

const copyOfPrimes = primes.slice();

primes.push(11);
// => 5

primes;
// => [2, 3, 5, 7, 11]

copyOfPrimes;
// => [2, 3, 5, 7]
```

#### With Arguments

We can provide two arguments to `.slice()`, the index where the slice should
begin and the index **before which** it should end:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(2, 5);
// => ["Wed", "Thu", "Fri"]
```

If no second argument is provided, the slice will run from the index specified
by the first argument to the end of the `Array`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(5);
// => ["Sat", "Sun"]
```

To remove the first element and return a new `Array`, we call `.slice(1)`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(1);
// => ["Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
```

And we can remove the last element in a way that will look familiar from earlier
in this lesson:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(0, days.length - 1);
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat"]
```

In fact, `.slice()` provides an easier syntax for grabbing the last element in
an `Array`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.slice(-1);
// => ["Sun"]

days.slice(-3);
// => ["Fri", "Sat", "Sun"]
```

When we provide a negative index, the JavaScript engine knows to start counting
from the last element in the `Array` instead of the first.

***DO NOT read about slice() and shrug and move on. It's used everywhere in JavaScript
code and having to look up it's parameters every time is a major time-loss. Memorize its
call format now.***

#### `.splice()`

While `.slice()` allows us to return a piece of an `Array` without mutating the
original (nondestructive), `.splice()` performs destructive actions. Let's
familiarize ourselves with the [MDN documentation][splice]:

![`Array.prototype.splice()` documentation on MDN](https://user-images.githubusercontent.com/17556281/29643370-b7f81d3e-883c-11e7-9ce4-f514d90c1727.png)

The documentation shows three ways to use `.splice()`:

```js
array.splice(start)
array.splice(start, deleteCount)
array.splice(start, deleteCount, item1, item2, ...)
```

#### With a Single Argument

```js
array.splice(start)
```

The first argument expected by `.splice()` is the index at which to begin the
splice. If we only provide the one argument, `.splice()` will destructively
remove a chunk of the original `Array` beginning at the provided index and
continuing to the end of the `Array`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];

days.splice(2);
// => ["Wed", "Thu", "Fri", "Sat", "Sun"]

days;
// => ["Mon", "Tue"]
```

Notice that `.splice()` returns the removed chunk and leaves the remaining
elements in the original `Array`.

With a negative 'start' index, the opposite happens:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]

days.splice(-2);
// => ["Sat", "Sun"]

days;
// => ["Mon", "Tue", "Wed", "Thu", "Fri"]
```

#### With Two Arguments

```js
array.splice(start, deleteCount)
```

When we provide two arguments to `.splice()`, the first is still the index at
which to begin splicing, and the second dictates how many elements we want to
remove from the `Array`. For example, to remove `3` elements, starting with the
element at index `2`:

```js
const days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'];
// => ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]

days.splice(2, 3);
// => ["Wed", "Thu", "Fri"]

days;
// => ["Mon", "Tue", "Sat", "Sun"]
```

### 8. Replace elements in an `Array`

#### `.splice()` with 3+ arguments

```js
array.splice(start, deleteCount, item1, item2, ...)
```

After the first two, every additional argument passed to `.splice()` will be
inserted into the `Array` at the position indicated by the first argument. We can
replace a single element in an `Array` as follows, discarding a card and drawing a
new one:

```js
const cards = ['Ace of Spades', 'Jack of Clubs', 'Nine of Clubs', 'Nine of Diamonds', 'Three of Hearts'];

cards.splice(2, 1, 'Ace of Clubs');
// => ["Nine of Clubs"]

cards;
// => ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

Or we can remove two elements and insert three new ones as our restaurant
expands its vegetarian options:

```js
const menu = ['Jalapeno Poppers', 'Cheeseburger', 'Fish and Chips', 'French Fries', 'Onion Rings'];

menu.splice(1, 2, 'Veggie Burger', 'House Salad', 'Teriyaki Tofu');
// => ["Cheeseburger", "Fish and Chips"]

menu;
// => ["Jalapeno Poppers", "Veggie Burger", "House Salad", "Teriyaki Tofu", "French Fries", "Onion Rings"]
```

We aren't required to remove anything with `.splice()` — we can use it to
insert elements anywhere within an `Array`. Here we're adding new books to our
library in alphabetical order:

```js
const books = ['Bleak House', 'David Copperfield', 'Our Mutual Friend'];

books.splice(2, 0, 'Great Expectations', 'Oliver Twist');
// => []

books;
// => ["Bleak House", "David Copperfield", "Great Expectations", "Oliver Twist", "Our Mutual Friend"]
```

Notice that `.splice()` returns an empty `Array` when we provide a second argument
of `0`. This makes sense because the return value is the set of elements that
were removed, and we're telling it to remove `0` elements.

Keep playing around with `.splice()` in your browser's console to get
comfortable with it.

#### Using the Computed Member Access Operator to Replace Elements

If we only need to replace a single element in an `Array`, there's a simpler
solution than `.splice()`:

```js
const cards = ['Ace of Spades', 'Jack of Clubs', 'Nine of Clubs', 'Nine of Diamonds', 'Three of Hearts'];

cards[2] = 'Ace of Clubs';
// => "Ace of Clubs"

cards;
// => ["Ace of Spades", "Jack of Clubs", "Ace of Clubs", "Nine of Diamonds", "Three of Hearts"]
```

However, using the computed member access operator (`[]`) is still _destructive_
— it modifies the original `Array`. There's a _nondestructive_ way to replace or
add items at arbitrary points within an `Array`, and it involves two of the
concepts we learned earlier.

### 9. Identify nested `Array`s


### 10. Destructure Arrays with "Spread" (`...`) Operator