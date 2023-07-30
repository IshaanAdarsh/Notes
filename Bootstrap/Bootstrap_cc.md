# Bootstrap:
- CSS framework directed at responsive, mobile-first front-end web development

## Quick Start:
- Add the following links to the <head> tag:
```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-4bw+/aepP/YC94hEpVNVgiZdgIC5+VKNBQNGCHeKRQN+PtmoHDEXuppvnDJzQIu9" crossorigin="anonymous">
<script defer src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js" integrity="sha384-HwwvtgBNo3bZJJLYd8oVXjrBZt8cqVSpeBNS5n7C8IVInixGAoxmnlMuBnhbgrkm" crossorigin="anonymous"></script>
```
> Add defer attribute so it works properly.

## Bootstrap Structure:
```html
container
└── row
    └── column
        └── box
```
### Containers & Breakpoint:
- Containers are used to contain, pad, and (sometimes) center the content within them.
  - Whatever breakpoint we set in the container class, the point before the (md<lg) will be fluid and after will be a set hard codded breakpoint.
```html
<div class="container">default .container class is a responsive, fixed-width container, meaning its max-width changes at each breakpoint.</div>
<div class="container-sm">100% wide until small breakpoint</div>
<div class="container-md">100% wide until medium breakpoint</div>
<div class="container-lg">100% wide until large breakpoint</div>
<div class="container-xl">100% wide until extra large breakpoint</div>
<div class="container-xxl">100% wide until extra extra large breakpoint</div>
<div class="container-fluid">Use .container-fluid for a full width container, spanning the entire width of the viewport.</div>
```
## Grid System:
### Row:
- A row in Bootstrp is using Flexbox to lay everything out.
```html
<div class="row row-cols-2 row-cols-lg-2 g-2">
// if we want to have a 2 column grid. the colums below will adjust accordingly
// Sets a specific condition for greater or equal to large.
// Gaps between rows, ranges from 0-5 (0-no gap and 5-maximum possible gap)
  // gy -> y-axis and gx -> x-axis

  <div class="col">
    <div class = "box"></div>  
  </div>
  <div class="col">
    <div class = "box"></div>  
  </div>
</div>
```
### Column:
- We provide different colums sizing to take up respective space in the row (1-12)
- If we go over 12, the next box wraps to the next row.
```html
<div class="row">
  <div class="col-1">
    <div class = "box">Gives it one out of the 12 total size of the row</div>  
  </div>
  <div class="col-auto">
    <div class = "box">Adjusts acording to the text supplied in the Box</div>
  </div>
  <div class="col">
    <div class = "box">If no proper sizing is given it adjust automatically, using flexbox.</div>
  </div>
  <div class="col-lg-4 col-8">
    <div class = "box">Give a 4 column width when greater or equal to large but blow this, it goes back to 8 columns. lg-4 overwrites the original command.</div>
  </div>

  // Offset
  <div class = "col-3 offset-3">
    <div class = "box">Offsets or moves the bock 3 columns to the right (creates space)</div>
  </div>
</div>
```

## [Table](https://getbootstrap.com/docs/5.0/content/tables/):
- could apply styling to entire table, row , column or cell by plaing class attribute inside it.
```html
 <div class="container">
      <table class="table table-danger">
      // table class adds the bootstrap to regular table
      // table-colour -> danger - light red bg , primary - light blue bg
      // table-colour-column -> adds atribute to the column
      // table-responsive -> prefered or else the table overflows
        <thead>
          <tr>
            <th>First</th>
            <th>Last</th>
            <th>Age</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Kyle</td>
            <td>Cook</td>
            <td>69</td>
          </tr>
        </tbody>
      </table>
  </div>
```

## [Form](https://getbootstrap.com/docs/5.0/forms/overview/)
```html
// Simple Form
<div class-"container")
    <form>
    <label for= "email" class = "form-label">Email</label>
    <input type="email" id="email" class = "form-control form-contro-lg">
    // Input goes to the full size of the page
    // Could adjust the size of the form control according to needs
    <button>Submit</button>
    </form>
</div>

// Disable the input:
<input type="email" id="email" class = "form-control" disabled>
    // The box gets greyed out and no pointer

// Readonly:
<input type="email" id="email" class = "form-control" value = "dickface@gmail.com" readonly>
    // The box gets a value assigned and cant be edited.

// Plain Text screen:
- If you want to sho only plain text on the screen could use class = "form-control-plaintext"

// Colour Picker:
<input type="color" id="email" value ="email@gmall.com" class="form-control form-control-color">

// Range:
<input type="range" id="email" value ="email@gmall.com" class="form-range">
    // Dont add form-control class as it looks bad

// Select Box:
<select class="form-select">
    <option>One</option>
    <option>Two</option>
</select>

// CheckBox:
// Label is after the input and add "form-check-input" for the above class.
// Keep the input and label inside a form-check Div.
<div class="form-check">
    <Input type="checkbox" Id="email" class="form-check-input" />
    <label for="email" class-"form-check-label">Email</label>
</div>
<button>Submit</button>

// Toggle Switch:
// COuld apply inline checkboxes by siong the "form-check-inline"
<div class="form-check form-switch form-check-inline" >
    <Input type="checkbox" Id="emall" class="form-check-input" />
    <label for="email" class-"form-check-label">Email</label>
</div>
```

### [Input Group](https://getbootstrap.com/docs/5.0/forms/input-group/):
- Whatever we put inside the input group, they are placed with a dividing line between them and rounded edges.
- Used to include text and input elements for the forms to make them more accessible.
```html
// Input the amount in dollars in a form
<form>
    <label for= "text" class-"form-label">Amount</label>
        <div class="input-group">
            <div class-"Input-group-text">$</div>
            <input type-"number" id-"text" class-"form-control">
            <button class "btn btn-primary"›+</button>
        </div>
    <button>Submit</button>
</form>
```

### Floating Labels:
- Must add placeholder and label should be after input tag.
```html
<form>
    <div class-"form-floating">
        <input type="email" Id-"email" class= "form-control" placeholder= "Place email here">
        <label for="email">Email</label>
    </div>
    <button>Submit</button>
</form>
```

### Form Validation:
- Add the "required" field to the input tag to make the user add the value compulsorily.
- To override the form validation use "novalidate" in form
```html
<form novalidate>
    <div class-"form-floating">
        <input type="email" Id-"email" class= "form-control" placeholder= "Place email here" required>
        <label for="email">Email</label>
        //Error Message based on the input value
        <div class-"invalid-feedback">Invalid email</div>
        <div class "valid-feedback">Correct email</div>
    </div>
    <button>Submit</button>
</form>
```

## BootStrap built-in Elements:
### Button:
- 
