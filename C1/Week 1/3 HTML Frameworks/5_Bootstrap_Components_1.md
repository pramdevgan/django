# Bootstrap Components 1

## Bootstrap Components 1

Bootstrap has a number of included components to add useful features to your website. There are quite a few, but here are some that are probably most useful (your mileage may vary based on the type of project you’re building!)

In this section we will show the HTML that is added to our template to demonstrate the component, and a screenshot of what it looks like. You can try it out on your own Blango project if you want. In the bottom panel, select the tab with the terminal and start the Django dev server.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

### Alerts

[Alerts](https://getbootstrap.com/docs/5.0/components/alerts/) are used to add an alert or message to a page, and can change color to indicate success, failure or warning. They consist of a `<div>` with an `alert` class and then a modifier class, like `alert-success`, `alert-warning`, etc. Add the following code to `{% block content %}` in the `index.html` file.

[Open index.html]()

```html
<div class="alert alert-success" role="alert">
  A simple success alert—check it out!
</div>
<div class="alert alert-danger" role="alert">
  A simple danger alert—check it out!
</div>
<div class="alert alert-warning" role="alert">
  A simple warning alert—check it out!
</div>
```

<details open=""><summary><strong>Refresh the Website</strong></summary>

Click on the blue, circular arrows to refresh the website.

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Alerts](https://apollo-media.codio.com/media%2F1%2F1b87d8beb1ae16e9f5727a9b39ba84aa-2004d2db00b1b82a.webp)

### Buttons

The [Button](https://getbootstrap.com/docs/5.0/components/buttons/) components allows for consistent looking buttons across browsers, with different coloring for primary, secondary, warning and error buttons. Buttons can be created from `<button>` or `<a>` elements and are done so with the `btn` class and then a modifer class, like `btn-primary`, `btn-secondary`, `btn-danger`, etc.

```html
<button type="button" class="btn btn-primary">Primary</button>
<a href="#" class="btn btn-secondary">Secondary</a>
<button type="button" class="btn btn-danger">Danger</button>
```

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Buttons](https://apollo-media.codio.com/media%2F1%2Fea72ad7e8afb0427fdc3a1d3f6fe5308-63e5b5df70ce9a33.webp)

Note that Bootstraps buttons look the same regardless of the element used to create them (`<a>` or `<button>`).

### Dropdowns

[Dropdowns](https://getbootstrap.com/docs/5.0/components/dropdowns/) are used when you want a dropdown menu from which you can select an option. It consists of `<div>` with the class `dropdown`. This `<div>` then contains: a Bootstrap button with class `dropdown-toggle` and special attribute `data-bs-toggle="dropdown"`; and a `<ul>` with class `dropdown-menu`. Bootstrap adds all the Javascript to make it interactive automatically. For accessibility, [ARIA](https://www.w3.org/TR/html-aria/) attributes are also used.

```html
<div class="dropdown">
  <button class="btn btn-secondary dropdown-toggle" id="dropdownMenuButton1" type="button" data-bs-toggle="dropdown" aria-expanded="false">
    BootStrap Dropdown
  </button>
  <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton1">
    <li><a class="dropdown-item" href="#">Item 1</a></li>
    <li><a class="dropdown-item" href="#">Item 2</a></li>
    <li><a class="dropdown-item" href="#">Item 3</a></li>
  </ul>
</div>
```

<details open=""><summary><strong>Refresh the Website</strong></summary>

Click on the blue, circular arrows to refresh the website.

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Dropdown](https://apollo-media.codio.com/media%2F1%2Fb137cfd5c795e740ecd8100e313b4629-1361ddcfad83dd2e.webp)

## Reading Question

How do you add a Bootstrap component to your HTML page?

- Use a special model
- **`Use a special class selector`**
- Use a special tag

In Bootstrap, you use regular HTML tags but pair them with a special class selector to get the desired look and feel of the HTML component.
