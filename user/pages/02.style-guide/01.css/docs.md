---
title: CSS
taxonomy:
    category: docs
--- 

Information about writing CSS for Cambridge sites.

Some examples are taken from [Airbnbs design guide](https://github.com/airbnb/css) (don't ask me which).

## BEM
___
Follow [BEM](http://getbem.com/naming/). A clear representation of the concept can be found here [BEM Key Concepts](https://en.bem.info/methodology/key-concepts/). Some extra rules can be found below

+ BEM stands for Block, Element and Modifier
+ **Blocks** should be a standalone, independent components. A block can exist anywhere, including in other blocks 
+ **Elements** should be something that makes up the block. An element **can not** be used outside it's block, it's an element of the block. An element **can not** can not live in another element
+ **Modifiers** represent a different state or version of the block or element, these should be used **rarely**. If you do, think carefully whether you are modifying the block or an element

```
.block { }
.block__element { }
.block--modifier { }
// or
.person { }
.person__head { }
.person--tall { }
.person__head--large { } // use this one rarely
```

Here's a more complete example:

```
<!-- New block Header -->
<div class="header">
  <!-- New block logo -->
  <div class="logo">
    <div class="logo__image">
        <img src="/img.jpg" alt="logo">
    </div>
    <div class="logo__text">
        Site name
    </div>
  </div>
  
  <!-- New block nav -->
  <div class="nav">
    <!-- Elements can be repeated (as can blocks, eg .blog, .news-story) -->
    <div class="nav__link nav__link"> 
      Blogs
    </div>
    <div class="nav__link nav__link--active">
      About us
    </div>
  </div>
  
  <!-- New element of header ( this gets tricky: search is not unique to the header, it's the header's search) -->
  <div class="header__search">
    <input type="text" placeholder="Search our site">
  </div>

</div>
```

+ If possible try and avoid using names with hyphens in them such as `.block-name`
+ A good tip is too use plurals and repeatable singles, similar to a foreach loop `foreach ($blogs as $blog)`, such as:

```
<div class="slides">
  <div class="slide">
    1
  </div>
  <div class="slide">
    2
  </div>
</div>
// or
<div class="example-entries">
  <div class="example-entry">
    a
  </div>
  <div class="example-entry">
    b
  </div>
</div>
```

## SASS
___
#### Syntax

* Use the `.scss` syntax, never the original `.sass` syntax
* Order your regular CSS and `@include` declarations logically (see below)

#### Ordering of property declarations

1. List all standard property declarations, anything that isn't an `@include` or a nested selector first.
2. Then any `@include` declarations if you have them
3. Nested selectors, _if necessary_, go last, and nothing goes after them.

```scss
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  .icon {
    margin-right: 10px;
  }
}
```


#### Nested selectors

Attempt to avoid using nested selectors. They encourage specifity, and discourage modular design. If you must **only go one level deep**

Nesting is OK for the following:
+ Pseudo classes such as `:hover`
+ Modifier classes like `.btn.active` that inherit the parent's properties
+ HTML tags like `p`, where creating a new selector like `.content__paragraph` would not make sense
+ If you don't have control over the markup (looking at you Drupal)
+ HTML tag heavy structures such as tables (`td`, `thead` etc) and forms (`option`, `select`), where again the semantics of the tag is self explanatory

For the `a` tag, as a general rule if it's wrapping other elements (like an image and text) add a selector to the `a. If it's the last element (like a link in a body of text), use `a` nested

```
.page-container {
  .content {
    .profile {
      // BAD!
    }
  }
}
```

## CSS
___
+ Try to only ever use shorcuts for selectors such as `padding`, `margin` and `border`

```
    // good
    padding: 0 5px 10px 2px;
    //bad
    padding-left: 10px;
```

+ Prefer tabs for indentation
+ Prefer dashes over camelCasing in class names. 
+ Do not use ID as selectors
+ When using multiple selectors in a rule declaration, give each selector its own line.
+ Put a space before the opening brace `{` in rule declarations
+ In properties, put a space after, but not before, the `:` character.
+ Put closing braces `}` of rule declarations on a new line
+ Put blank lines between rule declarations
+ Don't use vendor prefixies, use autoprefixer
+ Try and using *utility classes* or *modifier classes*, that do one minor thing such as `.padding-top-10px`, `.pink-text` or `.invisible`
+ Never use `!important`
+ Never use `@extend` 
+ Try and avoid abbreviating names, unless they're already widespread (eq `.btn` or `nav` is ok)
+ Names should be created at a component level, not a page level. `.nav` vs `.homepage-nav`
+ Prefer line comments (`//` in Sass-land) to block comments. Prefer comments on their own line. Avoid end-of-line comments.
+ Write detailed comments for code that isn't self-documenting:
    - Compatibility or browser-specific hacks
    - Uses of z-index

## Media queries
___
+ Only ever use `min-width`, never `max-width`
+ Write your selectors **mobile first**, so subsequent selectors for larger screens inherit their properties. This avoids repetition, and makes your code more managable.
+ Write in **ascending order of size**. Eg a style that applies to every size screen goes first, one that is `min-width: 992px` comes after. For instance:
```
    .content {
      width: 100%;
      margin: 0 15px;
    }

    @media (min-width: 720px) {
      .content {
        width: 700px;
        margin: 0 auto;
      }
    }

    @media (min-width: 920px) {
      .content {
        width: 900px;
      }
    }
```

+ Keep media queries for each scss file together. All selectors targeting `min-width: 992px` should be in one `@media` block

## JavaScript Hooks
___
+ Use classes prepended with `js-` and **do not** style these with CSS. Do not use `data-*` attributes for hooks, only for storing data. eg:
```
<input type="submit" class="btn js-btn" value="Follow" />
```