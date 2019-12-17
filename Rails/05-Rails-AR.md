# Rails and Active Record

Active Record is the built-in ORM that Rails utilizes to manage the model aspects of an application. What is an ORM? An ORM is an Object Relational Mapping system, essentially this is the module that enables your application to manage data in a method driven structure. This means that you are able to run queries, add records, and perform all of the traditional database processes by leveraging methods as opposed to writing SQL manually.

```sql
SELECT * FROM posts
```

Compared with leveraging Active Record:

```ruby
Post.all
```

By using Active Record, you are also able to perform advanced query tasks, such as method chaining and scoping, which typically require less code and make for a more readable query.

## Active Record Models

**So if we have a database table, why do we need a model file?**

By using model files, we are able to create an organized layer of abstraction for our data. 

An important thing to remember is that at the end of the day the model file is a Ruby class. 

It will typically inherit from the `ActiveRecord::Base` class, which
means that it has access to a number of methods that assist in working with the database.

However, you can treat it like a regular Ruby class, allowing you to
create methods, data attributes, and everything else that you would want to do in a class file.

A typical model file will contain code such as but not limited to the following:

- Custom scopes
- Model instance methods
- Default settings for database columns
- Validations
- Model-to-model relationships
- Callbacks
- Custom algorithms
