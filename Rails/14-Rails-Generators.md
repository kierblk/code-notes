# [Rails Generators](https://github.com/saramccombs/rails-generators-readme-online-web-pt-081219)

If you go down the list on all of the tasks necessary to build out CRUD functionality in an application, it's quite extensive. From creating database tables, configuring views, and drawing individual routes, the feature builds can be time consuming and bug prone. Wouldn't it be nice if there was a more efficient way of integrating standard features instead of having to build them manually each time?

A primary goal of the Rails team was to make it efficient to build core application functionality. The Rails system has a number of generators that will do some of the manual work for us.

As nice as it is to use the generators to save time, they also provide some additional extra benefits:

* They can setup some basic specs for an application's test suite. They won't write our complex logic tests for us, but they will provide some basic examples.

* They are setup to work the same way each time. This helps standardize your code and enables your development to be more efficient since you don't have to worry as much about bugs related to spelling, syntax errors, or anything else that can occur when writing code manually.

* They follow Rails best practices, which includes utilizing RESTful naming patterns, removing duplicate code, using partials and a number of other best of breed design patterns.

## Why not use them for everything?

Simple: great tools are only great tools if they are matched with the right task. In the same way that you should only use a chainsaw when you have a job that requires it, generators should only be used when they are needed.

In the same manner as our chainsaw example, certain generators create quite a bit of code. If that code is not going to be used, it will needlessly clutter the application code and cause confusion for future developers. 

## Rails Generate

All of the Rails generators are entered as commands into the terminal and will follow this syntax:

```ruby
rails generate <name of generator> <options> --no-test-framework
```

`--no-test-framework` is a flag that tells the generator not to create any tests for the newly-generated models, controllers, etc. When you're working on your own Rails applications, you don't need the flag — it's quite helpful for quickly stubbing out a test suite. However, it's necessary for Learn.co labs because we don't want Rails adding additional tests on top of the test suite that already comes with the lesson.

For efficiency's sake, Rails aliased the `generate` method to `g`, so the CLI command above could be shortened to:

```ruby
rails g <name of generator> <options> --no-test-framework
```

## Different types of generators

* Migrations
* Models
* Controllers
* Resources

### Migration

Only generates a migration.

```ruby
rails g migration <name of migration> <options> --no-test-framework

# Examples

rails g migration remove_published_status_from_posts published_status:string --no-test-framework

rails g migration add_post_status_to_posts post_status:boolean --no-test-framework

rails g migration change_post_status_data_type_to_posts post_status:string --no-test-framework
```

### Model

A generator type that will get used regularly. Creates a model, associated database table, and a migration to add the specified columns to the DB.

```ruby
rails g model <name of model, singular> <database column:type> --no-test-framework

# Examples

rails g model Author name:string genre:string bio:text --no-test-framework
```

### Controller

Great for static views or non-CRUD related features. This will add a controller file, routes for the declared actions, a directory folder for the associated views, a view helper method file, and some script files for this controller.

```ruby
rails g controller <name of model, plural> <actions desired> --no-test-framework

# Examples

rails g controller admin dashboard stats financials settings --no-test-framework
```

#### So why shouldn't we use controller generators in CRUD apps?

More view templates than ultimately desired will be created, routes that will no be needed will be created, as well as so many other things that will just need to be massively altered or deleted for a CRUD app.

Resource generators are recommended for CRUD functionality.

### Resource

The most powerful of all the generators. This generator creates a migration file, a database table, a model file, a controller file, a view directory, a view helper file, scripts for the controller, and a full resources call in the routes file. 

```ruby 
rails g resource <model name, singular> <database column:type> --no-test-framework

# Examples

rails g resource Account name:string payment_status:string --no-test-framework
```