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

# Model Tests

These go in `spec/models`, one file per model.

Model tests use the least amount of special features, since all you really need
is the model class itself. The most common usage for model tests is to make sure
you have set up your validations correctly.

Suppose we're working with this model:

```ruby
# app/models/monster.rb

class Monster < ActiveRecord::Base
  validates :name, presence: true
  validates :size, inclusion: { in: ["tiny", "average", "like, REALLY big"] }
  validates :taxonomy, format: { with: /\A[A-Z](\.|[a-z]+) [a-z]{2,}\z/,
    message: "must include genus and species, like 'Homo sapiens'" }
end
```

## Testing for Validity

First, we'll make sure that it understands a valid Monster:

```ruby
# spec/models/monster_spec.rb

describe Monster do
  let(:attributes) do
    {
      name: "Dustwing",
      size: "tiny",
      taxonomy: "Abradacus nonexistus"
    }
  end

  it "is considered valid" do
    expect(Monster.new(attributes)).to be_valid
  end
end
```

Some questions to answer first:

### What is `let`?

If you haven't seen `let` before, it is a [standard helper method](http://www.relishapp.com/rspec/rspec-core/docs/helper-methods/let-and-let)
that takes a symbol and a block. It runs the block **once per example** in which
it is called and saves the return value in a local variable named according to
the symbol. This means you get a fresh copy in every test case.

### Why is `let` better than `before :each`?

It's more fine-grained, which means you have better control over your data. It
can be used in combination with `before` statements to set up your test data
*just right* before the examples are run.

### Why did we use `let` to make an attribute hash?

We could have put the entire `Monster.new` call inside our `let` block, but
using an attribute hash instead has some advantages:

- If we want to tweak the data first, we can just pass `attributes.merge(name:
  "Other")` while preserving the rest of the attributes.
- We can also refer to `attributes` when making assertions about what the actual
  object should look like.

It's a good balance between saving keystrokes and maintaining the flexibility of
your test data.

### Where does `be_valid` come from?

RSpec provides plenty of built-in matchers, which you can peruse in their [API
docs](http://rspec.info/documentation/3.4/rspec-expectations/frames.html#!RSpec/Matchers.html), but `be_valid` is conspicuously absent from the list.

This code uses a neat trick that RSpec refers to as "[predicate
matchers](https://www.relishapp.com/rspec/rspec-expectations/docs/built-in-matchers/predicate-matchers)", and you'll see it **a lot** in Rails testing.

In Ruby, it's conventional for methods that return `true` or `false` to be named
with a question mark at the end. These methods are called **predicate methods**,
because "predicate" is an English grammar term for the part of a sentence that
makes a statement about the subject.

As you learned earlier in this unit, Rails provides a `valid?` method that
returns `true` or `false` depending on whether the model object in question
passed its validations.

In RSpec, when you call a nonexistent matcher (such as `be_valid`), it strips
off the `be_` (`valid`), adds a question mark (`valid?`), and checks to see if
the object responds to a method by that name (`monster.valid?`).

## Testing for Validation Failure

Now, let's add some tests to make sure our validations are working in the
opposite direction:

```ruby
# spec/models/monster_spec.rb

  let(:missing_name) { attributes.except(:name) }
  let(:invalid_size) { attributes.merge(size: "not that big") }
  let(:missing_species) { attributes.merge(taxonomy: "Abradacus") }

  it "is invalid without a name" do
    expect(Monster.new(missing_name)).not_to be_valid
  end

  it "is invalid with an unusual size" do
    expect(Monster.new(invalid_size)).not_to be_valid
  end

  it "is invalid with a missing species" do
    expect(Monster.new(missing_species)).not_to be_valid
  end
```

Note that each of these `let` blocks rely on the first one, `attributes`, which
contains all of our valid attributes. `missing_name` uses the Rails hash helper
`except` to exclude the `name` key while the other two use the standard Ruby
`merge` method to overwrite valid attributes with invalid ones.

## I saw some search results using `should`. What is that?

`should` is an older RSpec syntax that has been deprecated in favor of `expect`.

## Any other RSpec features to know about?

Several RSpec features have been moved over time into the
[rspec-collection_matchers](https://github.com/rspec/rspec-collection_matchers) gem, which can make some
detailed assertions more readable.


# Controller Tests

The biggest risk in writing controller tests is redundancy: controllers exist
to connect views and models, so it's difficult to test them in isolation.

First, we'll go over **how** to write controller tests. Then, our discussion of
the **why** will bring us into the final subject, "feature tests".

```ruby
# spec/controllers/monsters_controller_spec.rb

describe MonstersController, type: :controller do
  let(:attributes) do
    {
      name: "Dustwing",
      size: "tiny",
      taxonomy: "Abradacus nonexistus"
    }
  end

  it "renders the show template" do
    monster = Monster.create!(attributes)
    get :show, id: monster.id
    expect(response).to render_template(:show)
  end

  describe "creation" do
    before { post :create, monster: attributes }
    let(:monster) { Monster.find_by(name: "Dustwing") }

    it "creates a new monster" do
      expect(monster).to_not be_nil
    end

    it "redirects to the monster's show page" do
      expect(response).to redirect_to(monster_path(monster))
    end
  end
end
```

You can use the `get` and `post` methods (along with `patch` and `delete`) to
initiate test requests on the controller. A `response` object is available to
set expectations on, such as `render_template` or `redirect_to`.

The tests above are great, especially while we're still getting used to how
controllers are wired. However, almost these exact tests could be copied for
*any* controller set up according to Rails' RESTish conventions. There's nothing
inherently wrong with that, but the redundance, along with the need to test
views, inspired the creation of a new type of test supported by Capybara known
as a "Feature Test".

# Feature Tests

**Acceptance Test:** Test that is phrased in terms of providing value to the user, can "cover too much ground" making it difficult to maintain

**Integration Test:** Test that tests more than one piece of the system at one time

**Unit Test:** Test that tests a single unit of funtionality.
* Difficult to write isolated unit tests
* Not always clear if these are useful
* Jargon heavy, extremely specific

**Feature Tests** are the goldilocks choice. They allow us to think like a user while still making intellifent assertions about how the underlying system should respond to input.

## Testing for Validation Failure

Now, let's add some tests to make sure our validations are working in the
opposite direction:

```ruby
# spec/models/monster_spec.rb

  let(:missing_name) { attributes.except(:name) }
  let(:invalid_size) { attributes.merge(size: "not that big") }
  let(:missing_species) { attributes.merge(taxonomy: "Abradacus") }

  it "is invalid without a name" do
    expect(Monster.new(missing_name)).not_to be_valid
  end

  it "is invalid with an unusual size" do
    expect(Monster.new(invalid_size)).not_to be_valid
  end

  it "is invalid with a missing species" do
    expect(Monster.new(missing_species)).not_to be_valid
  end
```

Note that each of these `let` blocks rely on the first one, `attributes`, which
contains all of our valid attributes. `missing_name` uses the Rails hash helper
`except` to exclude the `name` key while the other two use the standard Ruby
`merge` method to overwrite valid attributes with invalid ones.

## I saw some search results using `should`. What is that?

`should` is an older RSpec syntax that has been deprecated in favor of `expect`.

## Any other RSpec features to know about?

Several RSpec features have been moved over time into the
[rspec-collection_matchers](https://github.com/rspec/rspec-collection_matchers) gem, which can make some
detailed assertions more readable.


# Controller Tests

The biggest risk in writing controller tests is redundancy: controllers exist
to connect views and models, so it's difficult to test them in isolation.

First, we'll go over **how** to write controller tests. Then, our discussion of
the **why** will bring us into the final subject, "feature tests".

```ruby
# spec/controllers/monsters_controller_spec.rb

describe MonstersController, type: :controller do
  let(:attributes) do
    {
      name: "Dustwing",
      size: "tiny",
      taxonomy: "Abradacus nonexistus"
    }
  end

  it "renders the show template" do
    monster = Monster.create!(attributes)
    get :show, id: monster.id
    expect(response).to render_template(:show)
  end

  describe "creation" do
    before { post :create, monster: attributes }
    let(:monster) { Monster.find_by(name: "Dustwing") }

    it "creates a new monster" do
      expect(monster).to_not be_nil
    end

    it "redirects to the monster's show page" do
      expect(response).to redirect_to(monster_path(monster))
    end
  end
end
```

You can use the `get` and `post` methods (along with `patch` and `delete`) to
initiate test requests on the controller. A `response` object is available to
set expectations on, such as `render_template` or `redirect_to`.

The tests above are great, especially while we're still getting used to how
controllers are wired. However, almost these exact tests could be copied for
*any* controller set up according to Rails' RESTish conventions. There's nothing
inherently wrong with that, but the redundance, along with the need to test
views, inspired the creation of a new type of test supported by Capybara known
as a "Feature Test".
