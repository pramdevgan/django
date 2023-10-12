## Grid and Container System 1

In the bottom panel, select the tab with the terminal and start the Django dev server.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

In using Bootstrap so far, we’ve put the components directly inside the `<body>`. This means we end up with them directly against the side of the browser window. This can make our layout feel cramped. Bootstrap solves this with a number of container classes that can be applied to keep your content a consistent size regardless of the browser window size.

A containing element (like a `<div>`) can have the `container` class added. It will jump between a number of set sizes at certain breakpoints as the window resizes. For example, it’s the full width of the window at up to 576px wide, then jumps to 540px wide up to a 768px wide browser, at which point it resizes to 720px wide. This is easier to understand visually. So let’s set up one you can experiment with.

Open your `base.html` file (click the tab in the bottom panel). We’ll add a `<div>` around the content `block`. It should have the class `container bg-dark text-light`. The two latter classes are utility classes that Bootstrap provides, that set the container to have dark background, and light text, respectively, just so we can see what’s going on.

In addition, remove “Hello World” and nav bar from the file. After these modifications, this part of your `base.html` should look like this:

```html
<div class="container bg-dark text-light">
    {% block content %}

    {% endblock %}
</div>
```

Now update your `blog` `index.html`'s (click the tab in the bottom panel) content `block` to have a simple message in it, something like this is fine:

```html
{% block content %}
    <h2>Hello in a Container</h2>
{% endblock %}
```

Load the main page of your project in a browser and you should see something like this, at small sizes (click and drag the edge of the website to make it a smaller size):

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Container Small](https://apollo-media.codio.com/media%2F1%2Fc288027082f8dbfe3cd75da3e399e7cb-a2465ac470ac95cf.webp)

Notice the container spans the full width, but also has a small margin to add some space around its content.

As you resize the window, the container should jump between different widths as you cross the breakpoints.

![Bootstrap Container Medium](https://apollo-media.codio.com/media%2F1%2F959c5b62b24f89f19e47b4fbe72e7fa6-1846da75652a990c.webp)

Another option is to use the `container-fluid` class. This will make a container that’s full width at all sizes.

In `base.html`, try changing the class from `container` to `container-fluid` on your containing `<div>`, then refresh the page. You should see it stay full width at all sizes, but still with a margin around the content to keep it looking better.

![Bootstrap Container Fluid](https://apollo-media.codio.com/media%2F1%2F72ee586652caa832720f7d1659016b59-bd0fc1b041243536.webp)

There are many options for containers, and you can switch to one that stays full width to larger sizes, then starts jumping to set sizes at breakpoints. There are too many options to replicate here, and the [containers documentation](https://getbootstrap.com/docs/5.0/layout/containers/) lists all of them and the sizes at which they switch breakpoints.

In Blango, we’re going to stick with a `container-fluid` class, so you can leave that there, but we’re finished with the `bg-dark` and `text-light` utilities, so those classes can be removed.

Bootstrap (and many other HTML frameworks) use a grid system to lay out columns. Usually, this consist of *rows* that can contain up to 12 *columns* each. Rows are just `<div>`s with a `row` class; likewise columns are `<divs>` with a `col` class – although the width can be set manually, more on that in a minute.

In their simplest form, each column inside a row is of equal width. Let’s try this out by first building a row with three equal columns. We’ll also use some color utility classes to see the columns. Open the `blog` `index.html`. Remove everything in the ‘{% block content %}’ and then build a row with three columns, by putting in this HTML:

```html
<div class="row">
    <div class="col bg-primary">Column 1</div>
    <div class="col bg-danger">Column 2</div>
    <div class="col bg-success">Column 3</div>
</div>
```

You should see three equal size columns, like this:

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Columns Three Equal Sizes](https://apollo-media.codio.com/media%2F1%2F7e4e2b4c732848a327c841973b5a0b6b-6db08598e14b58c0.webp)

## Reading Question

What is the maximum number of columns in Bootstrap?

- ***`12`***
- 9
- 3
- 6

Bootstrap allows up to 12 columns in their grid system.