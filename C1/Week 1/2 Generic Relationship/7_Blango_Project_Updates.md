# Blango Project Updates

## Blango Project Updates

We’ve discussed the theory behind generic relationships and seen some examples of how to use them. Now it’s time to add comments to Blango. Do this by:

* Creating a `Comment` model. It should have a `creator` field to store the user who created it, plus fields to store the created time and modified time. Don’t forget the generic relationship fields.

```python
class Comment(models.Model):
    creator = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
    content = models.TextField()
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey("content_type", "object_id")
    created_at = models.DateTimeField(auto_now_add=True)
    modified_at = models.DateTimeField(auto_now=True)
```

* Add a `comments` `GenericRelation` field on `Post` back to `Comment`. This will make it easier to find comments for a post.

```python
class Post(models.Model):
    author = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.PROTECT)
    created_at = models.DateTimeField(auto_now_add=True)
    modified_at = models.DateTimeField(auto_now=True)
    published_at = models.DateTimeField(blank=True, null=True)
    title = models.TextField(max_length=100)
    slug = models.SlugField()
    summary = models.TextField(max_length=500)
    content = models.TextField()
    tags = models.ManyToManyField(Tag, related_name="posts")
    comments = GenericRelation(Comment)

    def __str__(self):
        return self.title
```

* Add the `Comment` model to the Django admin by importing and registering it in the `admin.py` file.

```python
from django.contrib import admin
from blog.models import Tag, Post, Comment

class PostAdmin(admin.ModelAdmin):
    prepopulated_fields = {"slug": ("title",)}

# Register your models here.
admin.site.register(Tag)
admin.site.register(Post, PostAdmin)
admin.site.register(Comment)
```

* Don’t forget to run the `makemigrations` and `migrate` management commands after all this.

```bash
python3 manage.py makemigrations
python3 manage.py migrate
```

## Warning Message

When you try to migrate the model changes, Django gives you a warning message.

```markdown
You are trying to add the field 'created_at' with 'auto_now_add=True' to comment without a default; the database needs something to populate existing rows.

 1) Provide a one-off default now (will be set on all existing rows)
 2) Quit, and let me add a default in models.py
Select an option:
```

This happens because the `Comment` model was first created without `created_at` and `modified_at`. The comments in the database do not have these fields. Django wants to know how to treat `created_at` since it needs a value. Enter `1` at the prompt. Django suggests using `timezone.now` as the value. Press `Enter`.

```markdown
Please enter the default value now, as valid Python
You can accept the default 'timezone.now' by pressing 'Enter' or you can provide another value.
The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now
Type 'exit' to exit this prompt
[default: timezone.now] >>>
```


## Reading Question

Fill in the blanks below.


* Using `GenericRelation`indicates a **reverse generic** relationship.
* Using `GenericForeignKey` indicates a **generic** relationship.
