# Django Admin Quickstart

One of the features of Django that makes building websites with dynamic content so fast is its built-in admin system. It provides a web interface that lets you create, edit and delete any Django model instances that you choose. The admin system is enabled by default when you start a Django project, but only models that you choose are exposed. By default the path to access the admin UI is `/admin/`, (e.g. [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/) if running the Django debug server).

### Disabling Django Admin

If you don’t want Django Admin enabled, how is it turned off? There are two things to do (**Note,** do not do disable Django admin, this is just so you understand how to do it):

* Remove `django.contrib.admin` from `INSTALLED_APPS` in the Django settings

  [file]().
* Remove the `admin/` URL rule from the project’s `urls.py`

  [file]().

While on the subject of the admin URL, you can get a little extra security if you change it from the default `admin/` to something else. This would prevent attackers from guessing the URL. Since the admin site is password protected anyway, this is not something you’d normally have to do, but it could help if any of your admin users have weak passwords. We’ll stick with the default `admin/` in this course.

### Registering Models to the admin UI

Upon scaffolding a Djanog app, an `admin.py` file is automatically added. This is where Django will read the definition for the admin interface for your app. There are two ways to register a model and have it show in the Django admin UI. You can either register the model directly, which will just use the defaults and allow all fields to be editable. Most of the time, this is adequate, but sometimes you might want to create a model admin class by subclassing the Django `admin.ModelAdmin` class. This allows you to set options about how your model is displayed in the admin. Let’s examine the `admin.py` file and then see how to implement both these methods.

When scaffolded the `admin.py` file contains just one code line (and a comment, which can be removed):

```python
from django.contrib import admin
```

As you can probably guess, this imports the Django admin module, ready for use. To register a model into the admin section, we use the `admin.site.register` function.

## What is `admin.site`?

`admin.site` is an object representing the admin site. We also saw it used in the `urls.py` file, routing the `admin/` path to `admin.site.urls`. We won’t discuss its functionality in depth, but it’s possible to customize the site to override things like the page titles, header text and template. You can find more details about this at the [Django Admin Site Documentation](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#adminsite-objects)

Let’s start by looking at the simplest method of registering a model. We’ll do this with the `Tag` model. First our model needs to be imported into the `admin.py` file:

```python
from blog.models import Tag, Post
```

Then register it:

```
admin.site.register(Tag)
```

To configure how the admin site behaves with a certain model, a subclass of `admin.ModelAdmin` must be created. This subclass’s attributes determine how the model is displayed. First let’s look at how we’ll create one, for the `Post` model.

```python
class PostAdmin(admin.ModelAdmin):
    prepopulated_fields = {"slug": ("title",)}
```

Here we’re setting just one attribute, `prepopulated_fields`. When used in this way, some JavaScript is inserted into the admin page so that the `slug` field updates when the `title` field changes. It will automatically “slugify” the title. But, there are many other ways to customise the ModelAdmin. Some of the more common customizations are:

* `exclude`: a list of fields to disallow editing of in the admin. For example, we might want to prevent users from manually setting the `slug`, and instead compute it when saving the Model. In which case, we would set `exclude` to `["slug"]`.
* `fields`: this works the opposite way to `exclude`. If set, only fields in the `fields` list will be editable. Note that if a field requires a value, but is not editable (either by the use of `exclude` or `fields`), then saving the model instance will fail because the field will not be valid.
* `list_display`: a list of fields to include in the admin page list view. For example, we might want to see both a Post’s title, and when it was published. We would do this by setting `list_display` to `["title", "published-at"]`.

There are many more options that can be used, and the full list can be viewed at the [Django Model Admin Options Documenatation](https://docs.djangoproject.com/en/3.2/ref/contrib/admin/#modeladmin-options).

Now that the `PostAdmin` class is defined, let’s return to the `register` function. The `PostAdmin` class is passed as the second argument:

```python
admin.site.register(Post, PostAdmin)
```

## Reading Question

Select all of actions that Django performs to “slugify” text. **Hint:** there is more than one correct answer.

- ***Convert to lowercase***
- ***Remove non alpha-numeric characters***
- ***Remove common words***
- ***Replace spaces with dashes***

```
Django performs all of these actions when it “slugifies” text.
```
