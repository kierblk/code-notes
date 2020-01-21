# [Rails Testing](https://github.com/saramccombs/ruby-rails-testing)

One of the most fundamental aspects of programmer productivity is **the feedback
loop**. "Scripting" languages like Ruby and Python are great for this because
you can run your code immediately after writing it. Conversely, lower-level
languages like C must be compiled before being run.

![Two programmers swordfight from their office chairs, using "Compiling!" as an
excuse](http://imgs.xkcd.com/comics/compiling.png "Compiling!")

Rails ships with many features to save precious seconds in developer feedback
loops, but there's no two ways about it: in anything but the most trivial app,
it can be pretty complex to make sure your code is actually working correctly.

We'll learn to shorten our feedback loop with different flavors of Rails tests, combining some standard approaches suggested in the Guides
themselves with some more advanced practices that require additional dependencies (namely Capybara).

## Three Test Types

We'll be covering three types of tests:

- **Models** (RSpec)
- **Controllers** (RSpec)
- **Features** (RSpec/Capybara)

Features are the fanciest, so we'll leave them for last. They are preferred over
regular Rails "View" tests.

## RSpec

By default, Rails uses `Test::Unit` for testing, which keeps its tests in the
mysteriously-named `test/` folder.

If you're planning from the start to use RSpec instead, you can tell Rails to
skip `Test::Unit` by passing the `-T` flag to `rails new`, like so:

```
rails new cool_app -T
```

Then, you will add the gem to your Gemfile:

```ruby
gem 'rspec-rails'
```

And use the built-in generator to add a `spec` folder with the right boilerplate:

```
bundle install
bundle exec rails g rspec:install
```

This is the Rails equivalent of the usual `rspec --init`.