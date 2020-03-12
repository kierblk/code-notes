# [Use Fetch](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/communication-with-the-server/use-fetch)

# Resources

- [MDN Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

# Introduction

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



## 2. Working around backwards compatibility issues

## 3. Identify examples of the AJAX technique on popular websites

[sf]: https://en.wikipedia.org/wiki/Serialization
[asyncIO]: https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing
[el]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop