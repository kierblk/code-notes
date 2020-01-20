# [Rails - Validations with `form_tag`](https://github.com/saramccombs/validations-with-form_tag-rails)

Now that we've learned to handle the server side of validations, we need to
take care of the client side.

At this point, we'll be in step three of the following flow:

1. User fills out the form and hits "Submit", transmitting the form data via
   a POST request.
2. The controller sees that validations have failed, and re-renders the form.
3. **The view displays the errors to the user**.

# Pre-Filling Form Values

No one likes re-doing work. First, let's make sure we know how to pre-fill
forms with the user's input so they don't have to type everything all over
again.

There are two ways to pre-fill forms in Rails: `form_tag` and `form_for`.
`form_for` is _very_ heavy on Rails magic and continues to baffle scientists
to this day, so we'll be going over `form_tag` first.

Let's start with a vanilla form (no pre-filled values yet), using the
[FormTagHelper][form_tag_helper]:

[form_tag_helper]: http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html

```erb
<!-- app/views/people/new.html.erb //-->

<%= form_tag("/people") do %>
  Name: <%= text_field_tag "name" %><br>
  Email: <%= text_field_tag "email" %>
  <%= submit_tag "Create Person" %>
<% end %>
```

Here's what the HTML output will look like:

```html
<form action="/people" accept-charset="UTF-8" method="post">
  <input name="utf8" type="hidden" value="&#x2713;" />
  <input type="hidden" name="authenticity_token" value="TKTzvQF+atT/XHG/7h48xKVdXvILdiPj83XQhn2mWBNNhvv0Oh5YfAl2LM3DlHsQjbMOFVsYEyOwj+rPaSk3Bw==" />
  Name: <input type="text" name="name" id="name" /><br />
  Email: <input type="text" name="email" id="email" />
  <input type="submit" name="commit" value="Create Person" />
</form>
```

We're working with this `Person` model:

```ruby
# app/models/person.rb

class Person < ActiveRecord::Base
  validates :name, format: { without: /[0-9]/, message: "does not allow numbers" }
  validates :email, uniqueness: true
end
```

This means validation will fail if we put numbers into the "Name" field, and
the form will be re-rendered with the invalid `@person` object available.

Remember that our `create` action now looks like this:

```ruby
# app/controllers/people_controller.rb

  def create
    @person = Person.new(person_params)

    if @person.valid?
      @person.save
      redirect_to person_path(@person)
    else
      # re-render the :new template WITHOUT throwing away the invalid @person
      render :new
    end
  end
```

With this in mind, we can use the invalid `@person` object to "re-fill" the
usually-empty `new` form with the user's invalid entries. This way they don't
have to re-type anything.

(You wouldn't _always_ want to do this –– for example, with credit card numbers ––
because you want to minimize the amount of times sensitive information travels
back and forth over the internet.)

Now, let's plug the information back into the form:

```erb
<!-- app/views/people/new.html.erb //-->

<%= form_tag "/people" do %>
  Name: <%= text_field_tag "name", @person.name %><br>
  Email: <%= text_field_tag "email", @person.email %>
  <%= submit_tag "Create Person" %>
<% end %>
```

[text_field_tag]: http://api.rubyonrails.org/classes/ActionView/Helpers/FormTagHelper.html#method-i-text_field_tag

As you can see from the [docs][text_field_tag], the second argument to
`text_field_tag`, as with most form tag helpers, is the "default" value.
The HTML for the two field inputs used to look like this:

```html
Name: <input type="text" name="name" id="name" /><br>
Email: <input type="text" name="email" id="email" />
```

But now it will look like this:

```html
Name: <input type="text" name="name" id="name" value="Jane Developer" /><br />
Email: <input type="text" name="email" id="email" value="jane@developers.fake" />
```

When the browser renders those inputs, they'll be pre-filled with the data in
their `value` attributes.

This is the same technique used to create `edit`/`update` forms.

We can also use the **same** form code for empty _and_ pre-filled forms
because `@person = Person.new` will create an empty model object whose
attributes are all `nil`.

# Displaying All Errors With `errors.full_messages`

When a model fails validation, its `errors` attribute is filled with
information about what went wrong. Rails creates an
[ActiveModel::Errors][activemodel_errors] object to carry this information.

[activemodel_errors]: http://api.rubyonrails.org/classes/ActiveModel/Errors.html

The simplest way to show errors is to just spit them all out at the top of the
form by iterating over `@person.errors.full_messages`. But first, we'll have to
check whether there are errors to display with `@person.errors.any?`.

```erb
<% if @person.errors.any? %>
  <div id="error_explanation">
    <h2>There were some errors:</h2>
    <ul>
      <% @person.errors.full_messages.each do |message| %>
        <li><%= message %></li>
      <% end %>
    </ul>
  </div>
<% end %>
```

If the model has two errors, there will be two items in `full_messages`, which
could result in the following HTML:

```html
<div id="error_explanation">
  <h2>There were some errors:</h2>
  <ul>
    <li>Name does not allow numbers</li>
    <li>Email is already taken</li>
  </ul>
</ul>
```

This is nice, but it's not very helpful from a user interface standpoint. It
would be much better if the incorrect fields themselves were highlighted
somehow.

# Displaying Pre-Field Errors With `errors[]`

`ActiveModel::Errors` has much more than just a list of
`full_message` error strings. It can also be used to access field-specific
errors by interacting with it like a hash. If the field has errors, they will
be returned in an array of strings:

```ruby
@person.errors[:name] #=> ["does not allow numbers"]
@person.errors[:email] #=> []
```

With this in mind, we can conditionally "error-ify" each field in the form,
targeting the divs containing each field:

```erb
<div class="field">
  <%= label_tag "name", "Name" %>
  <%= text_field_tag "name", @person.name %>
</div>
```

Rails will add a class if there are errors, but you can manually do so like this:

```erb
<div class="field<%= ' field_with_errors' if @person.errors[:name].any? %>">
  <%= label_tag "name", "Name" %>
  <%= text_field_tag "name", @person.name %>
</div>
```

You can override `ActionView::Base.field_error_proc` to change it to something
that suits your UI. It's currently defined as this within `ActionView::Base:`.

**Note:** There is a deliberate space added in `' field_with_errors'` in the
example above. If `@person.errors[:name].any?` validates to true, the goal here
is to produce two class names separated by a space (`class=field
field_with_errors`). Without the added space, we would get
`class=fieldfield_with_errors` instead!

# The Whole Picture

By now, our full form has grown quite a bit:

```erb
<%= form_tag("/people") do %>
  <% if @person.errors.any? %>
    <div id="error_explanation">
      <h2>There were some errors:</h2>
      <ul>
        <% @person.errors.full_messages.each do |message| %>
          <li><%= message %></li>
        <% end %>
      </ul>
    </div>
  <% end %>


  <div class="field<%= ' field_with_errors' if @person.errors[:name].any? %>">
    <%= label_tag "name", "Name" %>
    <%= text_field_tag "name", @person.name %>
  </div>

  <div class="field<%= ' field_with_errors' if @person.errors[:email].any? %>">
    <%= label_tag "email", "Email" %>
    <%= text_field_tag "email", @person.email %>
  </div>

  <%= submit_tag "Create" %>
<% end %>
```

Notice that some whitespace has been added for "breathing room" and increased
readability. Additionally, indentation has been very carefully maintained.
