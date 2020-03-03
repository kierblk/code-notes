# [JS Fundamentals: Calling Methods](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/manipulating-the-dom/js-fundamentals-calling-methods)

## Resources

* [JavaScript Object Methods](https://www.w3schools.com/js/js_object_methods.asp)

## Learning Goals 

### 1. Define a JavaScript Method

Let's consider the `document.querySelector` method.

This bit of code _calls_ the _method_ `querySelector`. The method is said to be "defined in" the object `document`.

_Calling_ is the same as _running_, which we do when we write:

```JavaScript
  document.querySelector(); // Notice the addition of ()
```

When we _call_ `document.querySelector()`, we provide it an [argument](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments) inside the `()`.

This method expects us to provide a CSS identifier that will help us find the node we want as an _argument_.

If the `document` object finds an `HTMLElement` in its representation of the page, it _returns_ it. Otherwise the method returns `null`.

The thing `document.querySelector()` returns is _also_ an object. It, too, has both information and methods, state and behavior, properties and methods.... This `HTMLElement` [instance](https://developer.mozilla.org/en-US/docs/Glossary/Instance) has its own methods, like `remove()`.

## Conclusion

* JavaScript methods are actions that can be performed on objects.
* Objects have many useful methods that help us modify and iterate through them.