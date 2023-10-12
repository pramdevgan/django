## Introduction

Hello, and welcome to Advanced Django. This course is aimed at those who have some understanding of Django, and perhaps have even completed a project or two.

This course is divided into four modules. We’ll be building blog project in Django throughout the course, gradually adding features to it. The first module expands on the Django fundamentals. We’ll look at the admin section, generic model relationships and the Bootstrap HTML framework, then how using custom template tags and filters can cut down the amount of code in your templates.

Module 2 introduces *12-Factor Apps* : an informal standard for configuration applications. We’ll look at the most important of these factors to build into a Django application (configuration and logging). Then we’ll give you a better understanding of some of Django’s security features, then discuss some different ways to deploy your application.

Module 3 is about performance. We’ll introduce caching and how to use it with your Django application, then look at how to optimize your database and queries for more speed.

Module 4 is about the user. You’ll learn about custom user models, and how they differ from just using a profile object. We’ll then look at some third party modules to help with users and registration: Django Registrations (to make users validate their email address after signing up), and Django All Auth to allow authentication via third party services or social networks. We close the module by walking through how to set up authentication against Google OAuth.

## Code

All code is PEP8 formatted using the [Black](https://github.com/psf/black) code formatting tool for consistent formatting.

## The Project: Blango

In this course (and through Course 3) you’ll be building a Blog app in Django. It’s called *Blango* (*Blog* + *Django* , of course!)

Hopefully the concepts behind the app are quite familiar. It’s been deliberately chosen to let you focus on the Django side of things rather than the domain/data model. Each author is a Django user and can create blog Posts which have Tags assigned to them. Comments can be added to Posts, and files can be attached to either Posts or Comments.

Not everything will be built at once, we will gradually add features to make the application more useful.

Next
