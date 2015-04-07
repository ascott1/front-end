# CSS & Less Guide

This style guide aims to provide the ground rules for CFPB's CSS, such that it's highly readable and consistent across different developers on a team. 

## Table of Contents

1. [General Practices](#general-practices)
1. [Property Order](#property-order)
1. [Naming Conventions](#naming-conventions)
1. [Styles](#styles)
1. [Media Queries](#media-queries)
1. [Less](#less)
    - [Less General Practices](#less-general-practices)
    - [Selectors and Nesting](#selectors-and-nesting)
    - [Variables](#variables)

## General Practices

- Use soft-tabs with a two space indent
- One line per selector
- Use a single space after the colon
- Always end property declarations with a semicolon
- Put spaces after `:` in property declarations
- Put spaces before `{` in rule declarations

## Property Order

Box model properties go first, in order from inside the box out, followed by positioning.

Remaining properties are in alphabetical order.

```css
.selector {
    /* Display & Box Model */
    display: inline-block;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;
    overflow: hidden;

    /* Positioning */
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    z-index: 10;

    /* Other */
    background: #000 url('../img/bg.png') no-repeat center top;
    color: #fff;
    cursor: pointer;
    font-family: sans-serif;
    font-size: 16px;
    font-style: italic;
    font-weight: bold;
    line-height: 1;
    list-style: none;
    text-align: right;
}
```

_N.B.: It is not necessary to include the group headings in your actual CSS. They are just for clarity in this example._

## Naming Conventions
Custom [BEM ("Block Element Modifier")](https://en.bem.info/method/definitions/) format:

```css
.block-name
.block-name_element-name
.block-name__block-modifier
.block-name_element-name__element-modifier
```

### Avoid creating elements of modifiers
Appending an element name to a modifier class can result in a confusing class name like `.list__space_item`. Avoid this in favor of using a descendant, like this: `.list__spaced .list_item`.

### `id` attribute

While the `id` attribute might be fine in HTML and JavaScript, it should be **avoided entirely** inside stylesheets. Few reasons.

- ID selectors are not reusable
- Priority nightmares

##### Good

```css
.ur-name {
  // ...
}
```

##### Bad

```css
#ur-name {
  // ...
}
```

Just assign a class name to the element.

## Styles

These rules apply to your CSS property values

- If the value of a property is `0`, do not specify units
- The `!important` rule should be aggressively avoided.
  - Keep style rules in a sensible order
  - Compose styles to dissipate the need for an `!important` rule
  - Fine to use in limited cases
    - Overlays
    - Declarations of the `display: none !important;` type
- Keep `z-index` levels in variables in a single file. **Avoids confusion** about what level should be given to an element, and arbitrarily-high `999`-style values
- Use hex color codes `#000` unless there's an explicit need for an `rgba` declaration
- Avoid mixing units
- Unit-less `line-height` is preferred because it does not inherit a percentage value of its parent element, but instead is based on a multiplier of the `font-size`.

##### Good

```css
.btn {
  color: #222;
}

.btn-red {
  color: #f00;
}
```

##### Bad

```css
.btn-red {
  color: #f00 !important;
}

.btn {
  color: #222;
}
```

## Media Queries
In most cases styles should be declared mobile first, then enhanced with `min-width` media queries. By doing this we create a base experience that all devices can use and one that does not require media query support.

## Less

At the CFPB we use Less as our CSS preprocessor.

### Less General Practices

- Put comments in `//` statements
- Prefer nested selectors `.foo { .bar {} }` vs `.foo .bar {}`
  - _Only if both `.foo` and `.foo .bar` need styling_
- Don't nest selectors beyond 3 levels deep

### Selectors and Nesting

Styles shouldn't need to be nested more than three levels deep. This includes pseudo-selectors. If you find yourself going further, think about re-organizing your rules _(either the specificity needed, or the layout of the nesting)_.

### Variables

- Colors: (use generic variable names like recent cfgov-refresh update)
- Breakpoints: standard variable names for commonly used breakpoints

## Credits

Some of this document is based on [Nicolas Bevacqua's fbc-style-guide](https://github.com/bevacqua/css), which is licensed under the MIT license.