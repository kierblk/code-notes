# [Use Fetch](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/communication-with-the-server/use-fetch)

## Resources

- [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

## Introduction

Web users
expect sites to load quickly **and** to stay updated. Research shows that 40
percent of visitors to a website will leave if the site takes more than 3
seconds to load. Mobile users are even _less_ patient.

To solve this problem and help provide lots of other really great features, we
developed a technique called **_AJAX_**.

In AJAX we:

1. Deliver an initial, engaging page using HTML and CSS which browsers render
   _quickly_
2. _Then_ we use JavaScript to add more to the DOM, behind the scenes

AJAX relies on several technologies:

* Things called `Promise`s
* Things called `XMLHttpRequestObject`s
* A [serialization format][sf] called JSON for "JavaScript Object Notation"
* [asynchronous Input / Output][asyncIO]
* [the event loop][el]

Part of what makes AJAX complicated to learn is that to understand it
_thoroughly_, you need to understand _all_ these components. For the moment,
however, we're going to gloss over all these pieces in this lesson. It just so
happens that modern browsers have _abstracted_ all those components into a
single function called `fetch()`. While someone interviewing to be a front-end
developer will be expected to be able to explain all those components above
(which we _will_ cover later), while we're getting a hang of things, we're
going to simplify our task by using `fetch()`.

## 1. Explain how to fetch data with `fetch()`

The `fetch()` function retrieves data. It's a global _method_ on the `window`
object. That means you can simply use it with `fetch()` in DevTools.

Here's the skeleton for using it. We'll provide it again with lots of comments
so you can step through what's happening, but for a quick reference, here's
the skeleton:

```js
fetch("string representing a URL to a data source")
.then(function(response) {
  return response.json();
})
.then(function(json){
  // Use this data inside of `json` to do DOM manipulation
})
```

Let's add some in-line JavaScript comments to help us track what's going on.
Since JavaScript doesn't care about comments or whitespace, we're going to add
multi-line (`/*...*/`) comments to help explain what's going on:

```js
fetch("string representing a URL to a data source")
  /*
    The function above returns an object that represents what the data source
    sent back. It does *not* return the actual content.

    We have to call the then() method on the object that comes back. then()
    takes as its argument a function that receives the response as its argument.
    Inside of the function, we do whatever processing we need, but at the end we
    *have to return* the content that we've gotten out of the response.

    The response has some basic functions on it for the most common data types.
    The most important ones are .json() and .text().

    This callback function is usually only one line: returning the content from
    the response. What we return from this function will be used in the _next_
    then() function.
  */

  .then(function(response) {
    return response.json();
  })

  /*
    The function above returns the content from the response.
    We can use that content inside of the callback function that's
    passed in to the then() function below.
  */

  .then(function(json){
    // Use this data inside of `json` to do DOM manipulation
  })
```

## 2. Working around backwards compatibility issues

As you can see, `fetch()` provides us with a short way to fetch and work with
resources. However, `fetch()` has only recently arrived in browsers. In older
code you might see `jquery.ajax` or `$.ajax` or an object called an
`XMLHttpRequestObject`. These are distractions at this point in your education.
After working with `fetch()` you'll be able to more easily integrate these
special topics.

## 3. Identify examples of the AJAX technique on popular websites

* It allows us to pull in dynamic content. The same "framing" HTML page remains
  on screen for a cooking website. The recipe on display updates _without_ page
  load. This approach was pioneered by GMail whose nav area is swapped
  for mail content swiftly &mdash; thanks to AJAX.
* It allows us to get data from multiple sources. We could make a website that
  displays the current weather forecast and the current price of bitcoin side
  by side! This approach is used by most sites to render ads. Your content loads
  while JavaScript gets the ad to show and injects it into your page (sometimes
  AJAX can be used in a way that we don't _entirely_ like).

[sf]: https://en.wikipedia.org/wiki/Serialization
[asyncIO]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing
[el]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop