# REI Code Style Guides // Less

> Code style guide for Less stylesheets at REI

## <a name='TOC'>Table of Contents</a>


  1. [Selectors](#selectors)
  1. [Naming Conventions](#naming)
  1. [Values](#values)
  1. [Properties](#properties)
  1. [Organization](#organization)
  1. [Comments](#comments)
  1. [Resources](#resources)


## <a name='selectors'>Selectors</a>

- Avoid using IDs in your selectors. They undermine the *cascade* of CSS, leading to bloated code and general hackiness.

```css
/* bad */
#content #sidebar {
    float: right;
}

/* less bad */
#sidebar {
    float: right;
}

/* good */
.order-summary-sidebar {
    float: right;
}
```

- If you must use one, though, do not use any other selectors with it: IDs must be unique, so further specification is redundant (and hurts performance).

```css
/* bad */
.content div#sidebar {
    float: right;
}

/* good */
#sidebar {
    float: right;
}
```

- Drop element selectors in favor of targeted classes to avoid bleed-over effects.

```css
/* bad */
ul {
    /* ... */
}

/* good */
.product-list {
    /* ... */
}
```

- Say what you mean: ditch descendant selectors.

```css
/* bad */
ul .product-list-item {
    /* ... */
}

/* good */
.product-list-item {
    /* ... */
}
```

- If you must use descendant selectors, make the right-most selector as specific as possible. Browsers parse CSS from right-to-left ([see Joel Falconer below](#efficient-selectors)). In the following example, the browser will collect all `a` elements, then focus on the ones inside of parents with the `.login-area` class, and finally limit that group to the `#header` element. Yikes!

```css
/* really bad */
#header .login-area a {
    /* ... */
}

/* better, but still bad */
#header .login-action {
    /* ... */
}

/* good */
.header-login-action {
    /* ... */
}
```

## <a name='naming'>Naming Conventions</a>

- Stick to lowercase names, with dashes to separate words. It reads better and makes selecting individual bits easier.

```css
/* good */

.super-sweet-class {
  /* ... */
}
#id-becuase-yolo {
  /* ... */
}

/* bad */
.superSweetClass {
  /* ... */
}
#idBecauseYolo {
  /* ... */
}
```

## <a name='values'>Values</a>

- Be consistent when defining colors. Try to use the same method throughout your stylesheet.

```css
/* bad */
.style1 {
    color: red;
}
.style2 {
    background-color: #FF0000;
}
.style3 {
    border-color: rgb(255, 0, 0);
}

/* good */
.style1 {
    color: rgb(255, 0, 0);
}
.style2 {
    background-color: rgb(255, 0, 0);
}
.style3 {
    border-color: rgb(255, 0, 0);
}
```

- Even better: use LESS to keep your values DRY and consistent.

```less
/* best */

// In variables.less
@red: rgb(255, 0, 0);

// In styles.less
.style1 {
    color: @red;
}
.style2 {
    background-color: @red;
}
.style3 {
    border-color: @red;
}
```

- Avoid repetition when setting values for properties.

```css
/* bad */
.product-image {
    margin: 10px 10px 10px 10px;
}

/* good */
.product-image {
    margin: 10px;
}

/* bad */
.product-title {
    padding: 10px 0 10px 0;
}

/* good */
.product-title {
    padding: 10px 0;
}
```

## <a name='properties'>Properties</a>

- Use `translate(x, y)` rather than `position` (and `top`, `left`, etc.) to move elements on a page. ([see Paul Irish below](#transition)) ([jsPerf](http://jsperf.com/translate3d-vs-positioning/4))

```css
/* bad */
.order-summary-sidebar {
    top: 10px;
    left: 10px;
}

/* good */
.order-summary-sidebar {
    transform: translate(10px, 10px);
}
```

## <a name='organization'>Organization</a>

- Use one `main.less` file to import all of your project's dependencies and Less files.

```less
// Base dependencies
@import "some/shared/styles.less"

// My variables and mixins
@import "my-variables.less";
@import (reference) "my-mixins.less";

// My styles
@import "base.less";
@import "some-component.less";
@import "other-component.less";
```

- Import references to files whose contents shouldn't appear directly in your generated CSS.

```less
// In mixins.less
.focus() {
    border: 1px solid blue;
    border-radius: 10px;
    box-shadow: 0 0 6px blue;
}

// In main.less
@import (reference) "mixins.less";
```

- Use a `base.less` file for a small set of styles that are used throughout your project.

- Split your project into files covering as small a section as makes sense to avoid bloated stylesheets. It's easier to navigate five focused Less files than one covering a whole section.

## <a name='comments'>Comments</a>

- In Less, `//`-style comments will be removed when compiling your stylesheets, whereas `/* ... */`-style comments will remain, so prefer the former.

```less
// I will be removed

/* I will be in the generated CSS */
```

- Use comments to provide a guide to your stylesheet's structure.

```less
// Product tile styling
.product-tile {

    // Product details
    .detail-label {
        // styles
    }
    .detail-value {
        // styles
    }

    // Comparison actions
    .compare-add {
        // styles
    }
    .compare-remove {
        // styles
    }

    // Ratings
    .rating-stars {
        // styles
    }

}
```

- Comment blocks that are deeply nested to clarify what the resultant selector will be. (Even better: avoid nesting that requires this.)

```less
.great-grand-parent {

    .grand-parent {

        // .great-grand-parent .grand-parent .parent
        .parent {

            // .great-grand-parent .grand-parent .parent .child
            .child {
                // styles
            }

        }

    }

}
```

- Add comments to explain any odd styling choices. It's sad, but true that a little hackiness is some times necessary. Just be sure to explain it.

```less
.order-total {
    // float element to fix layout issues with order cost totals
    float: left
}
```

## <a name='resources'>Resources</a>

**CSS performance**

  - [Writing Efficient CSS: Understand Your Selectors](http://thenextweb.com/2011/03/22/writing-efficient-css-understand-your-selectors/) (<a name='efficient-selectors'>Joel Falconer</a>)
  - [GitHub's CSS performance](https://speakerdeck.com/jonrohan/githubs-css-performance) (slide deck by Jon Rohan)
  - [Why Moving Elements With Translate() Is Better Than Pos:abs Top/left](http://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/) (<a name='translate'>Paul Irish</a>)

**Naming conventions**

  - [Shoot to kill; CSS selector intent](http://csswizardry.com/2012/07/shoot-to-kill-css-selector-intent/)

**Other style guides**

  - [GitHub's CSS style guide](https://github.com/styleguide/css)

**jsPerf**

  - [translate vs. translate3d vs. position](http://jsperf.com/translate3d-vs-positioning/4)
