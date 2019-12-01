# Sinatra RESTful Routing & CRUD

### MVC: Model, View, Controller

Using a resaurant analogy, responsibilities/functions explained:
    - Model - Our kitchen, takes ingredients and turns them into "objects"
    - View - Our table, what our customers are looking at
    - Controller - Our waiter, goes between the kitchen and the table

CRUD: Create, Read, Update, Delete

### What is RESTful Routing, anyways?

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

#### Index Action

```ruby
get '/models' do
    @models = Model.all
end
```

#### New Action

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

#### Show Action

```ruby
get '/model/:id' do
    @model = Model.find_by_id(params[:id])
    erb :show
end
```

#### Edit Action

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

#### Delete Action

```ruby
delete '/models/:id/delete' do
    @model = Model.find_by_id(params[:id])
    @model.delete
    redirect to "/models"
end
```

**Use Rack::MethodOverride**

```html
<form action="/models/<%= @model.id %>/delete" method="post">
    <input type="hidden" name="_method" value="patch/delete">
    <input type="submit" value="delete">
</form>
```
