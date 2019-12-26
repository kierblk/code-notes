# [Rails Forms](https://github.com/saramccombs/rails-form_tag-readme-online-web-pt-081219)

- Allows users to submit data via form fields.
- Helpful for creating new DB records.
- Building a contact form.
- Integrating a search engine.
- Pretty much every other aspect of the application that requires user input.

When it comes to forms within Rails, you wull discover that you will have the flexibility to utilize both **built-in form helper methods** as well as **plain HTML form elements**.

## Documentation

[ROR ActionView::Helpers::FormTagHelpers](https://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html)

## Building the Form in HTML

First pass, plain HTML. Not going to focus on creating records in a DB, just the form process.

```ruby
<h3>Post Form</h3>

<form action="<%= posts_path %>" method="POST">
    <label>Post title:</label><br>
    <input type="text" id="post_title" name="post[title]"><br>
    
    <label>Post description:</label><br>
    <textarea id="post_description" name="post[description]"></textarea><br>
    
    <input type="hidden" name="authenticity_token" value="<%= form_authenticity_token %>">
    <input type="submit" value="Submit Post">
</form>

<%= params.inspect %>
```

But!! What is that "authenticity token" thing? 

One site making a request to another site via a form is the general flow of a Cross-Site Request Forgery. Rails blocks this from happening by default by requiring that a unique authenticity token be submitted with each form. This authenticity token is stored in the session and can't be hijacked by hackers: it performs a match check when the form is submitted, and it will throw an error if the token isn't there or doesn't match.

To fix this ActionController::InvalidAuthenticityToken error, we can integrate the form_authenticity_token helper into the form as a hidden field.

Here's our create method within the posts_controller:

```ruby
def create 
    Post.create(title: params[:post][:title], description: params[:post][:description])
    redirect_to posts_path
  end
```

But, let's refactor that.

## Using Form Helpers

`ActionView`, a sub-gem of Rails, provides a number of helper methods to assist with streamlining view template code. 

Specifically, we can use `ActionView` methods to improve our form using the `form_tag` and `hidden_field_tag` elements:

```ruby
<%= form_tag posts_path do %>
  <label>Post title:</label><br>
  <input type="text" id="post_title" name="post[title]"><br>
 
  <label>Post description:</label><br>
  <textarea id="post_description" name="post[description]"></textarea><br>

  <%= hidden_field_tag :authenticity_token, form_authenticity_token %>
  <input type="submit" value="Submit Post">
<% end %>
```

The `form_tag` Rails helper is smart enough to know that we want to submit the form via the `POST` method, and it automatically renders the HTML that we were writing by hand before. 

The `form_tag` method also automatically generates the necessary authenticity token, so we can remove the now-redundant `hidden_field_tag`.

becomes:

```ruby
<%= form_tag posts_path do %>
  <label>Post title:</label><br>
  <input type="text" id="post_title" name="post[title]"><br>
 
  <label>Post description:</label><br>
  <textarea id="post_description" name="post[description]"></textarea><br>

  <input type="submit" value="Submit Post">
<% end %>
```

Let's keep going with the refactoring and look at some other helpers, specifically `text_field_tag`, `text_area_tag`, and `submit_tag`. Keep in mind that Rails helpers aren't magic, they are simply helper methods.

```ruby
<%= form_tag posts_path do %>
  <label>Post title:</label><br>
  <%= text_field_tag :'post[title]' %><br>
 
  <label>Post description:</label><br>
  <%= text_area_tag :'post[description]' %><br>
 
  <%= submit_tag "Submit Post" %>
<% end %>
```
