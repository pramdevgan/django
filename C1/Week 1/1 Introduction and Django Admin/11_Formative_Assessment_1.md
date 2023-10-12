# Formative Assessment 1

---

Which line of code will show the published date and then the title in a list of posts in the admin panel?

- ***`list_display = ('published_at', 'title')`***
- `list_display = ('published', 'title')`
- `list_display = ('title', 'published_at')`
- `list_display = ('title', 'published')`

The correct answer is:

```python
list_display = ('published_at', 'title')
```

The `Post` object does not have an attributed named `published`, so you need to use `published_at`. If you want the date to come first, `published_at` should come before `title`.
