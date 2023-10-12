# Reverse Generic Relationships

## Reverse generic relationships

A disadvantage of the `GenericForeignKey` is that it can’t be queried against, so if you try something like this, you’ll get an exception (**Note,** the following is an example; you do not need to enter this code):

```python
c = Comment.objects.filter(content_object=p)
# stack trace removed
django.core.exceptions.FieldError: Field 'content_object' does not generate an automatic reverse relation and therefore cannot be used for reverse querying. If it is a GenericForeignKey, consider adding a GenericRelation.
```

Begin by starting a Django management Python shell:

```shell
python3 manage.py shell
```

We need to `filter()` against the `content_type` and `object_id` field directly. For example:

In [**1**]: **from** django.contrib.contenttypes.models **import** ContentType

In [**2**]: **from** blog.models **import** Post, Comment

In [**3**]: post_type = ContentType.objects.get_for_model(Post)

In [**4**]: p = Post.objects.first()

In [**5**]: c = Comment.objects.**filter**(content_type=post_type, object_id=p.pk)

In [**6**]: c
Out[**6**]: <QuerySet [<Comment: Comment **object** (**1**)>, <Comment: Comment **object** (**2**)>]>

This can be a bit tedious, but we know it will work for all models. If there’s a model whose generic related objects you’ll be querying quite often, you can consider setting up a `GenericRelation` field (imported `from django.contrib.contenttypes.fields`) on it. `GenericRelation` takes one argument: the generic model class to map to.

Our `Post` model should be updated like so:

```python
from django.contrib.contenttypes.fields import GenericRelation
# other imports ommited


class Post(models.Model):
    # existing fields omitted
    comments = GenericRelation(Comment)
```

This is only possible if it’s a model under your control, so we can use it to make fetching comments for a `Post` simple, but we can’t edit the `User` model so easily.

Now fetching the `Comment`s for a `Post` is simple. The `comments` attribute acts like a `RelatedManager` allowing you to query, `filter()`, `add()`, `create()` and `remove()` `Comment`s to a `Post`. Let’s see a short example of how to use it.

***Migrations***

```shell
python3 manage.py makemigrations
python3 manage.py migrate
```

Once again start a Django Python shell in the terminal:

```bash
python3 manage.py shell
```

Then perform the required imports:

```python
In [1]: from django.contrib.contenttypes.models import ContentType

In [2]: from blog.models import Post, Comment
```

Now let’s get all the `Comment` objects for a `Post`:

```python
In [3]: p = Post.objects.first()
  
In [4]: p.comments.all()
Out[4]: <QuerySet [<Comment: Comment object (1)>, <Comment: Comment object (2)>]>
```

Then, let’s remove the first `Comment` from the `Post`:

```python
In [5]: c1 = p.comments.all()[0]
  
In [6]: p.comments.remove(c1)
  
In [7]: p.comments.all()
Out[7]: <QuerySet [<Comment: Comment object (2)>]>
```

That’s most of what you need to know for how to use the contenttypes framework. The [full documentation](https://docs.djangoproject.com/en/3.2/ref/contrib/contenttypes/) is useful if you want to know about how to use custom queries in `GenericRelation` fields, or how to aggregate generic objects.

Let’s return to our project and add the `Comment` model.

### Reading Queestions

What is the advantage of using a reverse generic relationship between the `Post` and `Comment` models?

- ***`You can only query against the Comment model`***
- `You can query against both the Comment and Post models`
- `You can only query against the Post model`

When you have a generic relationship between the `Comment` and `Post` models and a reverse generic relationship between the `Post` and `Comment` models you can query against both the `Comment` and `Post` models.
