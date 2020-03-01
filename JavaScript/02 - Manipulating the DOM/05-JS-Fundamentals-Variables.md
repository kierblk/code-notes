# [JS Fundamentals: Variables](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/js-fundamentals-variables)

## Resources

  1. [MDN - Language basics crash course: Variables](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/JavaScript_basics#Variables)
  2. [Valid JS variable names in ECMAScript6](https://mathiasbynens.be/notes/javascript-identifiers-es6)
  3. [MDN - `var`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var)
  4. [MDN - `let`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
  5. [MDN - `const`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
  6. [JS ES6+: `var`, `let`, or `const`?](https://medium.com/javascript-scene/javascript-es6-var-let-or-const-ba58b8dcde75)

## Learning Goals

  ### 1. Define a variable

  "Saving" to a variable allows us to _save_ a result so we can use it again later.

  Storing calculations to _temporary_ storage places is the heart of making efficient programs.

  A variable is a container in which we can store values for later retreival.

  ### 2. Name variables in JavaScript

  Variable names in JS can sometimes be complicated, but if you follow these 3 rules then you'll be fine:

  1. Start every variable with a lowercase letter. Variable names starting with a number are not valid.
  2. Don't use spaces, camelCaseYourVariableNames instead of snake_casing_them.
  3. Don't use JS [reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Reserved_keywords_as_of_ECMAScript_2015) or [future reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Future_reserved_keywords).

  >Case matters. javaScript, javascript, JavaScript, and JAVASCRIPT are four different variables.

  ### 3. Initialize variables in JavaScript

  The `var` reserved word is the classic way to declare a variable. It's been around since the inception of JS and its what you will encounter in any pre-ES2015 code.

  Creating new variables in JS is really a two-step process. First we declare the variable:

  ```JavaScript
  var pi;
  //=> undefined
  ```

  The JS engine sets aside a chunk of memory to store the declared variable, then we can assign the new variable a value.

  ```JavaScript
  pi = 3.14159;
  ///=> 3.14159
  ```

  But we can package both the initialization steps (declaration and assignment) into a single line of code:

  ```JavaScript
  var pi = 3.14159;
  ///=> undefinded
  ```

  #### Multi-variable assignment

  We can streamline this:

  ```JavaScript
    var a = 5;
    var b = 2;
    var c = 3;
    var d = {};
    var e = [];
  ```

  into:

  ```JavaScript
    var a = 5,
      b = 2,
      c = 3,
      d = {},
      e = [];
  ```

  Which can be converted into:

  ```JavaScript
    var a = 5, b = 2, c = 3, d = {}, e = [];
  ```

  #### Reassigning Variable Values

  Changing the value of a variable in JS works as follows:

  ```JavaScript
    var pi = 3.14159;
    pi;
    //=> 3.14159
    pi = 3.14;
    pi;
    //=> 3.14;
  ```

  #### Variable Values

  Upon declaration, all variables are automatically assigned the value of `undefined`. It's only after we assign a new value that the variable will contain something other than `undefined`.

  We can use the `typeof` operator to check the data type of the value currently stored in a variable.

  ```JavaScript
    var language;
    //=> undefined
    
    typeof language;
    //=> "undefined"
    
    language = "JavaScript";
    //=> "JavaScript"
    
    typeof language;
    //=> "string"
  ```

  >Top Tip: When writing JavaScript code, it's good practice to never set a variable equal to undefined. Variables will be undefined until we explicitly assign a value, so encountering an undefined variable is a strong signal that the variable was declared but not assigned prior to the reference. That's valuable information that we can use while debugging, and it comes at no additional cost to us.

  ### 4. Identify when to use const, let, and var for declaring variables

  Because `var` is everywhere in legacy code (and StackOverflow posts) it's important that we learn it. However, as alluded to earlier, there is almost no reason to use `var` with the features JS post 2015.

  `var` comes with a considrable amount of "baggage" in the form of scope issues and allows developers to play a little too fast and loose with variable declarations.

  #### `let` & `const`

  ES2015 introduced two new ways to ceate variables: `let` and `const`. 
  
  Both solve all of `var`'s scope issues. 
  
  Both will throw an error if you try to declare the same variable a second time.

```JavaScript
  let pi = 3.14159;
  //=> undefined
    
  let pi = "the ratio between a circle's circumference and diameter";
  //=> Uncaught SyntaxError: Identifier 'pi' has already been declared
```

Just like with `var`, we can reassign a variable declared with `let`.

```JavaScript
  let pi = 3.14159;
  //=> undefined
    
  pi = "the ratio between a circle's circumference and diameter";
  //=> "the ratio between a circle's circumference and diameter"
    
  typeof pi;
  //=> "string"
```

Using `let` instead of `var` will help you avoid silly errors like declaring the sa,e variable at two different places within your code, but there's an even better option to use as your default: `const`.

Declaring a variable with the `const` reserved word means that not only can it not be redeclared but it also **cannot be reassigned**.

This is a good thing for 3 reasons:

1. When we assign a primitive value (any type of data except an object) to a variable declared with `const`, we know that variable will _always_ contain the same value.

2. When we assign an object to a variable declared with `const`, we know that variable will _always_ point to the same object. 

3. When another developer looks at our code and sees a `const` declaration, they immediately know that variable points to the same object or has the same value eery time it's refernced in the program.

For variables declared with `let` or `var`, the developer cannot be so sure and will have to keep track of how those variables change throughout the program.

The extra information provided by `const` is valuable, and it comes at no extra cost.

```JavaScript
  const pi = 3.14159;
  //=> undefined
    
  pi = 2.71828;
  //=> Uncaught TypeError: Assignment to constant variable.
```

However, because `const` doesn't allow reassignment after the variable is initialized, we must assign a value right away:

```JavaScript
  const pi;
  //=> Uncaught SyntaxError: Missing initializer in const declaration
    
  const pi = 3.14159;
  //=> undefined
```

As your JavaScript powers increase with experience, you'll develop a more nuanced understanding of what to use where. However, for now, this is a good rule of thumb:

  * Use `var`... never.
  * Use `let`... when you know the value of a variable will change. For example, a counter variable that starts at 0 and is subsequently incremented to 1, 2, 3, and so on. In the lessons on looping and iteration in JavaScript, let will have its moment in the spotlight.
  * Use `const`... for every other variable.

Best practice is to always declare variables with `const` and then, if you later realize that the value has to change over the course of your program, circle back to change it to `let`.