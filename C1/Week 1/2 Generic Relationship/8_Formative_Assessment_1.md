# Formative Assessment 1

Assume that you have a Django app named `music` and a model named `song`. Which line of code would load this `ContentType`?

```python
content = ContentType.objects.get(app_label="music", model="song")
```

```python
content = ContentType.objects.get(app_label="song", model="music")
```

```python
content = content_type.objects.get(app_label="music", model="song")
```


The correct answer is:

```python
content = ContentType.objects.get(app_label="music", model="song")
```

* `content_type` is not how you reference the `ContentType` model
* The app is named `music` so `app_label` must refer to `"music"`
* The model is named `song` so `model` must refer to `"song"`
