# @squirrel-forge/sass-util
sass abstracts, mixins, globals and utilities

## Installation

```
npm i @squirrel-forge/sass-util
```

## Usage

```
@import "~@squirrel-forge/sass-util";
```

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

Check the sourcecode on [github](https://github.com/squirrel-forge/sass-util) for extensive comments.
