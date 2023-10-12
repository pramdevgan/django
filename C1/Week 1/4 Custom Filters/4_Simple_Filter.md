# Simple Filter

## Simple Filter

In its simplest form, a filter is just a function that takes a single argument and returns a string to be rendered in the template.

In our Blango `Post` list we’re just showing the author’s username `{{ post.author }}`. However, we want to show some more details if available. That is, the author’s first and/or last name instead. We’ll call this filter `author_details`.

## Try It Out

You can try writing the function called `author_details`.

* It should take a single function, the author of the `Post` (which is a `django.contrib.auth.models.User` object).
* If the author has a `first_name` and a `last_name` set, then it should return a string in the format "{first_name} {last_name}".
* Otherwise it should return the author’s username. It can also be useful to check that a `User` object has been passed to the function and return an empty string if not – this is a failsafe default.

<details open=""><summary><strong>Solution</strong></summary>

Your `blog_extras.py` file should now look something like this:

```python
from django.contrib.auth import get_user_model
user_model = get_user_model()


def author_details(author):
    if not isinstance(author, user_model):
        # return empty string as safe default
        return ""

    if author.first_name and author.last_name:
        name = f"{author.first_name} {author.last_name}"
    else:
        name = f"{author.username}"

    return name
```

Note the use of `isinstance` to check that we’re working with a `User` object, just in case someone has passed the wrong type of variable. In our case, it’s not likely to happen as the `author` of a `Post` can’t be anything but a `User`. But it’s a good habit to do checks like this in filters, just in case a variable happens to be the wrong type – perhaps `None` when you don’t expect it. An exception raised in filter code will cause an error to be returned to the end user.

</details>

Before the filter can be used, it needs to be registered into the template library. This is actually a three step process:

1. Import the `django` `template` module.
2. Create an instance of the `django.template.Library` class.
3. Register the filter function into the `Library` with its `filter` function.

(Steps 1 and 2 only need to be done once per template tag file).

Let’s do this now:

* Add the import to the top of your `blog_extras.py` file:

<details open=""><summary><strong>Solution</strong></summary>

Import `template` like this:

```python
from django import template
```

</details>

* Create the `template.Library` instance. Convention is to call this variable `register`, as it makes it more clear what its methods do when you use them. It’s a global variable in the file, and should come before the filters.

<details><summary><strong>Solution</strong></summary>

```python
register = template.Library()
```

</details>

* Filters must be registered, so that any other non-filter functions in the file don’t get picked up by Django. There are couple of different ways to use the `Library.filter` function, which you can read about in the [official documentation](https://docs.djangoproject.com/en/3.2/howto/custom-template-tags/#registering-custom-filters), but we’re going to go with the simplest method: use it as a decorator

<details><summary><strong>Solution</strong></summary>

```python
@register.filter
def author_details(author):
    # existing function body
```

</details>

As you can see, since we called the `Library` instance `register`, it makes it clear that the decorator is *registering* a *filter* .

The name of the filter in the template is automatically made the same as the name of the function, but this can be customized by passing a `name` argument to `register.filter`. For example, `@register.filter(name="author_details")`. We don’t need to do this as we’re happy with the `author_details` name.

Now let’s use it in our template. Open the `index.html` template and load the `blog_extras` template library using the `load` tag.

[Open index.html]()

Load the `blog_extras` template library.

* Add `blog_extras` in `index.html`.

<details><summary><strong>Solution</strong></summary>

```html
{% extends "base.html" %} <!-- existing line -->
{% load blog_extras %}
```

</details>

* Update the byline text so it includes the `author_details` filter.

<details><summary><strong>Solution</strong></summary>

```html
<small>By {{ post.author|author_details }} <!-- existing line -->
```

</details>

Refresh the page in your browser and you should see the author’s first and last name instead of their username, if set. Make sure you’ve set a first and last name for one of your users in Django admin though!

START DEV SERVER

[View Blog]()

![Author Name Filter](https://apollo-media.codio.com/media%2F1%2F821a2fb7a1da73608e753b345ca6cecb-36a0e5c0af962eb5.webp)

Next we’ll see how Django handles HTML with filters.

## Reading Question

Assume the following code:

```python
@register.filter
def author_details(author):
    if not isinstance(author, User):
        # return empty string as safe default
        return ""

    if author.first_name and author.last_name:
        name = f"{author.first_name} {author.last_name}"
    else:
        name = f"{author.username}"

    return name
```

Why is that function definition preferable to the following function definition?

```python
@register.filter
def author_details(author):
    return f"{author.first_name} {author.last_name}"
```

**Hint,** there is more than one correct answer.

- **The second function will throw an error if it is passed a value that is not of type User.**
- **The second function will throw an error if author does not have both first_name and last_name attributes.**
- The second function will throw an error if either first_name or last_name is an empty string.

The first function definition is preferable because:

* It will not throw an error if `author` is not of type `User`
* It will not throw an error if `author` only has the attribute `first_name`

The second function only works if `author` is of type `User` and has the attributes `first_name` and `last_name`.
