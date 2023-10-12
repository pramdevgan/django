# Formative Assessment 2

Choose the **safest** way to display user

```html
format_html("{} {} {}", title, first_name, last_name)
```

```html
mark_safe(f"{title} {first_name} {last_name}")
```

```html
f"{title} {first_name} {last_name}"
```

Here is the correct answer:

```python
format_html({} {} {}, title, first_name, last_name)
```

* Using `mark_safe` means that Django will not escape the text. If you have user-generated text, this could be way to inject malicious code into the website.
* Using `format_html` will automatically escape the text. Malicious code would not be executed.
* A simple f-string provides no protection from malicious code.
