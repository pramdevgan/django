# Formative Assessment 2

Fill in the blanks below so that:

* When the breakpoint identifier is `sm` the two columns are stacked on top of each other.
* When the breakpoint identifier is `md` column 1 has 66% of the width.
* When the breakpoint identifier is `lg` column 2 has 66% of the width.


The correct answer is:

```html
<div class="row">
    <div class="col-sm-12 col-md-8 col-lg-4 bg-primary">Column 1</div>
    <div class="col-sm-12 col-md-4 col-lg-8 bg-danger">Column 2</div>
</div>
```

* The width of columns can be 1 to 12. When the number is larger than 12, the columns become stacked on top of one another.
* By setting `col-sm` to 12, this ensures one will be on top of the other.
* The first column should take up 66% of the screen when the breakpoint is `md`. If the maximum width is 12, then 66% of that would be a width of 8. That means the first column should be `col-md-8` and the second column should be `col-md-4` to fill up the remaining space.
* To make the second column take up 66% of the screen when the breakpoint is `lg`, set it to `col-lg-8` and set the first column to `col-lg-4`.
