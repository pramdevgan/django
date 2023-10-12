# Introduction

## HTML Frameworks Intro

You have definitely used a framework before: Django! A framework is a project that contains common functionality that can be used by many different people for their own projects. You just need to "fill in the blanks". Without Django, you’d have to write a lot of things from scratch. All the way from the HTTP server interface, to the database connection, URL routing and template engine.

HTML frameworks work in a similar manner. Without using one, you’d have to write a lot of custom CSS and Javascript, before you could even start on the parts of the site that are unique to your project.

HTML frameworks might also be referred to as *CSS Frameworks* , as most of their functionality is achieved with custom CSS, so you might see these terms used interchangeably. Note though that *Javascript Frameworks* , like [Vue.js](https://vuejs.org/), [React](https://reactjs.org/) or [Angular](https://angularjs.org/) are completely different and serve a different purpose: to provide interactive or dynamic web applications with Javascript code.

By using an HTML framework, we can get the following things:

* A *reset* look and feel, so that elements, font sizes and spacing look the same across different browsers.
* Components like navigation bars, panels, cards and modals.
* Automatic Javascript hooks for simple interactive elements
* Utilities for element spacing, text size, colors, and more.
* A grid system for layout.

Usually components and styles are built by adding classes to normal HTML elements – generally HTML frameworks don’t provide new types of tags.

Using frameworks can have some downsides though:

* Including a framework can bring in large CSS files which would slow down your page load. If you only wanted a couple of features from a framework this can seem inefficient.
* Websites built with a particular framework can end up looking similar. If you’re building a portfolio site to showcase your web design skills, this might not be what you want.
  – On the flipside though, the familiarity can make your UI easier for users to understand.
* If you want to customize the look of some of the elements, it can be a lot of work to write the correct CSS.

There are many HTML frameworks available, to fit many different needs. But once you learn one, the concepts are quite similar between them. Here’s a super short look at three of them:

### Bootstrap

[Bootstrap](https://getbootstrap.com/) is "the most popular HTML, CSS and JS library in the world.". It includes many different components and Javascript functionality for interactivity.

### Foundation

[Foundation](https://get.foundation/) is the "most advanced responsive front-end framework in the world". While not as popular as Bootstrap some people prefer it for its semantic markup and mobile-first approach.

### Bulma

[Bulma](https://bulma.io/) is newer than Bootstrap and Foundation, and is more lightweight. It’s not as full-featured and doesn’t include its own Javascript helpers, so you’ll need to write your own for interaction. Many people prefer it for this reason.

### Tailwind CSS

[Tailwind CSS](https://tailwindcss.com/) is growing in popularity and loved for its utility approach to classnames and its small size. Like Bulma, you’ll need to provide your own Javascript.

In this and the subsequent courses, we’ll use Bootstrap, because of its popularity and the number of components it provides. Plus, it’s used with the Django Rest Framework UI which we’ll look at in Course 2.
