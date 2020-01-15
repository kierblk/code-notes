# [Rails Edit/Update Action](https://github.com/saramccombs/rails-edit-update-action-readme-online-web-pt-081219)

There is a trend in Rails conventions where the logic for rendering a form is separate from the action that manages the database record alteration. For example:

- The `new` action in the controller simply renders the `new` form

- The `create` action is what actually handles the process of inserting the form
  data into the database

In like fashion, the `edit` and `update` actions have a similar convention:

- The `edit` action will handle rendering the `edit` form

- The `update` action will be the method that updates the database record itself

## Routes

Here's the routes for this lab:

```ruby
    get 'articles/:id/edit', to: 'articles#edit', as: :edit_article
    patch 'articles/:id', to: 'articles#update'
```

Notice we are using `patch` as our HTTP verb. 

What about PUT? PUT will actually work just fine here, but briefly, PUT is meant to be used when replacing a whole resource. 

PATCH, on the other hand, is for used for sending a set of changes to a resource.

## Actions

```ruby
    def edit
      @article = Article.find(params[:id])
    end

    def update
      @article = Article.find(params[:id])
      @article.update(title: params[:article][:title], description: params[:article][:description])
      redirect_to article_path(@article)
    end
```