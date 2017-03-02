---
title: CSS
taxonomy:
    category: docs
--- 

Information about writing CSS for Cambridge sites

### BEM

Follow [BEM](http://getbem.com/naming/). 

+ BEM stands for Block, Element and Modifier
```
.block { }
.block__element { }
.block--modifier { }
```
+ Some examples
```
.person { }
.person__head { }
.person--tall { }
```

### SASS

Only nest when

// examples

### CSS

+ Try to only ever use shorcuts for selectors such as `padding`, `margin` and `border`
```
// good
padding: 0 5px 10px 2px;
//bad
padding-left: 10px;
```
+ Somehting else

### Media queries

+ Only ever use `min-width`, never `max-width`
+ Write your selectors mobile first, in **ascending order of size**. eg a style that applies to every size screen goes first, one that is `min-width: 992px` comes after

### JavaScript Hooks

+ Do not use `data-*` attributes for hooks. Use classes prepended with `js-` and **do not** style these with CSS. eg
```
<input type="submit" class="btn js-btn" value="Follow" />
```