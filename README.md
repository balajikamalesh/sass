# SASS
- It is a CSS preprocessor
- Has its own syntax and compiles to plain CSS
- Preprocessors will add some features that don't exist in pure CSS, such as mixin, nesting selector, inheritance selector

## Pitfalls of CSS
 - We are working on Globals. Leads to collision
 - No Variables (*)
 - Not composable ex: class="left bold" (*)
 - Bad Modularity Primitives (Modular imports of multiple files not supported by CSS)

## Fundamentals
 - Basics ( syntax, nesting, scoping)
 - Variables and Importing
 - Mixins
 - Control flow
 - CSS Architecture
 - Defining your own SASS functions

## Basics
 - Invented by HAMPTOP CATLIN, he also invented HAML
 ```scss
 .foo {
     color: green;
     font-size: 1.3rem;
 }
 ```
### Nesting & Scoping
- Styles can be placed in the declaration block of a parent
- Easy to expand
- This is already DRY (Don't Repeat Yourself) code

```css
/* plain css */
.container {
    /* style1 */ 
}

.container .main {
    /* style2 */ 
}

.container .sidebar, .container .main {
    /* style3 */
}

.container .sidebar {
    /* style4 */
}
```

```scss
/* sass */
.container {
    /* style1 */
    
    .sidebar, .main {
        /* style3 */
    }

    .main {
        /* style2 */
    }

    .sidebar {
        /* style4 */
    }
}
```

### Selectors
- Descendent
```css
.container {
    .left-area {
         /* all descendents named left-area */
    }
}
```
- Direct Descendent (>)
```scss
.container {
    > .left-area { 
        /* only the first descendent named left-area (immediate children)*/
    }
}
```
- Parent Selector (&) (to refer to the immediate outer selector, It makes it possible to re-use the outer selector in more complex ways, like adding a pseudo-class or adding a selector before the parent)
```scss
.container {
    & .right-nav { 
       /* styles  */
    }
}
```

## Importing and Variables

### Importing
- Using @import in CSS results in a new round-trp HTTP request
- @import in SASS is a bit different
- File name starting with "_" are called "partials" ( ex: _layout.scss ), and are meant to be exported into other SCSS files
```scss
@import 'bootstrap';
@import '_layout';
```

### Variables
- We can create variables with style values and use them instead of the values itself
- It begins with a '$, ex: "$color" and supports various Types
- NUMBERS - '10', '200px', '50%'
- COLORS - 'RED', '#FFF'
- STRINGS - 'a.png', 'url(....)'
- BOOELANS - true, false
- SASS can convert units as long as dimensions are the same
```scss
// global variables
// !default means if this is already declared, this won't rewrite it 
$error_color: #f00 !default;

.alert-error {
    $text_color: #ddd; //local variables
    background-color: $error_color;
    color: $text_color;
    //darken is a Sass function
    text-shadow: 0 0 2px darken($text_color, 40%);
    .alert-error-2 {
        color: $text_color;
    }
}
```

```scss
// _variables.scss file
$hopbush: #c69 !default;
$patina: #699 !default;
$venus: #998099 !default;
$nebula: #d2e1dd !default;

$black: #000 !default;
$white: #fff !default;

$btn-disabled-opacity: 0.5 !default;
```

```scss
// app.scss file
@import 'variables'; //import partials file here 

body {
    h1 {
    color: #c69;
  }
}
.btn {
  padding: 2px 10px;
  border-radius: 2px;
  &.btn-primary {
    border: 1px solid $venus;
    background-color: $hopbush; //use variable names from the partials
    color: #fff;
  }
  &.btn-secondary {
    border: 1px solid $patina;
    background-color: $nebula;
    color: #000;
  }
  &:disabled {
    opacity: 0.5;
  }
}
```
