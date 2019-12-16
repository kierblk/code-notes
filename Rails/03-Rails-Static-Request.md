# [Rails Static Request (Lab)](https://github.com/saramccombs/rails-static-request-readme-online-web-pt-081219)

## Routing

How does your application know what view to render to users? This is where routing comes in. 

As a framework, Rails has a comprehensive routing system for both dynamic and static pages. 

Below are the differences between a static and dynamic route:

- **Static route** - A static route will render a view that does not change. Typically, you will not send parameters to it. Examples would be a site's about or contact pages.

- **Dynamic route** - Dynamic routes are pages that accept parameters and render different content based on those parameters. An example would be a blog's post page that contains a specific article.

### How HTTP Works at a High Level

The flow that takes place when a user attempts to go to a page on a Rails application:

1. A URL is entered into the browser; this is the HTTP request

2. That request is sent to the server where the application's router interprets the request and sends a message to the controller mapped to that route

3. The controller communicates with the view file mapped to the controller method

4. The server returns that HTTP response, which contains the view page that can be viewed in the browser

## Implementing a Static Route

```ruby
get 'about', to: 'static#about'
```

Let's look at the components that make up this route code:

- The HTTP verb - in this case we're using the `get` HTTP verb.

- The path - `'about'` represents the path in the URL bar that the route will be mapped to.

- The controller action - `'static#about'` tells the Rails routing system that this route should be passed through the `static` controller's `about` action. If the term `action` sounds foreign, actions are just Ruby speak for a method in a controller. So in the `StaticController` will be a method called `about` that gets called when a user goes to `/about`.

>NOTE: As long as your changes are within the app directory, you can keep the server going; only code changes outside of the app directory require stopping and starting the Rails server.

It's important to understand the difference between explicit and implicit rendering for the views:

- **Explicit rendering** - for explicit rendering, Rails lets you dictate which view file you want to have the controller action mapped to.

```ruby
def about
  render "some_page"
end
```

- **Implicit rendering** - for implicit rendering, Rails follows a standard convention that automatically looks for the view file with the same name as the controller action.

```ruby
def about
end

# And this empty method will render the `about.html.erb` view
```

Whoa! How is an empty method generating the same behavior as when we were calling the view template directly?

This follows along with the popular 'convention over configuration' pattern that Rails utilizes. This means that the Rails core team has built out a number of standardized processes, such as implicit view rendering to help make development life a little easier. 

It's not some kind of black code magic; behind the scenes, Rails has a large number of complex processes that make things like implicit view rendering work properly.

**So is explicit or implicit better?**

Typically, you will find that you want to utilize the **implicit** workflow in your day to day coding practice. The rationale is quite practical. Imagine that you are taking over a legacy Rails project. As you are getting acclimated to the code, would you prefer that the previous dev followed a standard naming process, or would you rather be forced to look through each controller to see how the controller actions were mapped to the views? 

Rails has always had the goal of making the development process as efficient as possible, which is why it is typically best to follow these types of implicit procedures. 

With that being said, it is important to understand how the views are mapped to the controller, which is why we also walked through the explicit process.