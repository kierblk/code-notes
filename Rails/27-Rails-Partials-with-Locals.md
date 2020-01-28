# Rails - Partials with Locals

## Objectives

1. Use the `locals` keyword
2. Understand why using instance variables in partials is non-optimal
3. Use a partial while rendering a collection
4. Use a partial from another controller with a local

## Introduction

Partials help us break our code up into reusable chunks.  They also often have
implicit dependencies that can lead to bugs.  For example, what if a partial
assumes that a `@user` variable is present. If the point is to _reuse_ partials,
if you put it inside of an action that _didn't_ set a `@user` variable, you're
going to have a bug. Using "locals" in partials is how we can make these
implicit assumptions explicit.  In the following example, we'll unpack exactly
what locals are and how they're used.

TODO: FInish taking notes on this lesson.