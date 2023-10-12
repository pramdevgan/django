# Project Setup

## Project Setup

Because this is an advanced Django course, we are not going to go over installing Django and starting a project. The GitHub repo that you forked is a starting point for the `blango` project.

Change in to the `blango` directory and start an app called `blog`.

```bash
cd blango
python3 manage.py startapp blog
```

As usual, you’ll need to add the `blog` app to your `INSTALLED_APPS` in your Django `settings.py` file.

## Open `settings.py`

Click the link below to open the `settings.py` file. You will now need to click between the tabs to toggle between the terminal and `settings.py`.

![Terminal and Settings.py Tabs](https://apollo-media.codio.com/media%2F1%2F7d7517a7f2c1e77f357724333c7dcbdf-b3b1f97bf84ba221.webp)

[Open settings.py]()

The `INSTALLED_APPS` variable should now look like this:

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
    "blog",
]
```





## Reading Question

Which Django command is used to star an app called `my_app`?

The correct command is:
```bash
python3 manage.py startapp my_app
```
Even though this is a Django project, the command starts with `python3`. Many of the commands used for this project make use of the `manage.py` file as well.
