# [Sending Data with Fetch Lab](https://learn.co/tracks/online-software-engineering-structured/front-end-web-programming/communication-with-the-server/sending-data-with-fetch-lab)

## Introduction

Our focus this lesson will be to learning how to send data using `fetch()`.

## 1. Use `fetch()` to send data to a remote host

Sending a POST request with `fetch()` is more complicated than what we've seen
up to this point. It still takes a `String` representing the desintation URL as
the first argument, as always. But as we will see below, `fetch()` can also take
a JavaScript `Object` (`{}`) as the _second_ argument. This `Object` can be
given certain [properties][p] with certain values in order to change `fetch()`'s
default behavior.

```js
fetch(destinationURL, configurationObject);
```

The `configurationObject` contains three core components that are needed for
standard POST requests.

### Add the HTTP Verb

So far, comparing to an HTML form, we've only got the destination URL
('http://localhost:3000/dogs' in this case). The next thing we need is to
include the HTTP verb. By default, the verb is GET, which is why we can send
simple GET requests with _only_ a destination URL. To tell `fetch()` that this
is a POST request, we need to add a `method` key to our `configurationObject`:

```js
configurationObject = {
  method: "POST"
};
```

### Add Headers

The second piece we need to include is some _metadata_ about the actual data we
want to send. This metadata is in the form of [_headers_][headers]. Headers are
sent just ahead of the actual data payload of our POST request. They contain
information about the data being sent.

One very common header is [`"Content-Type"`][content-type]. `"Content-Type"` is
used to indicate what format the data being sent is in. With JavaScript's
`fetch()`, [JSON][json] is the most common format we will be using. We want to
make sure that the destination of our POST request knows this. To do this, we'll
include the `"Content-Type"` header:

```js
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json"
  }
};
```

Each individual header is stored as a key/value pair inside an object. This
object is assigned to the `headers` key as seen above.

When sending data, the server at the destination URL will send back a response,
often including data that the sender of the `fetch()` request might find useful.
Just like `"Content-Type"` tells the destination server what type of data we're
sending, it is also good practice to tell the server what data format we
_accept_ in return.

To do this, we add a second header, [`"Accept"`][accept], and assign it to
`"application/json"` as well:

```js
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  }
};
```

There are many other [headers][headers] available for particular uses. Some are
used to send credentials or user authentication keys. Others are used to send
cookies containing user info. `"Content-Type"` and `"Accept"` are two that we'll
see the most throughout the remainder of this course.

Servers may reject requests without the specific headers the server is
configured to expect.

### Add Data

We now have the destination URL, our HTTP verb, and headers that include
information about the data we're sending. The last thing to add is the _data_
itself.

Data being sent in `fetch()` must be stored in the `body` of the
`configurationObject`:

```js
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: /* Your data goes here */
};
```

There is a catch here to be aware of - when data is exchanged between a client
(your browser, for instance), and a server, the data is sent as _text_. Whatever
data we're assigning to the `body` of our request needs to be a string.

#### Use `JSON.stringify()` to Convert Objects to Strings

When sending data using `fetch()`, we often send multiple pieces of information
in one request. In our code, we often organize this information using
objects. Consider the following object, for instance:

```js
{
  dogName: "Byron",
  dogBreed: "Poodle"
}
```

This object contains two related pieces of information, a dog's name and breed.
Let's say we want to send the data in this object to a server. We can't simply
assign it to `body`, as it isn't a string. Instead, we convert it to JSON.
The object above, converted to JSON would look like this:

```json
"{"dogName":"Byron","dogBreed":"Poodle"}"
```

Here, using JSON has enabled us to preserve the key/value pairs of our object
within the string. When sent to a server, the server will be able to take this
string and convert it back into key/value pairs in whatever language the server
is written in.

Fortunately, JavaScript comes with a built in method for converting objects to
strings, `JSON.stringify()`. By passing an object in, `JSON.stringify()` will
return a string, formatted and ready to send in our request:

```js
configurationObject = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify({
    dogName: "Byron",
    dogBreed: "Poodle"
  })
};
```

## Send the POST Request

We've got all the pieces we need. Putting it all together, we get:

```js
fetch("http://localhost:3000/dogs", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify({
    dogName: "Byron",
    dogBreed: "Poodle"
  })
});
```

With the JSON server running, if you open up `sample_form.html` or `index.html`,
you can use the above to successfully send a POST request and persist data to
`db.json`.

Obviously, we don't have to define everything inside of one anonymous `Object`.
We could also write (they're exactly the same!):

```js
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

let configObj = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj);
```

**Note**: As a security precaution, most modern websites block the ability to
use `fetch()` in console while on their website, so if you are testing out
code in browser, make sure to be on a page like `index.html` or
`sample_form.html`.

## 2. Handle the response from a successful request

Just like when we use `fetch()` to send GET requests, we have to handle
responses to `fetch()`. As mentioned before, servers will send a
[Response][response] that might include useful information. To access this
information, we use a series of calls to `then()` which are
given function _callbacks_.

Building on the previous implementation we might write the following:

```js
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

let configObj = {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj)
  .then(function(response) {
    return response.json();
  })
  .then(function(object) {
    console.log(object);
  });
```

Notice that the first `then()` is passed a callback function that takes in
`response` as an argument. This is a [`Response`][response] object, representing
what the destination server sent back to us. This object has a built in method,
`json()`, that converts the _body_ of the response from JSON to a plain old
JavaScript object. The result of `json()` is returned and made available in the
_second_ `then()`. In this example, whatever `response.json()` returns will be
logged in `console.log(object)`.

Sending the example above to our JSON server, once the request is successfully
resolved, we would see the following log:

```js
{dogName: "Byron", dogBreed: "Poodle", id: 6} // Your ID will vary depending
```

The JSON server is sending back the data we sent, along with a new piece of
data, an `id`, created by the server.

## 3. Handle errors from an unsuccessful request

When something goes wrong in a `fetch()` request, JavaScript will look down the
chain of `.then()` calls for something very similar to a `then()` called a
`catch()`.

When something goes wrong in a `fetch()`, the next `catch()` is called so that
error work can be performed. Say for instance, we forgot to add the HTTP verb to
our POST request, and the `fetch()` defaults to GET. By including a `catch()`
statement, JavaScript doesn't fail silently:

```js
let formData = {
  dogName: "Byron",
  dogBreed: "Poodle"
};

// method: "POST" is missing from the object below
let configObj = {
  headers: {
    "Content-Type": "application/json",
    "Accept": "application/json"
  },
  body: JSON.stringify(formData)
};

fetch("http://localhost:3000/dogs", configObj)
  .then(function(response) {
    return response.json();
  })
  .then(function(object) {
    console.log(object);
  })
  .catch(function(error) {
    alert("Bad things! Ragnarők!");
    console.log(error.message);
  });
```

Sent to our JSON server from a page like `index.html`, we would receive an
alert window pop-up and a logged message:

```text
Failed to execute 'fetch' on 'Window': Request with GET/HEAD method cannot have body.
```

While `catch()` may not stop _all_ silent errors, it is useful to have as a way
to gracefully handle unexpected results. We can use it, for instance, to display
a message in the DOM for a user, rather than leave them with nothing.

[json-server]: https://github.com/typicode/json-server
[p]: https://developer.mozilla.org/en-US/docs/Web/API/WindowOrWorkerGlobalScope/fetch#Parameters
[json]: https://www.json.org/
[headers]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers
[content-type]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type
[accept]: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept
[jsonstringify]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
[jsonobject]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON
