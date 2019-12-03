# Sinatra Mechanics of Sessions

A session is basically just a hash that stores data on the server and passes that data to the client as a cookie. You can access the data stored in the session in the same way you would any hash in Ruby.

## Setting Up a Session

In Sinatra, we enable sessions within the controller by adding two lines in the `configure` block:

```ruby
configure do
    enable :sessions
    set :session_secret, "secret"
end
```

>**IMPORTANT:** You should never set your session_secret by hand, and especially not to something so trivially simple as "secret"! We are doing this for the sake of demonstration this one time.

The first line of the configure block, `enable :sessions`, turns sessions on. The next line, `set :session_secret, "secret"`, is an encryption key that will be used to create a `session_id`. A `session_id` is a string of letters and numbers that is unique to a given user's session and is stored in the browser cookie. You can actually set your `session_secret` to anything that you want. Don't worry too much about understanding how the session_id works. It's just part of the mechanics behind getting a secure private session working. You probably won't ever need to interact with it.

`session_secret` is a pretty minimal security feature, but the basic idea is that setting your `:session_secret` to a word that other people don't know makes it harder for someone to create a fake `session_id` and hack into your site without signing up or signing in.

## Securing Your Session

As we mentioned at the beginning, you should not define you `session_secret` as we do in this lab. The most secure method is to use a secure number generator to generate a secret and to share that secret, via environment variables in the shell, to Sinatra.
