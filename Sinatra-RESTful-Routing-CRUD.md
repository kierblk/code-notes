# Sinatra RESTful Routing & CRUD

### Random Notes
  
Sinatra view files are `.erb` but you are also allowed to use `.html.erb` should you want to be explicit. However, Sinatra knows to render the HTML properly within the `.erb` files. This is not Sinatra convention and may require you to add `.html` to routes to a `.html.erb` file. 

Rails, on the other hand, requires the explicit `.html.erb` file type to render properly.

Commenting ruby within an `.erb` file:
```ruby
<%#= comment for ruby code %>
<%# Also a comment for ruby code %>
```

```html
<!-- comment for HTML -->
```

### MVC: Model, View, Controller

Using a resaurant analogy, responsibilities/functions explained:
  - Model - Our kitchen, takes ingredients and turns them into "objects"
  - View - Our table, what our customers are looking at
  - Controller - Our waiter, goes between the kitchen and the table

CRUD: Create, Read, Update, Delete

## What is RESTful Routing, anyways?

Super-high level, a set of conventions for routing, for transfering data from one place to another. Allows a set of developers to better follow and undestand what other developers are intending in their code. However, there are always situations where convention can be broken. 

REST: Representational State Transfer, coined by Roy Thomas Fielding.

Routing is simply a combination of an HTTP verb along with a URI. 

| HTTP Verb |       Route      | Action |                    Used For                   |
|:---------:|:----------------:|:------:|:---------------------------------------------:|
| GET       | /models          | Index  | Index page to display all models              |
| GET       | /models/new      | New    | Displays the create model form                |
| POST      | /models          | Create | Creates one model                             |
| GET       | /models/:id      | Show   | Displays one model based on ID in URI         |
| GET       | /models/:id/edit | Edit   | Displays edit form based on ID in URI         |
| PATCH     | /models/:id      | Update | Modifies an existing model based on ID in URI |
| PUT       | /models/:id      | Update | Replaces an existing model based on ID in URI |
| DELETE    | /models/:id      | Delete | Deletes one model based on ID in URI          |

## Index Action

```ruby
get '/models' do
    @models = Model.all
end
```

## New Action

```ruby
get '/models/new' do
    erb :new
end

post '/models' do
    @model = Model.create(
        title: params[:title],
        content: params[:content]
        )
    redired to "/models/#{@model.id}"
end
```

## Show Action

```ruby
get '/model/:id' do
    @model = Model.find_by_id(params[:id])
    erb :show
end
```

## Edit / Update Action

```ruby
get '/models/:id/edit' do
    @model = Model.find_by_id(params[:id])
    erb :edit
end

patch '/models/:id' do
    @model = Model.find_by_id(params[:id])
    @model.title = params[:title]
    @model.content = params [:content]
    @model.save
    redirect to "/models/#{@model.id}"
end
```

## Delete Action

```ruby
delete '/models/:id/delete' do
    @model = Model.find_by_id(params[:id])
    @model.delete
    redirect to "/models"
end
```

## Use Rack::MethodOverride for PATCH requests and DELETE requests

We need to update out `config.ru` file to use the Sinatra middleware that allows us to send patch requests.
`use Rack::MethodOverride` needs to be placed above the mounting for the Application Controller. 

The method override middleware will intercept every request sent and received by our application.

If it finds a request with `name=_method`, it will set the request type based on what is set in the value attribute. 

```html
<form action="/models/:id/delete" method="post">
    <input type="hidden" name="_method" value="patch/delete">
    <input type="submit" value="update/delete">
</form>
```

## CRUD Visual Summary

**CREATE**
`get '/models/new'` -------------> `new.erb`
`post '/models'` <---------------- `new.erb`

**READ**
`get '/models'` -----------------> `index.erb`
`get 'models/:id'` --------------> `show.erb`

**UPDATE**
`get '/models/:id/edit'` --------> `edit.erb`
`patch '/models/:id'` <----------- `edit.erb`

**DELETE**
`get '/models/:id'` -------------> `show.erb` with delete "form button"
`post '/models/:id/delete'` <----- `show.erb` with delete "form button"