# Formative Assessment 1

Drag the code blocks into the box below. Create a dropdown component using Bootstrap classes. The dropdown menu should have two items. **Hint** , not all of the blocks will be used, and the blocks must be properly indented.

Drag from here

* `<div class="dropdown-toggle">`
* `<li class="dropdown-item">Item 1</li>`
* `<ul class="dropdown-item">`
* `</div>`
* `<li class="dropdown-item">Item 2</li>`
* `<li class="dropdown">Item 1</li>`
* `<div class="dropdown">`
* `<ul class="dropdown-menu">`
* `<button class="dropdown-menu">Dropdown</button>`
* `</ul>`
* `<li class="dropdown">Item 2</li>`
* `<button class="dropdown-toggle">Dropdown</button>`


The correct answer is:

```html
<div class="dropdown">
  <button class="dropdown-toggle">Dropdown</button>
  <ul class="dropdown-menu">
    <li class="dropdown-item">Item 1</li>
    <li class="dropdown-item">Item 2</li>
  </ul>
</div>
```

* The container element (a `div` in this case) has the class `"dropdown"`
* The button element has the class `"dropdown-toggle"`
* The unordered list element has the class `"dropdown-menu"`
* The list elements have the class `"dropdown-item"`
