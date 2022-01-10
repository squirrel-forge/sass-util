# @squirrel-forge/sass-util
Collection of sass abstracts, mixins, globals and utilities.

## Installation

```
npm i @squirrel-forge/sass-util
```

## Usage

```scss
/* Set variables before importing, by default all are enabled */
$with-global: true;
$with-util: false;
@import "~@squirrel-forge/sass-util";

/* You may import only the sections or files you require */
// @import "~@squirrel-forge/sass-util/src/functions/index";
// @import "~@squirrel-forge/sass-util/src/mixins/index";
// etc.
```

Variable declarations can be found [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults).

### Contents

An overview of the package contents:

 - **Global** A set of global reset css, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_global.scss) for details.
 - **Util** A set of utility classes, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_util.scss) for details.
 - **Media** A media query abstraction, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_media.scss) for details.
 - **Break** Media definitions for the break utility, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_break.scss) for details.
 - **Font** Font definitions for the font utility and helpers, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_font.scss) for details.
 - **List** List normalization and style utilities, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_list.scss) for details.
 - **Text** Text helpers and media definitions, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_text.scss) for details.
 - **Wrap** Flex wrapper definitions, see variables [here](https://github.com/squirrel-forge/sass-util/blob/main/src/defaults/_wrap.scss) for details.

#### Mixins

An overview of mixins available:

 - **mx-attr-isset** @content is applied only if a given attribute is set.
 - **mx-attr-none** @content is applied only if a given attribute is not set.
 - **mx-attr-set** Sets a map of attributes.
 - **mx-attr-set-map** Sets a map of attributes from a map of attribute maps.
 - **mx-bem** Generates BEM style classes from a nested map.
 - **mx-break-before**, **mx-break-after** Pseudo inline break.
 - **mx-clear-before**, **mx-clear-after** Pseudo clear float.
 - **mx-font** Output font style by name from map.
 - **mx-font-fluid** Output fluid font style by name from map.
 - **mx-font-fluid-base** Fluid font style base mixin.
 - **mx-hide-accessible** Element will be visually hidden, but accessible for screenreaders etc.
 - **mx-media** @content will be wrapped in a media query of the given name.
 - **mx-no-select** Element text will not be selectable by user.

### Notes

Following some notes on mixin, function and sass behaviours directly relevant to using the utilities.

#### Sass maps

Inside map declarations to use comma separated values wrap them in (value, value) to make them a list value,
for example for font-family declarations:

```scss
$map: (
  key: (
    font-family: ("Oxygen", sans-serif),
  ),
);
```

Or you can escape the value as following:

```scss
$map: (
  key: (
    font-family: #{"Oxygen", sans-serif},
  ),
);
```

### Examples

#### Font styles

Source:
```scss
$font-styles: (

  // Base declaration
  default: (
    font-family: (Oxygen, sans-serif),
    font-size: 14px,
    font-weight: normal,
    line-height: 1.33,
  ),

  // Regular default and responsive declarations
  headline: (
    font-size: 30px,
    font-weight: bold,
  ),
  headline_at_small: (
    font-size: 20px,
  ),
  headline_at_tablet: (
    font-size: 40px,
  ),
  headline_at_medium: (
    font-size: 40px,
  ),
  headline_at_desktop: (
    font-size: 50px,
  ),

  // Fluid font responsive declarations
  headline-fluid_at_mobile: (
    font-weight: bold,
    fluid: (
      min-vw : 320px,
      max-vw : 767px,
      min-size : 20px,
      max-size : 30px,
    ),
    no-max: true,
  ),
  headline-fluid_at_tablet: (
    fluid: (
      min-vw : 768px,
      max-vw : 1024px,
      min-size : 30px,
      max-size : 35px,
    ),
    no-max: true,
  ),
  headline-fluid_at_medium: (
    fluid: (
      min-vw : 1025px,
      max-vw : 1366px,
      min-size : 35px,
      max-size : 50px,
    ),
  )
);
```

Rendered:
```css
/* Base declaration */
.font--default {
  font-family: Oxygen, sans-serif;
  font-size: 14px;
  font-weight: normal;
  line-height: 1.33;
}

/* Regular default and responsive declarations */
.font--headline {
  font-size: 30px;
  font-weight: bold;
}
@media screen and (max-width: 374px) {
  .font--headline { font-size: 20px; }
}
@media screen and (min-width: 768px) and (max-width: 1024px) {
  .font--headline { font-size: 40px; }
}
@media screen and (min-width: 1025px) {
  .font--headline { font-size: 40px; }
}
@media screen and (min-width: 1366px) {
  .font--headline { font-size: 50px; }
}

/* Fluid font responsive declarations */
.font--headline-fluid {
  font-weight: bold;
}
@media screen and (max-width: 767px) {
  .font--headline-fluid { font-size: 20px; }
}
@media screen and (min-width: 320px) {
  .font--headline-fluid { font-size: calc(20px + 10 * ((100vw - 320px) / 447)); }
}
@media screen and (min-width: 768px) and (max-width: 1024px) {
  .font--headline-fluid { font-size: 30px; }
}
@media screen and (min-width: 768px) {
  .font--headline-fluid { font-size: calc(30px + 5 * ((100vw - 768px) / 256)); }
}
@media screen and (min-width: 1025px) {
  .font--headline-fluid { font-size: 35px; }
}
@media screen and (min-width: 1025px) {
  .font--headline-fluid { font-size: calc(35px + 15 * ((100vw - 1025px) / 341)); }
}
@media screen and (min-width: 1366px) {
  .font--headline-fluid { font-size: 50px; }
}
```

#### Wrap with BEM styles

Source:
```scss
$wrap-styles: (

  // Section wrapper
  --section: (
    position: relative,
    flex-direction: column,
    padding: 0 1rem,
    _at_tablet-desktop: (
      max-width: calc(100% - 2rem),
    ),
  ),

  // Content wrapper, including variants
  --content: (
    position: relative,
    max-width: 380px,
    _at_small: (
      max-width: 300px,
    ),
    _at_tablet-portrait: (
      max-width: 720px,
    ),
    _at_tablet-landscape-desktop: (
      max-width: 1000px,
    ),
    -before: (
      position: relative,
      margin: 0 auto 2rem,
    ),
    -main: (
      position: relative,
    ),
    -after: (
      position: relative,
      margin: 2rem auto 0,
    ),
  ),
);
```

Rendered:
```css
.wrap {
  margin: auto;
  width: 100%;
}
.wrap:not(.wrap--no-flex) {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
}

/* Section wrapper */
.wrap--section {
  position: relative;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -ms-flex-direction: column;
  flex-direction: column;
  padding: 0 1rem;
}
@media screen and (min-width: 768px) {
  .wrap--section { max-width: calc(100% - 2rem); }
}

/* Content wrapper, including variants */
.wrap--content {
  position: relative;
  max-width: 380px;
}
@media screen and (max-width: 374px) {
  .wrap--content { max-width: 300px; }
}
@media screen and (min-width: 768px) and (max-width: 991px) {
  .wrap--content { max-width: 720px; }
}
@media screen and (min-width: 992px) {
  .wrap--content { max-width: 1000px; }
}
.wrap--content-before {
  position: relative;
  margin: 0 auto 2rem;
}
.wrap--content-main { position: relative; }
.wrap--content-after {
  position: relative;
  margin: 2rem auto 0;
}
```

Check the sourcecode on [github](https://github.com/squirrel-forge/sass-util) for extensive comments.
