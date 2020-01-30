# [Rails Routing and Nested Resources](https://github.com/saramccombs/routing-nested-resources-reading-online-web-pt-081219)

## Objectives

1. Understand the value of nested routes
2. Create nested routes
3. Understand how nested resource URL helpers are named

## Lesson

We're going to keep working on our blog application, augmenting it to filter posts by author in a more user-friendly and RESTful way.

### URL As Data

You've encountered REST already, but, just to review, it stands for REpresentational State Transfer and encapsulates a way of structuring a URL so that access to specific resources is predictable and standardized.

In practice, that means that, if we type `rails s` and run our blog app, browsing to `/posts` will show us the index of all `Post` objects. And if we want to view a specific `Author`, we can guess the URL for that (as long as we know the author's `id`) by going to `/authors/:id`.

**Top-tip:** the `/:id` notation above represents a *dynamic* route segment, which we've touched on before and will be seeing more of in this reading.

Why do we care?

When we added the filter button to our blog, we could filter by a certain author to see that author's posts, but the URL looked something like this:

`http://localhost:3000/posts?utf8=%E2%9C%93&author=1&date=&commit=Filter`

