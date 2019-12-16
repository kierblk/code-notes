# Rails Introduction

TOC:
1. [Rails Application Basics](https://github.com/saramccombs/rails-application-basics-readme)

----

## Rails Application Basics

**Why use a Framework?**

A. When it comes to building a web application, while it would technically be possible to build out all the functionalities yourself, its typically a better idea to leverage a system that has already spent over a decade developing the tools necessary for getting applications built.

**What exactly _IS_ Ruby on Rails?**

A couple of things...

- A **web framework** to provides developers the tools needed to build web applications, baseline tools that provide routing, asset management, database connections, etc so developers don't have to create base functionality for each new project.

- A **Ruby Gem**, at its core ROR is simply a set of Ruby code libraries

- A **MVC Framework**, Rails takes advantage of this popular application architecture that helps developers naturally separate concerns and organize applications properly.  This setup encourages a specific set of conventions.

**What Ruby on Rails is _NOT_**

- A programming language. This is one of the most common misconceptions, ROR is not a programming language but rather a set of code libraries built in Ruby.

- A slow framework. Due to the fact that ROR is one of the most straightforward frameworks to learn, it can lead to a number of poor coding practices from beginners. However, if built properly, Rails projects can be as fast as any other framework. Furthermore, Rails service-based architecture makes it a perfect canidate for microservice applications, which can be some of the fastest and best performing applications on the web.

### Installing the Rails Gem for Local Users

```gem install rails``

### Generating a New Rails Application

```rails new blog-flash``` 

- where "blog-flash" is the name of our application.

- There are a number of naming conventions for Rails app names, typically you want to use all lower case letters seperated by "-"

### Rails File Structure Overview

Here's a breakdown of each directory:

- **app** – contains the models, views, and controllers, along with the rest of the core functionality of the application. This is the one directory where you can make a change and not have to restart the Rails server. The majority of your time will be spent working in this directory. In addition to the full MVC structure, this directory also contains non Ruby files, such as: css files, javascripts, images, fonts, etc.

- **bin** – some built-in Rails tasks that you most likely will never have to work with.

- **config** – the config directory manages a number of settings that control the default behavior, including: the environment settings, a set of modules that are initialized when the application starts, the ability to set language values, the application settings, the database settings, the application routes, and lastly the secret key base.

- **db** – within the db directory you will find the database schema file that lists the database tables, their columns, and each column’s associated data type. The db directory also contains the seeds.rb file, which lets you create some data that can be utilized in the application. This is a great way to quickly integrate data in the application without having to manually add records through a web form element. The schema file can be found at db/schema.rb.

- **lib** – while many developers could build full applications without ever entering the lib directory, you will discover that it can be incredibly helpful. The lib/tasks directory is where custom rake tasks are created. You have already used a built-in rake task when you ran the database creation and migration tasks; however, creating custom rake tasks can be very helpful and sometimes necessary. For example, a custom rake task that runs in the background, making calls to an external API and syncing the returned data into the application’s database.

- **log** – within the log directory you will discover the application logs. This can be helpful for debugging purposes, but for a production application it's often better to use an outside service since they can offer more advanced services like querying and alerts.

- **public** – this directory contains some of the custom error pages, such as 404 errors, along with the robots.txt file which will let developers control how search engines index the application on the web.

- **test** – by default Rails will install the test suite in this directory. This is where all of your specs, factories, test helpers, and test configuration files can be found. Side note: We always use RSpec, which means this directory will actually be called spec.

- **tmp** – this is where the temporary items are stored and is rarely accessed by developers.

- **vendor** – this directory has been utilized for varying purposes in the past. In Rails 4+, its main purpose is for integrating Client-side MVC frameworks, such as AngularJS.

- **Gemfile** – the Gemfile contains all of the gems that are included in the application; this is where you will place outside libraries that are utilized in the application. After any change to the Gemfile, you will need to run bundle. This will call in all of the code dependencies in the application. The Gem process can seem like a mystery to new developers, but it is important to realize that the Gems that are brought into an application are simply Ruby files that help extend the functionality of the app.

- **Gemfile.lock** – this file should not be edited. It displays all of the dependencies that each of the Gems contain along with their associated versions. Messing around with the lock file can lead to application bugs due to missing or altered Gem dependencies.

- **README.rdoc** – the readme file is an important place to document the details of the application. If the application is an open-source project, this is where you can place instructions to other developers, such as how to get the app up and running locally.

### Creating the Database

``` rake db:create```

### Starting Up the Rails Server

``` rails s```

You can verify that it's working properly in the browser by navigating to `http://localhost:3000/.`

Here you will see the 'Yay! You're on Rails!' page that ships with Rails.

In order to shutdown the server, use the keyboard combo `CTRL+C`

### Using the Rails Console

Rails console is an important tool. This gives your a direct connection to your applications ecosyste, and lets you perform tasks.

- Running DB queries
- Running application code
- Performing full CRUD tasks with the database
- Allowing you to switch between making permentant DB changes and running in a sandbox mode to test scripts out

To start up the rails console, run: `rails c`

**So why not just use IRB instead of console?** There is a very significant difference between rails console and IRB. Even though they both run Ruby code, the rails console loads the full Rails environment which provides access to rails specific methods (along with the full application DB)