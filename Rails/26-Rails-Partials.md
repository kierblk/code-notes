# Rails Partials

[Video Review: Live Lecture - Refactoring with Layouts, Partials, and Helpers](https://youtu.be/QkRafFEj1yM)

## Objectives

1. Explain why partials are used
2. Use Rails's `render` method to render a partial
3. Describe how the name of a partial turns into its filename
4. Reference partials located in an external folder

## Introduction

As you know, while coding we are generally trying to not repeat our code. If we see a repeated chunk of code in different methods, we sometimes extract that chunk of code into its own method, which we can then reference in multiple places.

We can apply a similar tool to reduce repetition in HTML. Partials are view-level files that only form one part of an HTML page. By using a partial, we can remove repeated pieces of HTML and add better organization to the code in our views.

Duplication means twice the amount of code to maintain, twice the opportunity for bugs, and two slightly different forms when our interface should be consistent.

Instead of duplicating all of that code, we just want to write it once in our partial and call it from both our edit and show views. Here's how:

First, let's create a new file in `app/views/posts/` called `_form.html.erb`. To indicate that this file is a partial (and only part of a larger view), an underscore is prefixed to the filename.

Second, let's remove the repeated code in `app/views/posts/edit.html.erb`. The file should look like this:

```erb
<h3>Post Form</h3>

<%= form_tag post_path(@post), method: "put" do %>
<% end %>
```
Note that we left in the non-duplicated code. Now, let's also remove the duplicated code in the `app/views/posts/new.html.erb` file. The file should look like this:

```erb
<%= form_tag posts_path do %>
<% end %>
```
We left the code that is unique to each view and removed the duplicated code inside the `form_tag` blocks.

So, now what? It looks like we are missing a bunch of code in our `posts/new` and `posts/edit` files. Not to worry –– that's where our partial comes in handy.

First, we'll place the duplicated code in a new file called `app/views/posts/_form.html.erb`. The file should look as follows:
```erb
<label>Post title:</label><br>
<%= text_field_tag :title, @post.title %><br>

<label>Post Description</label><br>
<%= text_area_tag :description, @post.description %><br>

<%= submit_tag "Submit Post" %>
```
Next, we need to render the code into the `posts/edit` and `posts/new` pages by placing `<%= render "form" %>` where we want the code in the partial to be rendered. Notice that, while the file name of our partial starts with an underscore, when we reference it there is no underscore.

Our `posts/new` file should now look like this:
```erb
<!-- app/views/posts/new.html.erb -->

<%= form_tag posts_path do %>
 <%= render 'form' %>
<% end %>
```

And our `posts/edit` file like this:
```erb
<!-- app/views/posts/edit.html.erb -->

<h3>Post Form</h3>

<%= form_tag post_path(@post), method: "put" do %>
  <%= render 'form' %>
<% end %>
```

And that's it –– we're all done!

A couple of things to note:
1. Notice that, even though the last line of the form (the `<% end %>` tag) is duplicated code, we didn't move it into the partial. This is because it closes the beginning of the `form_tag` block, which DOES differ from form to form. We don't want to open our `form_tag` block in one file and close it in a different file. This is a stylistic point that you will get a feel for over time.

2. We could have named the partial whatever we wanted to. The only requirements are that it start with an underscore and that references to the partial are made without the underscore. But, just like method names, it's good to make the names of our partials as commonsensical as possible.

3. We were able to reference the partial by just calling `<%= render 'form' %>`.  Notice that we didn't specify the folder that the partial lives in, such as `<%= render 'posts/form' %>`. The reason we didn't need this (even though it would have worked if we had included it) is that both the `posts/new` and `posts/edit` files are referencing a partial housed in the same folder in which they reside, `app/views/posts`. When referencing a partial from a different folder, we must include the folder name as well (e.g., `<%= render 'posts/form' %>` as opposed to `<%= render 'form' %>`).

## Rendering a partial from a different folder

We can't use the above code for rendering a partial in a different folder. This won't work because, if we don't specify the partial's parent folder, Rails assumes that the partial lives in the same folder as the view that's calling it. We need to tell Rails to go outside the folder by being explicit about the folder and file name that it should render.

Example:

```erb
<!-- app/views/posts/show.html.erb -->

<%= render 'authors/author' %>

<h1><%= @post.title %></h1>
<p><%= @post.description %></p>
```

