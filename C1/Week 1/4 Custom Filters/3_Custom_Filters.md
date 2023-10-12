# Custom Filters

# Custom Filters

In Django templates, you can pass data through filters before it’s rendered. This is done with the `|` (pipe) operator inside a rendering block. For example, to render a value in lowercase, using the `lower` filter, you’d do this:

```html
{{ value|lower }}
```

Some filters accept arguments, which can be sent by adding `:` (colon) after the filter name. For example, the `date` filter takes an argument that specifies the output format:

```html
{{ post.published_at|date:"M, d Y" }}
```

Django has an [extensive set of built-in filters](https://docs.djangoproject.com/en/3.2/ref/templates/builtins/#built-in-filter-reference), but if none of them quite do the job you need, you can write your own. These can contain more complex logic, which can be easier than trying to write lots of custom code inside your template.

Before we get into that, let’s add a real page to Blango. It will be a page that lists all the blog posts we have.

## Try It Out

First, we’ll update the `index` view to fetch all the `Post` objects in the system, and send them to the `index.html` template. This should be functionality you’ve used with Django before. Your `views.py` will look something like:

```python
def index(request):
    posts = Post.objects.filter(published_at__lte=timezone.now())
    return render(request, "blog/index.html", {"posts": posts})
```

Note the use of the `published_at__lte=timezone.now()` filter. This means we’ll only load `Post` objects that have been published (have a publication date in the past).

Also, be sure to import `timezone` from `django.utils` and `Post` from `blog.models`, at the start of the file:

```python
from django.utils import timezone
from blog.models import Post
```

Next we need to render the post data in the template (`index.html`). We’ll just use a simple loop and render each blog `Post` in a Bootstrap `row`. You can copy and paste this to replace the `content` block in your template:

[Open index.html]()

```html
{% block content %}
    <h2>Blog Posts</h2>
    {% for post in posts %}
    <div class="row">
        <div class="col">
            <h3>{{ post.title }}</h3>
            <small>By {{ post.author }} on {{ post.published_at|date:"M, d Y" }}</small>
            <p>{{ post.summary }}</p>
            <p>
                ({{ post.content|wordcount }} words)
                <a href="#">Read More</a>
            </p>
        </div>
    </div>
    {% endfor %}
{% endblock %}
```

You can see we’re just showing the post’s `title`, `author`, `published_at` date, `summary` and a count of the words in its `content`

You should notice that we’re using two built in filters:

* The `date` filter which outputs the date in *month, day year* format (its argument).
* The `wordcount` filter to count the words in the `Post`'s content. Note that this is not strictly correct as we’re storing raw HTML in the `content` field and thus the count will include the tags and attributes; but for illustrative purposes it is fine.

If you don’t already have some test Blog data added, you should log to the Django admin and add a couple of posts, and another user as an extra author. This will come in handy later.

Provided you’ve done this and have some test data, when you start the Django dev server and navigate to the main page you should see something like this:

START DEV SERVER

[View Blog]()

![Blog post list](https://apollo-media.codio.com/media%2F1%2F442f04fd9ca01bf6084d99b2c6a78c77-60d2e78c3c6188e3.webp)

Next we’ll look at how to set up the files that contain the template tags and filters.

## Template Tag File Set Up

You’ve probably loaded custom template tag libraries into a template before using the build in `load` template tag. More than likely, you’ve loaded the `static` template tag library like this:

`{% load static %}`

Django looks for template libraries to load inside Python files in the `templatetags` folder inside Django apps. The template library it loads is simply the name of the file.

For example, in Blango we’ll create a template tag library with the path `blog/templatetags/blog_extras.py`. We would load it into the template like this:

```html
{% load blog_extras %}
```

Note that the convention is to name template tag files in the format *[something]_extras.py* , but this is not mandatory. You just need to be sure that your file won’t conflict with any of the built in template libraries or third parties that you might have included. Template tag files aren’t namespaced so `blog_extras` could be used by any app in our project.

## Try It Out

Let’s start by setting up the directory structure for the custom template tags. You’ll need to create the following things:

* A directory named `templatetags` inside the `blog` app directory.
* An empty `__init__.py` file inside the `templatetags` directory.
* An empty `blog_extras.py` file, also inside the `templatetags` directory.

<details><summary><strong>Solution</strong>
</summary>

![Template Tags Directory Structure](https://apollo-media.codio.com/media%2F1%2F135505826a33808503048df028b77431-fdddf42bfecd2fa1.webp)

</details>

You can leave this file open as we’ll be working with it straight away.

## Reading Question

Fill in the blanks below.

The <span style="color:green; font-size:26px">|</span> operator is used to filter data passed to a template.
The <span style="color:green; font-size:26px">:</span> operator is used to pass arguments to filters.
