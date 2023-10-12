# Formative Assessment 2

Drag the code blocks into the box below. Create the class `Song` model that has the following attributes (**in this order!** ):

* A reverse generic relationship with the `Artist` model
* A `title` field with a maximum length of 50 characters
* A `genre` field with a maximum length of 75 characters
* An `object_id` field

**Hint** , not all of the blocks will be used, and the blocks must be properly indented.

Drag from here

* object_id = models.PositiveIntegerField()
* genre = models.TextField(max_length=75)
* artist = GenericRelation(Artist)
* title = models.TextField(max_length=75)
* title = models.TextField(max_length=50)
* artist = models.ForeignKey(settings.AUTH_USER_MODEL, on_delete=models.CASCADE)
* genre = models.TextField(max_length=50)
* class Song():
* class Song(models.Model):

Construct your solution here


The correct answer is:

```python
class Song(models.Model):
  artist = GenericRelation(Artist)
  title = models.TextField(max_length=50)
  genre = models.TextField(max_length=75)
  object_id = models.PositiveIntegerField()
```

* Since `Song` is a model, it needs to inherit from `models.Model`
* Use `GenericRelation(Artist)` to create a reverse generic relationship with the `Artist` model
* Make sure `title` has `max_length=50` to set its maximum length to 50 characters
* Make sure `genre` has `max_length=75` to set its maximum length to 75 characters
