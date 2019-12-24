# [Rails Helpers](https://github.com/saramccombs/rails-url-helpers-readme-online-web-pt-081219)

Rails is meant to be flexible. As a result, there are typically a number of ways to accomplish the same goals. 

Let's review how to leverage built-in URL helper methods instead of hard coding route paths into an application (along with why this is a good idea).

## Paths vs Route Helpers

What's the difference? 

- Paths: works, slow, error prone, and if something changes it will require intervention to keep it working.

  - Example: `"/posts/#{@post.id}"`, Here you're saying: "I know exactly the GPS coordinates of my meeting, driver. Do exactly as I say."

- Route Helper: faster, dynamic in the fact that if something changes it can still route to the proper location.accordion

  - Example: `post_path(@post)`, Here you're saying: "Can you find the best way to a controller that knows how to work with this thing called a `Post` based on looking at this instance called `@post`.

**We want to use route helper methods as opposed to hard coding routes because:**

1. Route helpers are more dynamic since they are methods and not strings. This means as something changes with the route, there are many cases where the code itself won't need to be changed at all.

2. Route helper methods help clean up the view and controller code, as well as assisting with readability. (Side note: you CANNOT use these helper methods in your model files.)

3. It's more natural to be able to pass arguments into a method as opposed to using string interpolation. For example, `post_path(post, opt_in: true)` is more readable than `"posts/<%= post.id %>?opt_in=true"`.

4. Route helpers translate directly into HTML-friendly paths. Basically, if you have any weird characters within your URLs, the route helpers will convert them so they can be read properly by a browser. This includes things such as spaces or characters such as `&`, `%`, etc.