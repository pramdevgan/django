# Bootstrap Components 2

## Bootstrap Components 2

### Modals

In the bottom panel, select the tab with the terminal and start the Django dev server.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

If you want to display a pop up screen on the page, use a [Modal](https://getbootstrap.com/docs/5.0/components/modal/). You can set a title, body and footer, plus lots of options for how it behaves.

To set it up, you’ll need something to trigger the modal to open, like a `<button>`. Set its `data-bs-toggle` attribute to “modal” and `data-bs-target` to a CSS selector for the modal to open (for example `#example-modal` will open the modal with ID `example-modal`).

See the code below for an example of the button and the modal container and content – it must be contained in a `<div>` with class `modal`. Add the following code to `{% block content %}` in the `index.html` file.

```html
<button type="button" class="btn btn-primary" data-bs-toggle="modal" data-bs-target="#example-modal">
  Open Modal
</button>

<div class="modal" id="example-modal" tabindex="-1" aria-labelledby="example-modal-label" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="example-modal-label">Modal Title</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        Modal Body
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>
```

Here’s how the modal looks open:

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Modal](https://apollo-media.codio.com/media%2F1%2Fc5d0ade6063cc26d93f5c3b9ee97f397-7aed10fb0f6c3370.webp)

You can see the *Open Modal* button in the background.

### Navbar

[Navbars](https://getbootstrap.com/docs/5.0/components/navbar/) are essential on most pages. They are usually placed on the top of the page, and contain links to the main pages in your site. They have a lot of options for customization, which are better explained in the official docs, but here’s a short example. Add the following code to `{% block content %}` in the `index.html` file.

```html
  <nav class="navbar navbar-expand-sm navbar-light bg-light">
    <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent"
                aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li class="nav-item">
                    <a class="nav-link active" aria-current="page" href="#">Home</a>
                </li>
                <li class="nav-item">
                    <a class="nav-link" href="#">Link</a>
                </li>
            </ul>
        </div>
    </div>
</nav>
```

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Navbar](https://apollo-media.codio.com/media%2F1%2F61e2322581c39e65cc3b33ca188eccad-788a5025e29cc9f3.webp)

Note that your output does not match the image above. That is because the navbar has been placed into the `base.html` template directly inside the `<body>`, so that it appears below the *Hello, world!* text. Go into `base.html` and move the `<h1>` tag with `Hello, world!` to below the `{% block content %}` and refresh the page.

### Pagination

The last component we’ll look at is used for [pagination](https://getbootstrap.com/docs/5.0/components/pagination/). It’s used to display an unordered list (`<ul>`) as a horizontal set of buttons, and intended for showing the current page and switching pages.

The `<ul>` element should have the class `pagination`, and the `<li>` elements it contains will have the class `page-item`. You can also add the class `disabled` to disable an item and make it unclickable, or add the class `active` to highlight it to show the current page. You can see an example of both of those here. Add the following code to `{% block content %}` in the `index.html` file.

```html
<ul class="pagination">
    <li class="page-item disabled">
        <a class="page-link" href="#" tabindex="-1" aria-disabled="true">Previous</a>
    </li>
    <li class="page-item"><a class="page-link" href="#">1</a></li>
    <li class="page-item active" aria-current="page">
        <a class="page-link" href="#">2</a>
    </li>
    <li class="page-item"><a class="page-link" href="#">3</a></li>
    <li class="page-item">
        <a class="page-link" href="#">Next</a>
    </li>
</ul>
```

Here’s how it displays:

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Pagination](https://apollo-media.codio.com/media%2F1%2Fd94756a81efbbf04d1c9f9633a869166-4a2c53b5be0274e5.webp)

There are quite a few more components available, and it is worth browsing the Bootstrap documentation to see which components will work best for your particular needs.

Now we’ll have a look at how to lay out the page with the Bootstrap grid system.


## Reading Question

Which component is a pop-up screen on a page?

- **`Modal`**
- Nav Bar
- Pagination


Modal components are pop-up screens on a webpage.

A nav bar is component (typically at the top) that helps you navigate to the main pages of a website.
Pagination is a component that has a subset of the total content. You can navigate to the next page to see more content.
