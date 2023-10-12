# Codio Specific Setup

## Running Django in Codio

The changes on this page are done to allow Django to run on the Codio platform. By default, Django has strict security features that keep Codio from embedding Django.

The code samples below **only** apply for Codio. You **would not** make these changes when running Django outside of Codio.

Before setting up Django to run on Codio, you first need to import the `os` module.

```python
import os
```

The two biggest obstacles in getting Django to run inside Codio are recognizing the unique host name for each Codio project and cookies. The changes below will tell Django the exact host name of the Codio project and alter how Django handles cookies. Make sure your settings match the ones below.

```python
ALLOWED_HOSTS = ['*']
X_FRAME_OPTIONS = 'ALLOW-FROM ' + os.environ.get('CODIO_HOSTNAME') + '-8000.codio.io'
CSRF_COOKIE_SAMESITE = None
CSRF_TRUSTED_ORIGINS = ['https://' + os.environ.get('CODIO_HOSTNAME') + '-8000.codio.io']
CSRF_COOKIE_SECURE = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SAMESITE = 'None'
SESSION_COOKIE_SAMESITE = 'None'
```

Scroll down a bit and look for the definition of the variable `MIDDLEWARE`. Comment out the two lines that refer to `csrf`. CSRF stands for cross-site request forgery, which is a way for a malicious actor to force a user to perform an unintended action. Djano normally has CSRF protections in place, but we need to disable them. There are serious security implications to doing so, however your project on Codio is not publicly available on the internet. Comment out the two lines in the `MIDDLEWARE` setting as shown below.

```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
#     'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
#     'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

**Reminder:** these changes only apply to working with Django on Codio. **Do not** make these changes to a project you plan on making available on the internet.

## Reading Question

Why is it a bad idea to make the changes on this page to every Django project you create? **Hint,** there is more than one correct answer.

* [X] **These changes decrease the security of your website.**
* [X] **These changes are specific to the Codio platform, which you will not be using when building a production-ready website.**

> The changes on this page reduce security for a publicly facing website. Many of these changes are not needed since your website will not be on Codio.


```
Note: Do not modify your settings.py file when you are coding in your local machine.
```