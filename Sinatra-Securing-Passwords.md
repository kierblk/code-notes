# Sinatra Securing Passwords

We never want to store our users' passwords in plain text in our database. Instead, we'll run the passwords through a hashing algorithm.

A hashing algorithm manipulates data in such a way that it cannot be un-manipulated. This is to say that if someone got a hold of the hashed version of a password, they would have no way to turn it back into the original. In addition to hashing the password, we'll also add a "salt". A salt is simply a random string of characters that gets added into the hash. That way, if two of our users use the password "fido", they will end up with different hashes in our database.

We'll use an open-source gem, bcrypt, to implement this strategy.

## Helper Methods

```ruby
helpers do
	def logged_in?
		!!session[:user_id]
	end

	def current_user
		User.find(session[:user_id])
	end
end
```

## Basic Application Controller

```ruby
class ApplicationController < Sinatra::Base

	configure do
		set :views, "app/views"
		enable :sessions
		set :session_secret, "password_security"
	end

	get "/" do
		erb :index
	end

	get "/signup" do
		erb :signup
	end

	post "/signup" do
		user = User.new(:username => params[:username], :password => params[:password])
		
		if user.save
			redirect to "/login"
		else
			redirect to "/failure"
		end
	end

	get "/login" do
		erb :login
	end

	post "/login" do
		user = User.find_by(:username => params[:username])
		
		if user && user.authenticate(params[:password])
    		session[:user_id] = user.id
    		redirect "/success"
		else
    		redirect "/failure"
		end
	end

	get "/success" do
		if logged_in?
			erb :success
		else
			redirect to "/login"
		end
	end

	get "/failure" do
		erb :failure
	end

	get "/logout" do
		session.clear
		redirect to "/"
    end
end
```

## BCrypt

BCrypt will store a salted, hashed version of our users' passwords in our database in a column called `password_digest`. 

```ruby
class CreateUsers < ActiveRecord::Migration[5.1]
  def change
    create_table :users do |t|
      t.string :username
      t.string :password_digest
    end
  end
```

## ActiveRecord's `has_secure_password`

This ActiveRecord macro gives us access to a few new methods. It works in conjunction with a gem called bcrypt and gives us all of those abilities in a secure way that doesn't actually store the plain text password in the database.

```ruby
class User < ActiveRecord::Base
  has_secure_password
end
```

Note that even though our database has a column called password_digest, we still access the attribute of password. This is given to us by `has_secure_password`.

Because our user has `has_secure_password`, we won't be able to save this to the database unless our user filled out the password field. Calling `user.save` will return false if the user can't be persisted.

We validate password match by using a method called `authenticate` on our `User` model. We get this method via the `has_Secure_password` macro.

## Resources

- [Video Review: Building Authentication in Sinatra](https://youtu.be/_S1s6R-_wYc)
- [BCrypt Docs](https://github.com/codahale/bcrypt-ruby)
- [ROR Guide: Has Secure Password](http://api.rubyonrails.org/classes/ActiveModel/SecurePassword/ClassMethods.html)
- [Video: BCrypt Introduction](https://youtu.be/O6cmuiTBZVs)
- [Video: Computerphile - How NOT to Store Passwords!](https://youtu.be/8ZtInClXe1Q)
