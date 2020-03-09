# [JS Event Listening](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/recognizing-javascript-events/javascript-event-listening)

## Resources

- [MDN - Web Events](https://developer.mozilla.org/en-US/docs/Web/Events)
- [StackOverflow - Bubbling and Capturing][stackoverflow]
- [QuirksMode - Event order][quirks]

[stackoverflow]: http://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing
[quirks]: http://www.quirksmode.org/js/events_order.html

## Learning Goals

- Demonstrate triggering event listeners on DOM nodes with `addEventListener()`

## Demonstrate Defining Event Listeners on DOM Nodes with `addEventListener()`

`addEventListener()` takes two arguments:

1. the name of the event
2. a _callback function_ to "handle" the event

Take a look at `index.html` in the browser. When you click in the `<input>`
area, nothing happens. Now let's set up some _event handling_.

Start by adding an event listener for the `click` event on the `input#input`
element in `index.html`.

```js
  // The node that will be doing the listening is
  // stored in the input constant
  const input = document.getElementById('input');

  // We are invoking addEventListener on the node
  // that will be doing the listening
  // The first argument 'click' is the event name we are
  // listening for.
  // The second argument is the callback function. The
  // work that will be executed when the node "hears"
  // the event specified.
  input.addEventListener('click', function(event) {
    alert('I was clicked!');
  });
```