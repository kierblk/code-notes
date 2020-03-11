# [JS Document Onload](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/javascript-document-onload)

## Resources

1. [DOMContentLoaded](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded)
2. [Running Your Code at the Right Time](https://www.kirupa.com/html5/running_your_code_at_the_right_time.htm)

## Introduction

An important part of working with JavaScript is ensuring that your code
runs at the right time. 

Every now and then, you may have to add some extra code to ensure your code doesn't run before the page is ready. 

There are many factors that go into determining the "right time."

There are two events that represent two important milestones in terms of page load:

1. The `DOMContentLoaded` event fires when your page's DOM is fully parsed
2. The `load` event fires when a resource and its dependent resources (CSS, JavaScript) have finished loading

### 1. Why `DOMContentLoaded` is important?

The `DOMContentLoaded` event is the browser's built-in way to indicate when a
page is loaded. It isn't possible to manipulate HTML elements that haven't
rendered yet, so trying to manipulate the DOM before the page fully loads can
potentially lead to problems.

### 2. Set up an event on `DOMContentLoaded`

As always, `addEventListener` takes a `String` with the name of the
event and a _callback function_.

```js
document.addEventListener("DOMContentLoaded", function() {
  console.log("The DOM has loaded");
});
```

If you put the above code in `index.js`, 'The DOM has loaded' will not be logged
immediately. In fact, you can confirm this yourself by putting a second
`console.log()` _outside_ of the event listener callback:

```js
document.addEventListener("DOMContentLoaded", function() {
  console.log("The DOM has loaded");
});

console.log(
  "This console.log() fires when index.js loads - before DOMContentLoaded is triggered"
);
```