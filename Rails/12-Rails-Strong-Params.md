# [Rails Strong Params](https://github.com/learn-co-students/strong-params-basics-online-web-pt-081219)

## What are strong params?

In short, this is how you whitelist the parameters that are permitted to be sent to the database from a form.

## Why Strong Params?

Strong params prevent access to certain parameters and allow access to those that are whitelisted.`

## Code Implementation

**FYI** Forbidden Attributes Error --> Rails needs to be told what parameters are allowed to be submitted through the form to the database. The default is to let NOTHING through.

```ruby
    # app/controllers/posts_controller.rb
     
    def create
      @post = Post.new(params.require(:post).permit(:title, :description))
      @post.save
      redirect_to post_path(@post)
    end
     
    def update
      @post = Post.find(params[:id])
      @post.update(params.require(:post).permit(:title))
      redirect_to post_path(@post)
    end
```

## Permit vs Require

The `#require` method is the most restrictive. It means that the params that get passed in **must** contain a key called "post" (using the above code as an example).

If this key is not included then it fails and the user gets an error.

The `#permit` method is a bit looser. It means that the params hash **may** have whatever keys are in it.

So, in the above code example, the `create` action may have the `:title` and `:description` keys. If it doesn't have one of those keys, its no problem: the hash just won't accept any other keys.

## DRYing up Strong Params

A standard CRUD setup will have you utilizing the same strong params within multiple actions. We can abstract and DRY this code with a strong params method. In this example, `post_params`.

```ruby
    # app/controllers/posts_controller.rb
     
    def create
      @post = Post.new(post_params)
      @post.save
      redirect_to post_path(@post)
    end
     
    def update
      @post = Post.find(params[:id])
      @post.update(post_params)
      redirect_to post_path(@post)
    end
     
    private
     
    def post_params
      params.require(:post).permit(:title, :description)
    end
```

What about situations where we **DONT** want access to all attributes?

We make sure we meet that need/requirement with a slightly fancy splat:

```ruby
    # app/controllers/posts_controller.rb
     
    def create
      @post = Post.new(post_params(:title, :description))
      @post.save
      redirect_to post_path(@post)
    end
     
    def update
      @post = Post.find(params[:id])
      @post.update(post_params(:title))
      redirect_to post_path(@post)
    end
     
    private
     
     
    # We pass the permitted fields in as *args;
    # this keeps `post_params` pretty dry while
    # still allowing slightly different behavior
    # depending on the controller action. This
    # should come after the other methods
     
    def post_params(*args)
      params.require(:post).permit(*args)
    end
```