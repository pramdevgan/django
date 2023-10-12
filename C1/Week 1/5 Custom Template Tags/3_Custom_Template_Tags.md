# Custom Template Tags

## Custom Template Tags

If filters aren’t powerful enough to achieve the desired output in your template, the next step is to use template tags. Template tags are much more powerful and flexible. You have used a lot of template tags already:

* `extends`, as in `{% extends "base.html" }`
* `block`, like `{% block content %}`
* `if` and `for` template tags, for flow control
* and probably many more!

Django allows you to write your own custom template tags too. Template tags can accept no arguments, or as many as you need, including positional, and optional keyword arguments. You use them to output values, render a template, or even parse content between two tags that you specify.

Before we start on some custom template tags, we’ll add a new Post detail page to Blango, so we can view a Post’s content. This will involve:

* Creating a new template to display the post
  * And, a small refactoring of the byline rendering to remove duplicated code
* Linking to the Post detail page in the `index.html` template
* Adding a view to fetch and render the new template
* Adding a URL mapping to the new view

Let’s get started.

## Try It Out

Create a new file called `post-detail.html` inside the `blango/templates/blog` directory. As with `index.html`, it will extend the `base.html` template and override the `content` block.

Copy and paste this content inside `post-detail.html`:

```html
{% extends "base.html" %}
{% block content %}
<h2>{{ post.title }}</h2>
<div class="row">
    <div class="col">
        {% include "blog/post-byline.html" %}
    </div>
</div>
<div class="row">
    <div class="col">
        {{ post.content|safe }}
    </div>
</div>
{% endblock %}
```

Two things to note:

* We are including `post-byline.html` which doesn’t exist yet, but we will create it soon.
* The `safe` filter is being applied to `post.content`. As we discussed in the previous section on HTML safe filters, this is definitely **not** best practice for a production site as we couldn’t trust the user generated input. As was already mentioned, a library like [Bleach](https://bleach.readthedocs.io/en/latest/) should be used to sanitise the HTML output before being rendered. For the sake of our example site, where we are probably the one and only user entering content, it is good enough.

Create another new file in the same directory, called `post-byline.html`. We want to display the byline (author detail and published date) on both the Post list and Post detail pages, so we’ll move it into its own template so it can be included.

Inside `post-byline.html`, you can paste this content:

[Open post-byline.html]()

```html
{% load blog_extras %}
<small>By {{ post.author|author_details:request.user }} on {{ post.published_at|date:"M, d Y" }}</small>
```

Next we’ll do a couple of changes to `index.html`:

[Open index.html]()

* Remove the `{% load blog_extras %}` template tag, as we no longer need to use the `author_details` filter in this template.
* Replace the byline HTML with an `include` of the `post-byline.html` template.
* Change the *Read More* link to go to the new URL that we’ll create.

You can copy and paste this HTML into `index.html`:

```html
{% extends "base.html" %}
{% block content %}
    <h2>Blog Posts</h2>
    {% for post in posts %}
    <div class="row">
        <div class="col">
            <h3>{{ post.title }}</h3>
            {% include "blog/post-byline.html" %}
            <p>{{ post.summary }}</p>
            <p>
                ({{ post.content|wordcount }} words)
                <a href="{% url "blog-post-detail" post.slug %}">Read More</a
            </p>
        </div>
    </div>
    {% endfor %}
{% endblock %}
```

Notice the use of the `url` template tag to link to a URL with the name `blog-post-detail`, providing the `post.slug` as an argument.

Next, we have to create the view to render this template. Open the `blog` app’s `views.py` file. The `post_detail` view is quite simple, just fetching a Post using its `slug`. We make use of the `get_object_or_404` shortcut which will automatically return a 404 Not Found response if the requested object isn’t found in the database:

[Open views.py]()

```python
def post_detail(request, slug):
    post = get_object_or_404(Post, slug=slug)
    return render(request, "blog/post-detail.html", {"post": post})
```

Make sure to import the `get_object_or_404` function at the stop of the file.

```python
from django.shortcuts import render, get_object_or_404
```

For the final step, we need to add the URL mapping in `urls.py`.

[Open urls.py]()

Add a new url mapping to `urlpatterns`, like this:

```python
    path("post/<slug>/", blog.views.post_detail, name="blog-post-detail")
```

After editing this file, start the Django dev server if it’s not already running, then load (or refresh) the main page. You should see that the post list page doesn’t look any different, but you should be able to click on a `Read More` link to go to a Post detail page, which will look similar to this (depending on your post content, of course):

START DEV SERVER

[View Blog]()

![Post Detail](https://apollo-media.codio.com/media%2F1%2F1f88f1d70de1790f957cb626010f8480-d642cf92eec4b4d8.webp)

Now on to template tags, starting with simple tags.
