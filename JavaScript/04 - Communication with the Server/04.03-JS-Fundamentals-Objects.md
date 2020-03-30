# [JS Fundamentals - Objects ](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/communication-with-the-server/js-fundamentals-objects)

## Resources
- MDN
  + [`Object.assign()`][assign]
  + [`Object.keys()`][keys]
  + [`delete`][delete]
  + [Object basics][Basics]

[assign]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign
[keys]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys
[delete]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete
[Basics]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Basics
- [Objects in javascript : object.assign/deep copy](https://medium.com/@tkssharma/objects-in-javascript-object-assign-deep-copy-64106c9aefab)

## Introduction

`Array`s are great for representing simple, ordered data sets, but they're
generally not so great at modeling a more complex structure. For that, we need
`Object`s.

> **ASIDE**: Un-helpfully JavaScript called this thing with curly braces (`{}`)
> an `Object`.
>
> It's similar to Ruby's `Hash`, Python's `Dictionary` or C-like languages'
> `struct`(ure).
>
> There *is* a relationship to object-oriented 
> programming where we create classes and instances, but that's not what's
> at play here. Don't confuse the two.
>
> When JavaScript was created, it was thinking it'd only be a lightweight language
> for doing DOM-based programming. It didn't think that it would ever need
> "object orientation" like Java or C++ did. But JavaScript turned out to be
> way more popular than even it expected and **later** gained that class- and
> instance-based thing known as "Object-Oriented Programming."
>
> So for this lesson and the next few that follow, try not to think
> of `Object` as being like "Object-Oriented Programming," but instead think
> of it as being closer to a key/value based data structure.

## 1. Identify JavaScript `Object`s

JavaScript `Object`s are a collection of properties bounded by curly braces (`{ }`), similar to a hash in Ruby. The properties can point to values of any data type — even other `Object`s.

We can have empty `Object`s:

```js
{}
```

Or `Object`s with a single _key-value_ pair:

```js
{ key: value }
```

When we have to represent multiple key-value pairs in the same `Object` (which is
most of the time), we use commas to separate them out:

```js
{
  key1: value1,
  key2: value2
}
```

For a real example, let's see our address as an `Object`:

```js
const address = {
  street1: '11 Broadway',
  street2: '2nd Floor',
  city: 'New York',
  state: 'NY',
  zipCode: 10004
};
```

The real data in an `Object` is stored in the _value_ half of the key-value
pairings. The _key_ is what lets us access that value. In the same way we use
_identifiers_ to name variables and functions, inside an `Object` we assign each
value a key. We can then refer to that key and the JavaScript engine knows
exactly which value we're trying to access.

## 2. Access a value stored in an `Object`

There are two ways to access values in an `Object`, one of which we already
learned about in the `Array`s lesson: dot notation and bracket notation.

### Dot Notation

With _dot notation_, we use the _member access operator_ (a single period) to
access values in an `Object`. For example, we can grab the individual pieces of
our address, above, as follows:

```js
address.street1;
// => "11 Broadway"

address.street2;
// => "2nd Floor"

address.city;
// => "New York"

address.state;
// => "NY"

address.zipCode;
// => 10004
```

Dot notation is fantastic for readability, as we can just reference the bare key
name (e.g., `street1` or `zipCode`). Because of this simple syntax, it should be
your go-to strategy for accessing the properties of an `Object`.

***NOTE***: Most people just call it _dot notation_ or the _dot operator_, so don't
worry too much about remembering the term _member access operator_.

### Bracket Notation

With _bracket notation_, we use the _computed member access operator_, which,
recall from the lesson on `Array`s, is a pair of square brackets (`[]`). To access
the same properties as above, we need to represent them as strings inside the
operator:

```js
address['street1'];
// => "11 Broadway"

address['street2'];
// => "2nd Floor"

address['city'];
// => "New York"

address['state'];
// => "NY"

address['zipCode'];
// => 10004
```

Bracket notation is a bit harder to read than dot notation, so we always default
to the latter. However, there are two main situations in which to use bracket
notation.

#### With Nonstandard Keys

If (for whatever reason) you need to use a nonstandard string as the key in an
`Object`, you'll only be able to access the properties with bracket notation. For
example, this is a valid `Object`:

```js
const wildKeys = {
  'Cash rules everything around me.': 'Wu',
  'C.R.E.A.M.': 'Tang',
  'Get the money.': 'For',
  "$ $ bill, y'all!": 'Ever'
};
```

It's impossible to access those properties with dot notation.In order to access a property via dot notation, **the key must follow the same
naming rules applied to variables and functions**. It's also important to note
that under the hood **all keys are strings**. 

Don't waste too much time
worrying whether a key is accessible via dot notation. If you follow these rules
when naming your keys, everything will work out:

- camelCaseEverything
- Start the key with a lowercase letter
- No spaces or punctuation

If you follow those three rules, you'll be able to access all of an `Object`'s
properties via bracket notation **or** dot notation.

***Top Tip***: Always name your `Object`'s keys according to the above three rules.
Keeping everything standardized is good, and being able to access properties
via dot notation is much more readable than having to always default to
bracket notation.

#### Accessing Properties Dynamically

The other situation in which bracket notation is required is if we want to
dynamically access properties. From the lesson on `Array`s, remember why we call
it the _computed member access operator_: we can place any expression inside the
brackets and JavaScript will _compute_ its value to figure out which property to
access. 

The real strength of bracket notation is its ability to compute
the value of variables on the fly. For example:

```js
const meals = {
  breakfast: 'Oatmeal',
  lunch: 'Caesar salad',
  dinner: 'Chimichangas'
};

let mealName = 'lunch';

meals[mealName];
// => "Caesar salad"
```

If we try to use the `mealName` variable with dot notation, it doesn't work:

```js
mealName = 'dinner';
// => "dinner"

meals.mealName;
// => undefined
```

With dot notation, JavaScript doesn't treat `mealName` as a variable — it checks
whether a property exists with a key of `mealName`, only finds properties named
`breakfast`, `lunch`, and `dinner`, and so returns `undefined`. Essentially, dot
notation is for when you know the exact name of the property in advance, and
bracket notation is for when you need to compute it when the program runs.

The need for bracket notation doesn't stop at dynamically setting properties on
an already-created `Object`. Since the ES2015 update to JavaScript, we can also
use bracket notation to dynamically set properties _during the creation of a new
`Object`_. For example:

```js
const morningMeal = 'breakfast';
const middayMeal = 'lunch';
const eveningMeal = 'dinner';

const meals = {
  [morningMeal]: 'French toast',
  [middayMeal]: 'Personal pizza',
  [eveningMeal]: 'Fish and chips'
};

meals;
// => { breakfast: "French toast", lunch: "Personal pizza", dinner: "Fish and chips" }
```

Let's try doing the same thing without the square brackets:

```js
const morningMeal = 'breakfast';
const middayMeal = 'lunch';
const eveningMeal = 'dinner';

const meals = {
  morningMeal: 'French toast',
  middayMeal: 'Personal pizza',
  eveningMeal: 'Fish and chips'
};

meals;
// => { morningMeal: "French toast", middayMeal: "Personal pizza", eveningMeal: "Fish and chips" }
```

Without the square brackets, JavaScript treated each key as a literal
identifier instead of a variable. Bracket notation — the _computed member access
operator_ once again shows its powers of computation!

Bracket notation will really come in handy when we start iterating over `Object`s
and programmatically accessing and assigning properties.

## 3. Add a property to an `Object`

To add properties to an `Object`, we can use either dot notation or bracket
notation:

```js
const circle = {};

circle.radius = 5;

circle['diameter'] = 10;

circle.circumference = circle.diameter * Math.PI;
// => 31.41592653589793

circle['area'] = Math.PI * circle.radius ** 2;
// => 78.53981633974483

circle;
// => { radius: 5, diameter: 10, circumference: 31.41592653589793, area: 78.53981633974483 }
```
Note that modifying an `Object`'s properties using dot notation is _destructive_.
This means that we're making changes directly to the original `Object`. 

## 4. Use convenience methods like `Object.assign()` and `Object.keys()`

Is there a way to nondestructively merge the change(s) into a
new `Object`, leaving the original intact?

We can create a method that accepts an old menu and creates a new menu with the proposed changes:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  // Code to return new, updated menu object
}
```

Then, with the ES2015 _spread operator_, we can copy all of the old menu
`Object`'s properties into a new `Object`:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  const newObj = { ...obj };

  // Code to return new, updated menu object
}
```

And finally, we can update the new menu `Object` with the proposed change and
return the updated menu:

```js
function nondestructivelyUpdateObject(obj, key, value) {
  const newObj = { ...obj };

  newObj[key] = value;

  return newObj;
}

const sundayMenu = nondestructivelyUpdateObject(tuesdayMenu, 'fries', 'Shoestring');

tuesdayMenu.fries;
// => "Sweet potato"

sundayMenu.fries;
// => "Shoestring"
```

**A Side Note**: You may notice that we're using `const` here, but _adding_ a key
and value. But that can't be right, since `const` means ***constant***, that is
can't change. The _data_ in a `const` pointing to an `Array` or `Object`
can still be changed, but a new value _cannot_ be assigned to the name. Given `const
x = {}` it's OK to say `x.dog = "Poodle"`, but it is ***not*** OK to say `x = [1,2,3]`.

Anyway, back to nondestructively returning `Object`s. We've got our code written,
but it's quite a bit to write, and it's not very extensible. If we want to
modify more than a single property, we'll have to completely rewrite our
function! Luckily, JavaScript has a much better solution for us.

### `Object.assign()`

JavaScript provides us access to a global `Object` `Object` that has a bunch of
helpful methods we can use. One of those methods is `Object.assign()`, which
allows us to combine properties from multiple `Object`s into a single `Object`. The
first argument passed to `Object.assign()` is the initial `Object` in which all of
the properties are merged. Every additional argument is an `Object` whose
properties we want to merge into the first `Object`:

```js
Object.assign(initialObject, additionalObject, additionalObject, ...);
```

The return value of `Object.assign()` is the initial `Object` after all of the
additional `Object`s' properties have been merged in:

```js
Object.assign({ eggs: 3 }, { flour: '1 cup' });
// => { eggs: 3, flour: "1 cup" }

Object.assign({ eggs: 3 }, { chocolateChips: '1 cup', flour: '2 cups' }, { flour: '1/2 cup' });
// { eggs: 3, chocolateChips: "1 cup", flour: "1/2 cup" }
```

Pay attention to the `flour` property in the above example. **If multiple
`Object`s have a property with the same key, the last key to be defined wins
out**.

A common pattern for `Object.assign()` is to provide an empty `Object` as the
first argument. That way we're composing an entirely new `Object` instead of
modifying or overwriting the properties of an existing `Object`.

Let's write a function for our restaurant that accepts an old menu and some
changes we want to make and returns a new menu **without modifying the old
menu**:

```js
function createNewMenu (oldMenu, menuChanges) {
  return Object.assign({}, oldMenu, menuChanges);
}

const tuesdayMenu = {
  cheesePlate: {
    soft: 'Chèvre',
    semiSoft: 'Gruyère',
    hard: 'Manchego'
  },
  fries: 'Sweet potato',
  salad: 'Caesar'
};

const newOfferings = {
  cheesePlate: {
    soft: 'Brie',
    semiSoft: 'Fontina',
    hard: 'Provolone'
  },
  salad: 'Southwestern'
};

const wednesdayMenu = createNewMenu(tuesdayMenu, newOfferings);

wednesdayMenu;
// => { cheesePlate: { soft: "Brie", semiSoft: "Fontina", hard: "Provolone" }, fries: "Sweet potato", salad: "Southwestern" }

tuesdayMenu;
// => { cheesePlate: { soft: "Chèvre", semiSoft: "Gruyère", hard: "Manchego" }, fries: "Sweet potato", salad: "Caesar" }
```

**Note:** For deep cloning, we need to use other alternatives because `Object.assign()` copies property values. 

For example, if `newOfferings` did not have an updated value for `hard` cheese such as:

```js
const newOfferings = {
  cheesePlate: {
    soft: 'Brie',
    semiSoft: 'Fontina'
  },
  salad: 'Southwestern'
};
```

Our output for `const wednesdayMenu = createNewMenu(tuesdayMenu, newOfferings);` would look like this:

```js
wednesdayMenu;
// => { cheesePlate: { soft: "Brie", semiSoft: "Fontina"}, fries: "Sweet potato", salad: "Southwestern" }
```

... instead of the desired outcome of this:

```js

wednesdayMenu;
// => { cheesePlate: { soft: "Brie", semiSoft: "Fontina", hard: 'Manchego'}, fries: "Sweet potato", salad: "Southwestern" }
```

### `Object.keys()`

Another convenience method available on the global `Object` `Object` is
`Object.keys()`. When an `Object` is passed as an argument to `Object.keys()`, the
return value is an `Array` containing all of the keys at the top level of the
`Object`:

```js
const wednesdayMenu = {
  cheesePlate: {
    soft: 'Brie',
    semiSoft: 'Fontina',
    hard: 'Provolone'
  },
  fries: 'Sweet potato',
  salad: 'Southwestern'
};

Object.keys(wednesdayMenu);
// => ["cheesePlate", "fries", "salad"]
```

Notice that it didn't pick up the keys in the nested `cheesePlate` `Object` — just
the keys from the properties declared at the top level within `wednesdayMenu`.

***NOTE***: The sequence in which keys are ordered in the returned `Array` is not
consistent across browsers and should not be relied upon. All of the `Object`'s
keys will be in the `Array`, but you can't count on `keyA` always being at
index `0` of the `Array` and `keyB` always being at index `1`.

TODO: I don't feel like `.keys` is explained very well in the proposed problem above. Get answer.

## 5. Remove a property from an `Object`

Uh oh, we ran out of Southwestern dressing, so we have to take the salad off the
menu. In JavaScript, that's as easy as:

```js
const wednesdayMenu = {
  cheesePlate: {
    soft: 'Brie',
    semiSoft: 'Fontina',
    hard: 'Provolone'
  },
  fries: 'Sweet potato',
  salad: 'Southwestern'
};

delete wednesdayMenu.salad;
// => true

wednesdayMenu;
// => { cheesePlate: { soft: "Brie", semiSoft: "Fontina", hard: "Provolone" }, fries: "Sweet potato" }
```

We pass the property that we'd like to remove to the `delete` operator, and
JavaScript takes care of the rest. Poof! No more `salad` property on the
`wednesdayMenu` `Object`.

## 6. Identify the Relationship Between Arrays and Objects

Think back to the early lesson on data types in JavaScript. We listed off seven
types into which all data falls: numbers, strings, booleans, symbols, `Object`s,
`null`, and `undefined`. Notice anything missing? Arrays!

Why isn't an `Array` a fundamental data type in JavaScript? The answer is that
**it's actually a special type of `Object`**. Yes, that's right: ***`Array`s are
`Object`s***.

In fact, _everything_ we just learned how to do to `Object`s can also be done to
`Array`s because `Array`s **are** `Object`s.

Just
remember these simple guidelines about Arrays as special objects, and you'll be just fine:

- **For accessing elements in an `Array`, always use integers**.
- **Be wary of setting `Object`-style properties on an `Array`**. There's rarely any reason to, and it's usually more trouble than it's worth.
- **Remember that all `Object` keys, including `Array` indexes, are strings**. This will really come into play when we learn how to iterate over `Object`s, so keep it in the back of your mind.