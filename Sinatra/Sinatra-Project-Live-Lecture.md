# Sinatra Portfolio Project - Live Lecture Notes 12-3-19

Video Recording

## `/failure` and `/success` routes

```ruby
get '/failure' do
    @errors = [error array, error array]
    erb :failure
end
```

```html
<h1>ERROR!!</h1>
<ul>
    <% @errors.each do |error| %>
        <%= error %>
    <% end %>
</ul>
```

This @errors instance variable will contain whatever the valid error message needs to be no matter the route that failed and the failure erb will render that error without issue.

----

```ruby
get '/success' do
    erb :success
end
```

----

Ensure that the schema for the password is `:password_digest` and not `:password`.

Ensure your user model contains `has_secure_password` to get those magical active record methods.

----

Private methods for fetching the user params will help to DRY your code and keep things more secure.

```ruby
private

def user_params
    { username: params[:username], password: params[:password] }
end
```

----
```ruby
post '/login' do
    user = User.find_by(username: params[:username])
    if user && user.authenticate(params[:password])
        session[:user_id] = user_id
        redirect to "/"
    else
        @errors = ["Invalid Username"]
        erb :failure
    end
end
```

To enable sessions have this in the app controller for the login.

```ruby
configure do
    set :views, 'app/views'
    enable :sessions
    set :session_secret, "password_security"
  end
```

----

Adding to the DB

```ruby
post '/quotes' do
    quote = Quote.new(quote_params)
    if quote.save
        redirect to "/quotes"
    else
        @error = ["Could not save your quote."]
        erb :failure
    end
end
```

```ruby
private

def quote_params
    { author: params[:author], body: params[:body] }
end
```