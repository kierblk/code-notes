# [Rails Create Action](https://github.com/saramccombs/rails-create-action-readme-online-web-pt-081219)

[Lab](https://github.com/saramccombs/rails-create-action-lab-online-web-pt-081219)

Code a `create` action — '**C**' in the '**CRUD**' life
cycle — that saves a new `Post` object and then redirects to the newly-created
post's `show` page.

```ruby
def create
  @post = Post.new
  @post.title = params[:title]
  @post.description = params[:description]
  @post.save
  redirect_to post_path(@post)
end
```

In this `create` action, we're following the convention of
redirecting to the new resource's `show` page. It stands to reason that a user
who submits a new post would then like to view the successfully-created post.
With that being said, the page flow is not set in stone, and we could've
redirected the `create` action to the `index` action just as easily.

