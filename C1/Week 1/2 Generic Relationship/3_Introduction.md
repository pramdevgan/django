# Introduction

Django has a powerful system for relating different models together. By using `ForeignKey`, `ManyToManyField` and `OneToManyField` fields, we can model many different ways of how models relate to each other. In Blango so far, we’ve used a `ForeignKey` field on the `Post` model to set the author of each Post. We also used a `ManyToManyField` to assign `Tag`s to `Post`s.

One of the limitations of this system is that relationships between models are statically defined, and can only exist for a single model per field: `Tag`s can only be mapped to `Post`s (or vice versa).

Django comes with the *contenttypes* framework, which provides a high level way of accessing referring to models in a project. It also allows for *generic relationships* , a way of mapping objects together without statically defining a model to a single other model.

We’ll get into generic relationships soon, but let’s start with a look at the main features the *contenttypes* framework provides.
