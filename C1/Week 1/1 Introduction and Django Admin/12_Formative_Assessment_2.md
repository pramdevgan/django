# Formative Assessment 2

---

Which line of code sets the maximum length of a title to 125 characters.

- ***`title = models.TextField(max_length=125)`***
- `title = models.TextField(max_length=25)`
- `title = models.TextField(length=125)`
- `title = models.TextField(max=125)`

The correct answer is:

```python
title = models.TextField(max_length=125)
```

Make sure the numeric value is `125`. The correct name for maximum length is `max_length`.
