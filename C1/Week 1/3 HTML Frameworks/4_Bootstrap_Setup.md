# Bootstrap Setup

## Bootstrap Setup

How do we “install” Bootstrap into our project? It’s simple, the only requirement is to link in the Bootstrap CSS, by adding a `<link>` element to the `<head>` of our HTML. Like this:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
```

And the vast majority of the time you’ll want to include the Bootstrap Javascript files, by adding a `<script>` element to the end of your `<body>` in the HTML, like this:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
```

Note that the version (*5.0.2* in our case) and integrity hashes (the values that start with *sha-384* ) will change with new releases of Bootstrap. You find the latest versions to use on the [Bootstrap introduction page](https://getbootstrap.com/docs/5.0/getting-started/introduction/).

Bootstrap also provide a [starter template](https://getbootstrap.com/docs/5.0/getting-started/introduction/#starter-template) which can be very handy to copy and paste to get a new site up and running. In fact, we’ll do that now to get our first view in Blango. You should be familiar with the process of setting up templates and views in Django, so we’ll just briefly go over the steps.

1. Create a `templates` directory inside the root of the project. We’ll use this to store global templates. Do this by right-clicking on `blango` and selecting `New Folder...`. The path to the new directory should be `blango/templates`.
2. Inside the `templates` project directory, create a new file called `base.html`. Right-click on `templates` and select `New File...`. In here we’ll basically copy and paste the [starter Bootstrap template](https://getbootstrap.com/docs/5.0/getting-started/introduction/#starter-template), but make a couple of edits:

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-EVSTQN3/azprG1Anm3QDgpJLIm9Nao0Yz1ztcQTwFspd3yD65VohhpuuCOmLASjC" crossorigin="anonymous">
    <title>Hello, world!</title>
  </head>
  <body>
    <h1>Hello, world!</h1>
    {% block content %}

    {% endblock %}
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js" integrity="sha384-MrcW6ZMFYlzcLA8Nl+NtUVF0sA7MsXsP1UyJoMp4YLEuNSfAP+JcXn/tWtIaxVXM" crossorigin="anonymous"></script>
  </body>
</html>
```

Here, we have removed the comments and commented out code, and added a template `block` called `content` that can be overridden by child templates.

`base.html` can now be saved.

3. Now we want Django to be able to load templates from this directory, so we need to add it to the `TEMPLATES` settings in our `settings.py`. Open this file, and then find the `TEMPLATES` setting. You should see it has a key of `DIRS`, with an empty list:

[Open settings.py]()

```python
'DIRS': [],
```

Add the path to the `templates` directory into the list, like this:

```python
'DIRS': [BASE_DIR / 'templates'],
```

<details><summary><strong>Path Objects and Strings</strong></summary>

[](https://docs.python.org/3/library/pathlib.html#pathlib.Path)

</details>

While we’re here, notice the setting `"APP_DIRS": True`. This means that Django will automatically try to find templates in app directories. We’ll see what this means in the next step.

`settings.py` can now be saved and closed.

4. Now, we’ll add a templates directory for the `blog` app, to hold blog specific templates. Go to the `templates` directory. Inside this, create a directory called `blog` (so you should have the path `blango/templates/blog`). The `blog` directory is for template namespacing. It means templates in here won’t conflict with the names of other templates in our project.

Since we had the setting `'APP_DIRS': True`, Django is automatically going to look in the `blango/templates` directory for templates, so we don’t need to make any more settings changes.

5. Create a new file in the `blango/templates/blog` directory called `index.html`. It should inherit from the global `base.html` and override the `content` block. The contents aren’t too important, so you can use something like:

[Open index.html]()

```html
{% extends "base.html" %}
{% block content %}
<h2>Index Template</h2>
{% endblock %}
```

Save and close `index.html`.

6. We need a view to render this template. Create one called `index` in the `blog/views.py`:

[Open views.py]()

```python
def index(request):
    return render(request, "blog/index.html")
```

7. Finally, let’s route the root path to this view. Add a route for `""` (empty string) to this view in `urls.py`. Don’t forget to also import the views file. Here’s a truncated view of `urls.py`

[Open urls.py]()

```python
# other imports
import blog.views

urlpatterns = [
    # other patterns
    path("", blog.views.index)
]
```

Save `urls.py`.

8. Now, you can start the Django dev server and check out the template.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

[View index.html]()

You should see something like this:

![Bootstrap Hello World Template](https://apollo-media.codio.com/media%2F1%2F66c061940cc5330a31909d7cfe3e67cb-f7aca956e03b9c51.webp)

Now we have Bootstrap included and ready to go in our template, and we can start using Bootstrap classes and components. Next we’ll take a quick look at some of the Bootstrap components.


## Reading Question

What are the benefits of using the Bootstrap framework? **Hint,** there is more than one correct answer.

- ***Easy access to pre-made components***
- ***Consistent look and feel across browsers***
- Provide interactive web applications with JavaScript code
