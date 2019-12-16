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

