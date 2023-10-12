# Generic Relationships

To explain the importance of generic relationships, let’s use a concrete example. In a blog you might want someone to be able to leave comments. We could accomplish this with a `Comment` model with a `ForeignKey` to a particular `Post`. The model might look something like this:

```python
class Comment(models.Model):
    creator = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    content = models.TextField()
    post = models.ForeignKey(Post, on_delete=models.CASCADE)
```

It would be great though, if as well as being able to comment on a `Post`, you could also comment on an author.

This is not so easy to do. One way could be to add another `ForeignKey` on `Comment` that points to the author (`User`) being reviewed. The `Comment` model could be updated to be something like this:

```python
class Comment(models.Model):
    creator = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    content = models.TextField()
    post = models.ForeignKey(Post, on_delete=models.CASCADE, null=True)
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE, null=True)
```

But this would end up being confusing:

* Both `post` and `author` fields can be `null` now, which means that the database will allow us to insert a `Comment` that’s not mapped to any object (they could both be null). Before, when we only mapped to `Post`s, the `post` field did not allow `null` and so the database would enforce consistency.
* Likewise, `post` and `author` could both be populated. This would mean the `Comment` applies to both, which might not make sense.
* We’d need extra code to check and query the right field when fetching the `Comment`s, based on which context we are in (`Post` or `Author`).
* If we ended up adding some other model, and wanted to allow comments on it, we’d need yet another field to store this information.

## Django Permissions

The Django permissions system uses the *contenttype* framework, as it provides a generic way to set permissions on any model that has been added to the project. You can imagine how complex it would be to set up permissions without this kind of generic system.

By utilizing `ContentType` we can allow a model to be related to any number of models by just adding three attributes to a Model:

* A `ForeignKey` field that points to a `ContentType`. Normally this is called `content_type`
* A `PositiveIntegerField` that stores the primary key of the related object. Normally this is called `object_id`
* A `GenericForeignKey` field, a special type of field that will look up the object from the other two new fields.

Let’s look at how to implement this on the `Comment` model (declare `Comment` before `Post`). Something like:

```python
from django.contrib.contenttypes.fields import GenericForeignKey
from django.contrib.contenttypes.models import ContentType


class Comment(models.Model):
    creator = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    content = models.TextField()
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey("content_type", "object_id")
```

<details><summary><strong>Migrations</strong></summary>

Don't forget to run migrations before continuing.
```python
    python3 manage.py makemigrations
    python3 manage.py migrate
```

</details>

Note that we set `content_object` with two arguments: `GenericForeignKey("content_type", "object_id")`. These are the names of the fields on the model that contain the `ContentType` and related object’s ID, respectively. If these fields are called `content_type` and `object_id` then the arguments can be omitted (that is, in our case, using it like `content_object = GenericForeignKey()` would behave exactly the same.

Storing a value in a `GenericForeignKey` field is similar to a normal `ForeignKey`: just assign the object to it. The `GenericForeignKey` field takes care of storing the right `ContentType` and object PK into the `content_type` and `object_id` fields.

Begin by starting a Django management Python shell:

```bash
python3 manage.py shell
```

You can make a `Comment` on a `Post` like this:

```python
In [1]: from blog.models import Post, Comment
  
In [2]: from django.contrib.auth.models import User
  
In [3]: p = Post.objects.first()
  
In [4]: u = User.objects.first()
  
In [5]: c1 = Comment(creator=u, content="What a great post!", content_object=p)
  
In [6]: c1.save()
  
In [7]: c1.content_object
Out[7]: <Post: An Example Post>
```

And similarly, we can add a comment on a `User`.

```python
In [8]: c2 = Comment(creator=u, content="I like myself!", content_object=u)

In [9]: c2.save()

In [10]: c2.content_object
Out[10]: <User: username>
```

Note that this is a bit of strange comment, since there’s currently only one user in the system! But, you can see the same method of setting and getting the `content_object` applies regardless of the model class on the other side.

Generic relationships can also be added using the Django admin, but it is not very friendly as you need to enter the PK of the related object manually (notice the *Object_id* field in the screen shot below).

![Generic Relationships Admin Panel](https://apollo-media.codio.com/media/1/59b904a54e744457357bbe0e66981746-b34d44f02deec769.webp)

Now that we know how to create generic related objects, let’s see how to fetch them, with reverse generic relationships.

## Reading Question

Fill in the blanks below.

- A **foreign key** specifies a relationship with a single model.

- A **generic foreign key** specifies a relationship with many models.
