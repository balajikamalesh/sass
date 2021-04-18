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
 - Variables and Mixins
 - Control flow
 - CSS Architecture
 - Defining your own SASS functions

## Basics
 - Invented by HAMPTOP CATLIN, he also invented HAML
 ```css
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

```css
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
```css
.container {
    > .left-area { 
        /* only the first descendent named left-area (immediate children)*/
    }
}
```
- Parent Selector (&) (to refer to the immediate outer selector, It makes it possible to re-use the outer selector in more complex ways, like adding a pseudo-class or adding a selector before the parent)
```css
.container {
    & .right-nav { 
        
    }
}
```
