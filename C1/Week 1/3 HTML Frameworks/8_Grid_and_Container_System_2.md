# Grid and Container System 2

## Grid and Container System 2

In the bottom panel, select the tab with the terminal and start the Django dev server.

```bash
python3 manage.py runserver 0.0.0.0:8000
```

Columns can also have their width set manually with width modifier column classes. Use classes from `col-1` to `col-12` to set a width of between 1 and 12 columns. You can set a manual width on any number of columns in a row, and any without a width will adjust themselves to be equally sized in the remaining space. If columns start taking up a width more than 12, they start stacking vertically.

For example, we could set the left column to have a size of 6, meaning it would take up half of the 12 columns. The middle and right column would then take up a quarter of the width each. Let’s try that out, change the first column to have the class `col-6`. Add the following code to `{% block content %}` in the `index.html` file.

```html
<div class="row">
    <div class="col-6 bg-primary">Column 1</div>
    <div class="col bg-danger">Column 2</div>
    <div class="col bg-success">Column 3</div>
</div>
```

Once you save and refresh the page, it should look like this:

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Columns Wide Left Column](https://apollo-media.codio.com/media%2F1%2F76f286ead124d0bb30c5755bdcc2e04d-9c5ed088ce857159.webp)

Each row’s columns act independently, so you can have 3 columns in one row, then 8 in the next, then just 1 in the 3rd row, for example.

The last thing to see with columns is that we can have columns of different widths for different breakpoints (screen widths). This means we can have our content look good at a certain width, and just have it stack vertically instead of getting squished at small browser window sizes. For example, a 6-wide column takes up 50% of the grid width, or 600px on a 1200px wide browser window. On a 600px wide browser, we’d want it to be 12-wide, or take up 100% of the grid, for the same absolute column size. Note that these sizes were chosen arbitrarily as no Bootstrap breakpoint is exactly twice as wide as another, but hopefully it illustrates the concept.

We can set different column widths at different breakpoints with breakpoint specific classes. Bootstrap’s breakpoint tiers and sizes are:

* Extra small (xs) <576px
* Small (sm) ≥576px
* Medium (md) ≥768px
* Large (lg) ≥992px
* Extra large (xl) ≥1200px
* Extra extra large (xxl) ≥1400px

The breakpoint identifier (the letters in the brackets) can be used in the column class to set its behaviour in that breakpoint. For example, these columns will behave as normal 1/3rd width columns above the medium breakpoint. Below 768px browser size, they become full-width and stack. Add the following code to `{% block content %}` in the `index.html` file.

```html
<div class="row">
    <div class="col-md bg-primary">Column 1</div>
    <div class="col-md bg-danger">Column 2</div>
    <div class="col-md bg-success">Column 3</div>
</div>
```

Click and drag the right edge of the website to change its width. This is how they look below the medium breakpoint width:

<details><summary><strong>Refresh the Website</strong></summary>

##

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Vertical Stacked Columns](https://apollo-media.codio.com/media%2F1%2Fa2c54afe6bab2ea984d1a2b2ea611300-73766c0e8ce452a6.webp)

And above the medium breakpoint width:

![Bootstrap Medium Columns in Screen Greater than 768 pixels](https://apollo-media.codio.com/media%2F1%2F3967b6cb1e5ebf0b586dd339795545a4-085152be5c0884d2.webp)

Manual width columns and breakpoints can also be combined, and even multiple classes at once to set different manual sizes at different breakpoints. This final example (add the following code to `{% block content %}` in the `index.html` file):

* at the extra small breakpoint, stacks the columns.
* between the small and medium breakpoints, sets the left column to 10, and middle column to 2. Since this adds to 12 the final column is stacked.
* at the medium breakpoint and above, sets the left column to 6, the middle column to 2, and the right column takes up the remaining space (4).

```html
<div class="row">
    <div class="col-xs-12 col-sm-10 col-md-6 bg-primary">Column 1</div>
    <div class="col-xs-12 col-sm-2 col-md-2 bg-danger">Column 2</div>
    <div class="col bg-success">Column 3</div>
</div>
```

This is an example you should try for yourself and adjust the size up and down to see how it behaves. Here’s a screenshot in the small breakpoint:

<details><summary><strong>Refresh the Website</strong></summary>

![blue, circular arrows](https://apollo-media.codio.com/media%2F1%2F365ca2d115d614cf9dd7fa0bfe3e8059-196204e3b3c73892.webp)

</details>

![Bootstrap Different Breakpoints](https://apollo-media.codio.com/media%2F1%2F5a9d6e2c1410264fbcff15c57a84288b-25440126fa8aa1c1.webp)

As you can see, the grid system is very flexible and very powerful, once you get the hang of it. The [grid documentation](https://getbootstrap.com/docs/5.0/layout/grid/) contains all the options and info about the breakpoints, and includes different ways to align and justify your content too. But these basics should cover most of your use cases.

Throughout the course we may introduce some other small utility classes the Bootstrap provides, but we will explain their purpose when we do. Luckily they’re quite easy to pick up.
Now that we know how to layout our page with Bootstrap, in the next section we’re going to look at Django’s custom filters.


## Reading Question

Fill in the blanks below.

* A **breakpoint** is a point at which your content will resize so that layout responds to screensize.
* A **breakpoint identifier** tells a class which breakpoint to use for layout.
* A column width of 6 will be **50%** of the width of the screen.

A **breakpoint** is the screen size at which the layout changes. This way content is easy to read no matter if you are looking at the website on a desktop, tablet, or phone.

A **breakpoint identifier** tells Bootstrap which layout to use. This is done by a two-letter combination like `md` or `xl`.

Bootstrap has up to 12 columns, so a column width of 6 takes 50% (6/12 = 0.5) of the width of the screen.
