# Boiled Page button component

Button SCSS component for Boiled Page frontend framework. It is intended to apply the same button style for button and anchor elements, group buttons together, add dropdown subnavigation to a button, make a button element looks like an anchor.

## Install

Place `_button.scss` file to `/assets/css/components` directory, and add its path to components block in `assets/css/app.scss` file. If you want to use button dropdown component, you will also need to add dropdown script to make it working properly.

- Dropdown script: <https://www.github.com/abelbrencsan/boiled-page-dropdown-script>

## Usage

### Button component

Button component is intended to apply same button style for button and anchor elements.

#### Classes

Class name | Description | Example
---------- | ----------- | -------
`button` | Applies a button. | `<button class="button"></button>`

#### Examples

##### Example 1

The following example shows an anchor element styled as a button. 

```html
<a href="#" class="button" role="button">Button</a>
```

##### Example 2

The following example shows a button element styled as a button. 

```html
<button type="button" class="button">Button</button>
```

#### Extension ideas

##### Small button

```scss
/* Button component extensions */
a.button, button.button {

  // Small button
  &.button--small {
    font-size: $small-font-size;
  }
}
```

##### Large button

```scss
/* Button component extensions */
a.button, button.button {

  // Large button
  &.button--large {
    font-size: $large-font-size;
  }
}
```

##### Button for icons

```scss
/* Button component extensions */
a.button, button.button {

  // Button for icons
  &.button--iconbutton {
    width: $element-height;
    padding: 0;

    &.button--iconbutton--circle {
      border-radius: 50%;
    }
  }
}
```

##### Button with a small badge on the top right corner

```scss
/* Button component extensions */
a.button, button.button {

  // Button with a small badge on the top right corner
  &.button--badge {
    position: relative;
    overflow: visible;

    &[data-badge]:before {
      display: inline-block;
      position: absolute;
      top: -0.5em;
      right: -0.5em;
      padding: 0.125em 0.5em;
      border-radius: $border-radius;
      background-color: $link-color;
      color: $bg-color;
      font-size: $small-font-size;
      line-height: 1;
      white-space: nowrap;
      content: attr(data-badge);
      cursor: default;
      pointer-events: none;
    }
  }
}
```

##### Scheme colored buttons

Add `generate-button` to each scheme in SCSS variables with the value of true or false. Then you can use buttons in colors of enabled schemes.

```scss
/* Button component extensions */
a.button, button.button {

  // Scheme colored buttons
  @each $scheme in map-keys($schemes) {
    @if (map-val($schemes, $scheme, generate-button)) {
      &.button--#{$scheme} {
        background-color: map-val($schemes, $scheme, bg-color);
        color: map-val($schemes, $scheme, fg-bold-color) !important;

        body.no-touch &:hover, &:active {
          background-color: lighten(map-val($schemes, $scheme, bg-color), 5);
        }
      }
    }
  }  
}
```

### Button group component

Button group component is intended to group buttons together.

#### Classes

Class name | Description | Example
---------- | ----------- | -------
`button-group-list` | Applies a button group list. Use grid component for alignments. | `<ul class="button-group-list"></ul>`

#### Examples

##### Example 1

The following example shows a center aligned button group list.

```html
<ul class="button-group-list grid grid--center">
  <li class="grid-col">
    <button type="button" class="button">Button 1</button>
  </li>
  <li class="grid-col">
    <button type="button" class="button">Button 2</button>
  </li>
</ul>
```

### Button subnav component

Button subnav component is intended to add a dropdown subnavigation to a button.

#### Classes

Class name | Description | Example
---------- | ----------- | -------
`button-subnav` | Applies a button subnavigation. | `<div class="button-subnav"></div>`

#### Examples

##### Example 1

The following example shows a button with dropdown subnavigation. `data-button-subnav` attributes are used for dropdown script.

```html
<div class="button-subnav" data-button-subnav>
  <button type="button" class="button" data-button-subnav-trigger>Button</button>
  <ul data-button-subnav-element>
    <li>
      <a href="#">About Us</a>
    </li>
    <li>
      <a href="#">Pricing</a>
    </li>
    <li>
      <a href="#">Resources</a>
    </li>
    <li>
      <a href="#">Features</a>
    </li>
  </ul>
</div>
```

Add `buttonSubnavs` property to `app` object in `assets/js/app.js`.

```js
buttonSubnavs: []
```

Place the following code inside `assets/js/app.js` to initalize elements with `data-button-subnav` attribute as dropdowns.

```js
// Initialize button subnavigations
var buttonSubnavElems = document.querySelectorAll('[data-button-subnav]');
for (var i = 0; i < buttonSubnavElems.length; i++) {
  app.buttonSubnavs[i] = new Dropdown({
    trigger: buttonSubnavElems[i].querySelector('[data-button-subnav-trigger]'),
    element: buttonSubnavElems[i].querySelector('[data-button-subnav-element]')
  });
  app.buttonSubnavs[i].init();
}
```

Place the following code inside the `onBreakpointChange` function in `assets/js/app.js` to recalculate maximum height of opened button subnavigation's element when breakpoint changes.

```js
// Recalculate maximum height of opened button subnavigation's element
for (var i = 0; i < app.buttonSubnavs.length; i++) {
  app.buttonSubnavs[i].recalcHeight();
}
```

#### Extension ideas

##### Button subnav with right aligned subnavigation

```scss
/* Button subnav component extensions */
div.button-subnav {

  // Button subnav with right aligned subnavigation
  &.button-subnav--right {

    > ul {
      left: auto;
      right: 0;

      &:before {
        left: auto;
        right: $box-padding;
      }
    }
  }
}
```

### Button link component

Button link component is intended to make button elements look like an anchor element.

#### Classes

Class name | Description | Example
---------- | ----------- | -------
`button-link` | Applies a button link. | `<button class="button-link"></button>`

#### Examples

##### Example 1

The following example shows a button link. 

```html
<button type="button" class="button-link">Button</button>
```
