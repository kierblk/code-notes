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

## Using `rails routes` on the command line

Running `rails routes` in the terminal within a rails project will give an output of the routes available to us within that project.

The output will look something like this:
```ruby
Prefix Verb URI Pattern          Controller#Action
 posts GET  /posts(.:format)     posts#index
  post GET  /posts/:id(.:format) posts#show
```

Let's break these four columns down, as they tell us everything that we'll need to use the route helper methods.

### Prefix Column

This column gives the prefix for the route helper methods. Int he above example, `posts` and `post` are the prefixes foe the methods that you can use throughout your applications. The two most popular method types are `_path` and `_url`. So if we want to render a link to our posts' index page, the method would be `posts_path` or `posts_url`. The difference between `_path` and `_url` is that `_path` gives the relative path and `_url` renders the full URL.

>**FYI:** If you open up the rails console, by running `rails console`, you can test these route helpers out. Run `app.posts_path` and see what the output is. You can also run `app.posts_url` and see how it prints out the full path instead of the relative path. 

**In general, it's best to use the `_path` version so that nothing breaks if your server domain changes.**

### HTTP Verb

Column 2. Defines the request type.

### URI/URL

This column shows what the path for the route will be and what parameters need to be passted to the route. In the example, the second row for the show route calls for an ID. When you pass the `:show` argument to the `resources` method, it will automatically create this route and assume that you need to pass the `id` into the URL string.

Whenever you have `id` parameters listed in the path like this, you will need to pass the route helper method an ID. For example, our show route code would look like this: `post_path(@post)`. The index route would be `post_path`.

>FYI: you can ignore the (.:format) text for now.

### Controller and Action

This column shows the controller and action with a syntax of `controller#action`.

----

One of the other nice things about utilizing route helper methods is that they create predictable names for the methods. Once you get into day-to-day Rails development, you will only need to run `rails routes` to find custom paths.

Let's imagine that you take over a legacy Rails application that was built with traditional routing conventions. If you see CRUD controllers for newsletters, students, sales, offers, and coupons, you don't have to look up the routes to know that you could call the index URLs for each resource below:

- Newsletters - `newsletters_path`
- Students - `students_path`
- Sales - `sales_path`
- Offers - `offers_path`
- Coupons - `coupons_path`

This is an example of the Rails design goal: "convention over configuration." Rails' convention is that resources are accessible through their pluralized name with `_path` tacked on. Since all Rails developers honor these conventions, Rails developers rapidly come to feel at home in other Rails developers' codebases.