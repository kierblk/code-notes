# [Rails MVC Review](https://github.com/saramccombs/refresher-on-mvc)

## Objectives

1.  List advantages created by compartmentalizing an application's functionality

2.  Identify model-view-controller roles within a simplified example

3.  Identify model-view-controller roles within Rails' implementation of the paradigm

## Separation of Concerns

At its core, MVC is designed to modularize distinct functionality within an
application.

- `View`: what an end user on a website experiences when interacting with
  a program in their browser: what they read, what they click, what flashes
  at them, and what they hear (despite the name "view"). In technology-speak, the
  vocabulary word would be _interface_
- `Model`: where the actual data, (be it information about restaurants,
  train times, or rare marsupials), resides and is altered
- `Controller`: what manages communication between the two: it takes
  model information and prepares it for the view and vice versa

  Now that we have identified the core components, let's examine what they
actually do when a user engages with our web application:

1.  A user, through interaction with the `view`, (in this case, the browser's GUI),
    requests data (clicks on a link, submits a form, enters a URL in the browser's
    bar
2.  The request is sent across the internet to the server
3.  The `controller` (_which does not change data itself!_) asks the `model` to
    either provide it data (which it will send) or to change model-held data
    depending on the user's request
4.  The `model` accesses/manipulates the actual 1's and 0's held on the server's
    database and returns the desired result to the `controller`
5.  The `controller` packs the response and sends it back to the client
6.  The `view` (on the originating client's machine) _presents_ the data for the
    user

In considering the above steps, try to answer the following question:

- Do the **model** and **view** have any actual direct interaction?
- Is the data represented in the `view`, that the user sees and interacts with,
  anything but a virtual copy of the _actual_ data a user perceives they are
  interacting with?

## An Advantage of Modularity

For every
new device, we write new-device-only code (i.e. `view` code) which **cannot**
introduce bugs into the pre-existing Model or Controller code. It's because of
design patterns like this that 1970's banking software is still holding your
account data while you view and manipulate it with 21st century technology.

## Where Rails Fits In

Rails takes architectural guidance on how to separate concerns from the MVC
pattern. Like most implementations of academic or philosophical ideals, Rails's
implementation is not to-the-letter perfect MVC. That's OK. Consider the
textbook definition of apple pie crust: the textbook definition describes exact
ratios of salt, sugar, fats, etc. But my implementation might be different than
Avi's implementation. Is mine less correct? Is his less correct? There's room
for intelligent discourse and discovery of what's appropriate to the
constraints.

#### Rails MVC Implementation

The `controller` and `model` implementations in Rails are straightforward to align with our understanding of MVC.

Not only are they named helpfully and live in helpfully-named directories like
`models/` and `controllers/`, but they encapsulate their responsibilities as
prescribed in the MVC architecture. The controller actions mediate requests and
delegate lookups by calling methods on models. As expected, models work with the
low-level persistent storage subsystems (e.g. databases) to UPDATE, SELECT, and
DELETE data in the database. The Rails views are templates for displaying data.
They are automatically turned into HTML that is sent over the internet by Rails.
However, the data they need to "complete" themselves is provided by a Rails
controller. Rails "automagically" shares any variable prefixed with `@` in a
controller action with the view.

_ASIDE_: Some feel that this "automagic" is "bad." DHH (David Heinemeier Hansson) feels that this
"automagic" is "good." Reasonable programmers can disagree over the advantages
and disadvantages of this choice. However, since DHH created Rails and runs the
project, his opinion is the one implemented.

## Summary

- The MVC paradigm is a language- and application-agnostic pattern for separating
  concerns
- MVC describes an architecture of three modularized parts: `model`, `controller`,
  `view`
- While Rails emulates the majority of an MVC structure, it is not a perfect
  "textbook" match &mdash; _by design_!