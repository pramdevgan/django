# Filters with Arguments

### Filters with Arguments

Filter functions can also take a single argument. We’ve seen this with the `date` filter, which takes a format string. Adding an argument to a filter is simple: just add an argument to the filter function, and then pass in the argument in the template, with the `:` operator.

Let’s update `author_details` to return the string `<strong>me</strong>` if a `Post` is authored by the currently logged in user.

## Try It Out

You should have all the knowledge to complete this yourself, hint: the current user is accessible in the template with the `request.user` variable. Give it a try yourself, and if you get stuck, come back here.

Here’s how you do it, first the update to the `author_details` function.

```python
@register.filter
def author_details(author, current_user):
    if not isinstance(author, user_model):
        # return empty string as safe default
        return ""

    if author == current_user:
        return format_html("<strong>me</strong>")

    if author.first_name and author.last_name:
        name = f"{author.first_name} {author.last_name}"
    else:
        name = f"{author.username}"

    if author.email:
        prefix = format_html('<a href="mailto:{}">', author.email)
        suffix = format_html("</a>")
    else:
        prefix = ""
        suffix = ""

    return format_html('{}{}{}', prefix, name, suffix)
```

Remember to mark the return string as safe using the `format_html` function, so the `<strong>` element is rendered properly in HTML.

Then update your `index.html` file to pass `request.user` to the filter:

```html
<small>By {{ post.author|author_details:request.user }} on {{ post.published_at|date:"M, d Y" }}</small>
```

Refresh the post list and your page should look like this (provided you’re logged in as one of the authors, which you can do through the Django admin section. The login to the admin page carries through to the rest of the site):

START DEV SERVER

[View Blog]()

![Current User is Author](https://apollo-media.codio.com/media%2F1%2F1060d8bed41c567369ef6a0e87ba33b3-08555aab66444dfd.webp)

Note that you could also provide a default value to `current_user` in the function definition, e.g:

```python
def author_details(author, current_user=None):
```

Then, your filter would be callable without any arguments. You could use this to provide default values to a filter but still make its behavior customizable.

## A Post Script on HTML in Template Tags

One of the key features of Django is its template system. From the start, it has been designed to allow multiple people with different skills to contribute to a Django project. Those who have HTML, CSS and other UX skills can work on the templates in HTML, while back-end Python developers can build the views and models. When you start generating HTML in template filter, you remove the ability for this type of separation of concerns.

Another thing to consider is that it can be harder to locate where HTML is being generated, if it’s not in a template and instead is being generated with a template tag.

That’s not to say you shouldn’t do it, but keep these drawbacks in mind before you do. One advantage is that it can cut down on many lines of code and logic in a template, which can arguably be harder to read. For comparison, our `author_details` code in a template would look something like this:

```html
<small>By
    {% if post.author == request.user %}
        <strong>me</strong>
    {% else %}
        {% if post.author.email %}
            <a href="mailto:{{ post.author.email }}">
        {% endif %}
            {% if post.author.first_name and post.author.last_name %}
                {{ post.author.first_name }} {{ post.author.last_name }}
            {% else %}
                {{ post.author.username }}
            {% endif %}
        {% if post.author.email %}
            </a>
        {% endif %}
    {% endif %}
    on {{ post.published_at|date:"M, d Y" }}
</small>
```

It’s a few less lines of code but harder to read. The piece that particularly stands out to the author is the use of `{% if post.author.email %}` twice, once for the opening and once for the closing `<a>` tag. If you have more HTML in between these `if` blocks it can get hard to keep track of the opening and closing tags when they’re always wrapped up in conditionals.

As with so many things in programming though, it depends on your particular situation, personal prefererence and company/individual needs. Those were just some points to consider when making your decision.

Next we’re going to look at custom template tags, which can be used when filters aren’t quite flexible enough to get the job done for you.

Reading Question
Select the code sample that passes an argument to a filter.

```html
<small>By {{ post.author|author_details(request.user) }} on {{ post.published_at|date("M, d Y") }}</small>
```

```html
<small>By {{ post.author|author_details[request.user] }} on {{ post.published_at|date["M, d Y"] }}</small>
```

```html
<small>By {{ post.author:author_details|request.user }} on {{ post.published_at:date|"M, d Y" }}</small>
```

```html
<small>By {{ post.author|author_details:request.user }} on {{ post.published_at|date:"M, d Y" }}</small>
```

Here is the solution:

```html
<small>By {{ post.author|author_details:request.user }} on {{ post.published_at|date:"M, d Y" }}</small>
```

The `:` operator is used to pass an argument to a filter. In the example above, `request.user` is passed to the `author_details` filter, and `"M, d Y"` is passed to the `date` filter.
