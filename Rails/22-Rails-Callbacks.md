# [Rails Active Record Callbacks](https://github.com/saramccombs/activerecord-lifecycle-reading-online-web-pt-081219)

Now that you are integrating `ActiveRecord` into Rails, we must should note that
we can make bits of code run whenever something happens in our model: like when
it's created (but not yet saved to the database), saved to the database, or
even deleted.  Everything we cover here is called "Active Record Lifecycle
Callbacks". Many people just call them callbacks.

We write lifecycle callbacks similarly to how you use `has_many` or `validates`
and place this "hook" onto saving at the top of our model file. Since lifecycle
methods run "as if by magic," we won't see them being called explicitly in one
method by another method versus Rails running it for us, we put such statements
at the top so that it catches other programmers' eyes.

Here is a rule of thumb: **Whenever you are modifying an attribute of the
model, use `before_validation`. If you are doing some other action, then use
`before_save`.**

We use `before_save` for actions that need to occur that aren't modifying the model
itself. For example, whenever you save to the database, let's send an email to
the `Author` alerting them that the post was just saved!

This is a perfect `before_save` action. It doesn't modify the model so there is
no validation weirdness, and we don't want to email the user if the Post is
invalid.

`before_create` is very close to `before_save` with one major
difference: it only gets called when a model is created for the first time.
This means not every time the object is persisted, just when it is **new**.

For more information on all of the callbacks available to you, check out [this
amazing rails guide][callbacks]

[callbacks]: http://guides.rubyonrails.org/active_record_callbacks.html

