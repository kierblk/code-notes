# Sinatra User Authentication

Using sessions!

## Logging In

Action of logging in is the simple action of storing a user's ID in the session hash.

### Basic User Flow

1. User visits the login page, fills out the form with their email and password. Submit button will POST the data to the controller route.
2. The controller route accesses the users email and password from the params hash. That info is used to find the appropriate user from the database with a line such as `User.find_by(email: params[:email], password: params["password])`. Then, that user's ID is stored as the value of `session[:user_id]`.
3. As a result, we can introspect onthe session hash in **any other controller** and grab the current user by matching up a user ID with the value in `session[:user_id]`. This means that for the duration of the session, the app will know who the current user is on every page. 

## Logging Out

Conceptually, it means we are terminating the session.

Physically, this is the action of clearing all the data, including the user's ID, fro the session hash.

Ruby method: `#clear`

## User Registration

A new user submits their information via a form.

When that form gets submitted, a POST request is sent to a route defined in the controller. This route will have code that does the following:

1. Gets the new user's name, email, and password from the params hash.
2. Uses that information to create and save a new instance of `User`, for example: `User.create(name: params[:name], email: params[:email], password: params[:password])`.
3. Signs the user in once they have completed the sign-up process. It would be annoying if you had to create an account and *THEN* sign in immediately afterwards. So in the same controller route in which we create a new user, we set the `session[:user_id]` to the new user's ID, effectively logging them in.
4. Finally, we redirect the user to somewhere else, such as their personal homepage or dashboard.
