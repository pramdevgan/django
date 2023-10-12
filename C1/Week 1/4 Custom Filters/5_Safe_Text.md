# Safe Text

## Safe Text

Django is very safe and secure by default. Any variables that are rendered automatically have their HTML entities escaped, to prevent malicious HTML being injected into templates unexpectedly.

For example, the string `<a href="#">Click me!</a>` would be rendered as:

```html
<a href="#">Click me!</a>
```

This prevents [Cross Site Scripting (XSS)](https://owasp.org/www-community/attacks/xss/) and other types of attacks to your site, in which visitors can be redirected to malware or have the page content changed unexpectedly, due to bad HTML being supplied by users.

What if we need to use HTML entities in our output value? There are a couple of ways. Django has the built in filter [`safe`](https://docs.djangoproject.com/en/3.1/ref/templates/builtins/#safe) which skips the encoding, if you know a string is safe to output verbatim. Generally you’d only want to use this with your own values, and not mark any user-supplied data as "safe".

The other way is to use a “safe” string. This is a [special string class](https://docs.djangoproject.com/en/3.2/ref/utils/#django.utils.safestring.SafeString) that is not escaped when rendered. We’ll look at how to mark normal strings as safe soon.

But, what if you need to output a mix of safe HTML that you’ve defined, and unsafe data from a user? This discussion is getting a bit abstract and theoretical, so let’s look at a real problem in the context of Blango.

We want to have the author’s name be a clickable link to email them, if they have an email address in their profile. For reference, this is a `mailto` link, like this:

```html
<a href="mailto:ben@example.com">ben</a>
```

To achieve this we need to update the `author_details` function to work with a variety of combinations of user data. We should wrap the user’s name (either their username or full name) in an `<a>` tag only if they have an email address. The output string will be composed of both safe data that we can control (namely the HTML that we write) and unsafe data that the user has provided (their name and email address). We’ll be building up this functionality a step at a time to cement the concepts.

This time we’ll be building up the clickable link to email. First let’s take a naïve approach at updating the `author_details` function just to return the HTML. While this won’t give us a clickable link, it’s good to see Django’s safe-by-default approach.

<details><summary><strong>Email Addresses</strong></summary>
Login to the Django admin page to verify that users have created an email address for their profile. If not add one. Without an email address, you will not be able to see the changes being made to your blog.
</details>

## Try It Out

Modify the `author_details` function so that the author name `ben` becomes:

```html
<a href="mailto:ben@example.com">ben</a>
```

<details><summary><strong>Solution</strong></summary>
Even the code you wrote works, you should copy and paste this to replace it as we'll be adding to it piece by piece. Replace your `author_details` function with this code:

```python
@register.filter
def author_details(author):
    if not isinstance(author, user_model):
        # return empty string as safe default
        return ""

    if author.first_name and author.last_name:
        name = f"{author.first_name} {author.last_name}"
    else:
        name = f"{author.username}"

    if author.email:
        email = author.email
        prefix = f'<a href="mailto:{email}">'
        suffix = "</a>"
    else:
        prefix = ""
        suffix = ""

    return f"{prefix}{name}{suffix}"
```

</details>

Start the dev server in your browser you’ll see something like this:

START DEV SERVER

[View Blog]()

![Escaped Email Link](https://apollo-media.codio.com/media%2F1%2Fb0a3715705b0b7c611db9c87a86da7d8-4c76a4240fe5cbda.webp)

One way to “fix” this might be to use the `safe` filter in our template, doing something like `{{ post.author|author_details|safe }}`. This would give us a clickable link, but is definitely **NOT** safe! Because we’re marking the whole string as safe, we’d also be outputting any malicious HTML that could have been injected into the user’s name or email address.

To have good output that’s *really* safe, we need to first escape the dangerous parts of the text that we’re dealing with. Then, mark the whole string as safe so that only the HTML we trust is output verbatim.

Escaping strings is done with the [`django.utils.html.escape`](https://docs.djangoproject.com/en/3.2/ref/utils/#django.utils.html.escape) function. This will encode the HTML entities in a string. Once we have escaped only the dangerous values, we can mark a string as safe with the [`django.utils.safestring.mark_safe`](https://docs.djangoproject.com/en/3.2/ref/utils/#django.utils.safestring.mark_safe) function. Once a string has been marked as safe, Django won’t escape it again when outputting in a template, so use with caution.

## Try It Out

Let’s update the `author_details` function to make its output both clickable and safe. See if you can make the changes before checking the provided code:

* Import the `django.utils.html.escape` function and use it to escape the dangerous user supplied data (name, username and email).

<details><summary><strong>Solution</strong></summary>
Here's the solution; first add these imports at the start of the file:

```python
from django.utils.html import escape
from django.utils.safestring import mark_safe
```

</details>

* Import the `django.utils.safestring.mark_safe` function and mark the final string safe.

<details><summary><strong>Solution</strong></summary>
Then update your filter function:

```python
@register.filter
def author_details(author):
    if not isinstance(author, user_model):
        # return empty string as safe default
        return ""

    if author.first_name and author.last_name:
        name = escape(f"{author.first_name} {author.last_name}")
    else:
        name = escape(f"{author.username}")

    if author.email:
        email = escape(author.email)
        prefix = f'<a href="mailto:{email}">'
        suffix = "</a>"
    else:
        prefix = ""
        suffix = ""

    return mark_safe(f"{prefix}{name}{suffix}")
```

</details>

Now we know the whole string is safe to be marked as safe, because it’s composed only of HTML that we’ve defined, and all user supplied data is escaped.

Try it out by refreshing the post list. Any users with email addresses should now be clickable.

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

[]()

</details>

![Clickable Email Link](https://apollo-media.codio.com/media%2F1%2F7a550452dfb91abf5b80a7ccd5101b94-66f05c97edecae84.webp)

If you really want to be sure that the output is safe, try changing one of the user’s first names to a small piece of HTML, and refreshing the post list. You should see that the HTML is escaped and thus readable, rather than being rendered verbatim and affecting the page’s markup.

![Clickable Escaped Email Link](https://apollo-media.codio.com/media%2F1%2Feb64537300092906c1a2a715b3a14a87-282f1f45e7240a36.webp)

Now that we’ve had a look at what’s happening at a low level, we can introduce a helper function that adds more security. The [`django.utils.html.format_html`](https://docs.djangoproject.com/en/3.2/ref/utils/#django.utils.html.format_html) is the preferred way of building HTML strings as it escapes values and marks strings safe in a single step. For example, when we build the opening `<a>` tag for the email link, we are escaping the email address on the line before and then putting it in the string. If we forgot to do the escape step, it could be dangerous.

So instead of creating the prefix like this:

```python
email = escape(author.email)
prefix = f'<a href="mailto:{email}">'
```

We can do it in a single step:

```
prefix = format_html('<a href="mailto:{}">', author.email)
```

`format_html` works similarly to the built in `str.format` method, except each argument is automatically escaped before being interpolated.

Let’s update our `author_details` function to use it now. First we can remove our `escape` and `mark_safe` imports as `format_html` does this for us. Then, we can import `format_html` instead:

```python
from django.utils.html import format_html
```

Then we’ll use it in our filter function:

```python
@register.filter
def author_details(author):
    if not isinstance(author, user_model):
        # return empty string as safe default
        return ""

    if author.first_name and author.last_name:
        name = f"{author.first_name} {author.last_name}"
    else:
        name = f"{author.username}"

    if author.email:
        prefix = format_html('<a href="mailto:{}">', author.email)
        suffix = format_html("</a>")
    else:
        prefix = ""
        suffix = ""

    return format_html('{}{}{}', prefix, name, suffix)
```

## Check Your Code

To check the clickable email link, you must first open your blog in a new tab. Click the blue arrow (shown below). Then click on the author of the blog post. Your computer should start the email process.

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

If you closed those tabs, you can start the dev server again.

START DEV SERVER

[View Blog]()

`format_html` can be called with just one argument (like creating the closing `</a>`) tag, in which case the string is just marked as safe. At the end of the function, we’re passing in already escaped and safe parameters, `prefix` and `suffix`. Since these are already marked as safe, they won’t be re-escaped.

To summarize this section, as the security aspect is very important:

* By default, Django will escape all output in templates before rendering, so it’s secure against XSS and other injection attacks automatically.
* Don’t use the `safe` filter or mark a string as safe (with `mark_safe`) unless you’ve constructed all of that string yourself. A string that is composed of any form of use input should be considered unsafe.
* Strings should only be marked safe if any parts that have come from a user have been passed through the `escape` function.
* To be safer and use less code, use the `format_html` function, which escapes strings parameters before interpolation.

We’re going to close this section by looking at filters with arguments.

## Reading Question

Fill in the blanks below.

* The **escape** function converts HTML into something that cannot be executed.
* The **safe** filter should be used when you know for certain that the HTML content poses no risk to your site.
* The goal is to protect websites from **XSS** attacks
* The correct answers are:The goal is to protect websites from **XSS** attacks

<br><br>

The correct answers are:
*  The **escape** function converts HTML into something that cannot be executed.
  * The **safe** filter should be used when you know for certain that the HTML content poses no risk to your site.
  * The goal is to protect websites from **XSS** attacks.
