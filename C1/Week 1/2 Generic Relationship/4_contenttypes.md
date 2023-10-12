# contenttypes

The main use of the contenttypes framework is to dynamically load models classes based on their name, and subsequently, query objects for that model.

The main model is `ContentType`, which is importable from `django.contrib.contenttypes.model`. This works like a normal model whose `objects` you can query. If you know the model you want, you can query it using the app name and model name.

Let’s see how to load the `Post` `ContentType` from the `blog` app. First start a Django Python shell:

```bash
python3 manage.py shell
```

### Entering Shell Commands

When copying/pasting shell commands into the terminal, it is important to not copy the entire code block. This will cause errors. You should only copy lines of code that start with `In [#]:`. This indicates a line of input. Copy everything after the `:`. Lines of code that start with `Out[#]:` are the expected output.

![understanding input and output for the shell](https://apollo-media.codio.com/media/1/eb70a9f0dc3332574338194e98730d33-4e513abd34f855c6.webp)

Then import `ContentType` and query for the object.

```python
In [1]: from django.contrib.contenttypes.models import ContentType

In [2]: post_type = ContentType.objects.get(app_label="blog", model="post")

In [3]: post_type
Out[3]: <ContentType: blog | post>
```

We could also get a list of all the `ContentTypes` we have installed, by calling `ContentType.objects.all()`:

```python
In [4]: ContentType.objects.all()
Out[4]:
<QuerySet [<ContentType: admin | log entry>, <ContentType: auth | permission>, <ContentType: auth | group>, <ContentType: auth | user>, <ContentType: contenttypes | content type>, <ContentType: sessions | session>, <ContentType: blog | post>, <ContentType: blog | tag>]>
```

Note that the `ContentType` object is *not* the `Post` model. But, we can retrieve the class with the `model_class()` method:

```python
In [5]: post_type.model_class()
Out[5]: blog.models.Post
```

It’s also possible to go in reverse, and retrieve the `ContentType` object from the model. This is done with the `ContentType.objects.get_for_model()` method.

```
In [6]: from blog.models import Post

In [7]: ContentType.objects.get_for_model(Post)
Out[7]: <ContentType: blog | post>
```

This is useful if you want to know the `app_label` and `model` name for a model class.

Once a `ContentType` object is found, the shortcut method `get_objects_for_this_type()` will perform a `get` lookup and retrieve objects for that model class.

```python
In [8]: post_type.get_object_for_this_type(pk=1)
Out[8]: <Post: An Example Post>
```

Note that this is a shortcut to `get` on the `Post.objects` manager instance:

```python
In [9]: post_type.model_class().objects.get(pk=1)
Out[9]: <Post: An Example Post>

In [10]: post_type.get_object_for_this_type(pk=1) == post_type.model_class().objects.get(pk=1)
Out[10]: True
```

Other methods of loading objects (like `filter()` and `all()`) are similarly available – remember once you call `model_class()` it’s just like you’ve imported the model.

This is the extent of what is generally needed to be known to use contenttypes, but if you’re curious about the extra methods that are available, then you can read the [contenttypes framework documentation](https://docs.djangoproject.com/en/3.2/ref/contrib/contenttypes/#methods-on-contenttype-instances).

Now that we’ve seen how the contenttypes framework can let us dynamically access models, let’s get back to discussing generic relationships.

### Reading Question

What is the purpose of the `contenttypes` framework?

- **`It keeps track of all models installed in a Django project.`**
- It keeps track of only the default models installed in a Django project.
- It keeps track of only the user-defined models installed in a Django project.

> The `contenttypes` framework keeps track of **all** models installed in a Django project.
