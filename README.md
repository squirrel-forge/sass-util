# @squirrel-forge/sass-util

Collection of sass abstracts, mixins, globals and utilities.
Built for the dart-sass *@use module syntax*, allowing for full and individual feature usage.

*Please Note* that from version **0.9.0** the package is fully based on the *@use module syntax*, if you are looking for the old version using the @import syntax install version **0.8.x**, but consider migrating to the **0.9.x** standard to avoid missing out on updates. 

## Installation

```
npm i @squirrel-forge/sass-util
```

## Usage

Make use of your IDE's autocompletion, for reference you can find a full list of [namespaces](#available-namespaces) below,
or checkout the [example implementation](src/util.scss) and the [generated output](dist/util.css).  
Note that the *@use* syntax works differently than the classic *@import*, check the [use syntax notes](#use-syntax) for relevant details and or refer to the [official sass docs](https://sass-lang.com/documentation/at-rules/use).

```scss
/**
 * Using the full library
 */
@use '~@squirrel-forge/sass-util' as util;

/**
 * You may use only the modules or submodules you require,
 * note that you need to add the 'src' folder to the use path
 */
@use '~@squirrel-forge/sass-util/src/media';
// etc.
```

### Using the full library

When using the full package, make use of the namespacing to select from the individual submodules.

```scss
@use '~@squirrel-forge/sass-util' as util;
@include util.media-config((
  custom-breakpoint: 'screen and (max-width: 10rem)',
));
@include util.media-query('custom-breakpoint') {
  // @content
}
```

### Using individual submodules

When using submodules directly, namespacing is shorter, without the parent prefixes, this way you have granular control over which modules to use, but you need to add the *src* folder path to your @use url.

```scss
@use '~@squirrel-forge/sass-util/src/media';
@include media.config((
  custom-breakpoint: 'screen and (max-width: 10rem)',
));
@include media.query('custom-breakpoint') {
  // @content
}
```

Not recommended, but possible: If you wish to use modules more than once and require configuration changes,
then you need to modify the namespaces variables directly, but keep in mind that the values change permanently even for other contexts and need to be reset manually, since modules are only loaded once.

## Available namespaces

An alphabetical overview of available **namespaces**, *variables*, functions and mixins, those marked with a "**+**" can be loaded individually.  
Note when loading individual modules, functions or mixins directly, you must include the *src* path folder in your use url, also note initial loading order matters when using the *with* keyword for configuration, see the [notes](#use-syntax) for more details.  
Any namespace can be loaded individually, if it contains multiple submodules there is a corresponding index available.

### + util

Complete library, the namespace defined when loading the full package with *@use*.

```scss
@use '~@squirrel-forge/sass-util' as util with (
  $config-value: 'string',
);
```

#### + util / abstract

Only abstract functions and helpers, none of these contain configuration.

 - +config(```$options: null, $defaults: null, $extend: false, $strict: true, $error: 'config::'```) - Map with defaults with merged options.
 - +default-args(```$data, $optional...```) - A list with arguments and defaults.
 - +has-query(```$name, $query-marker: '_at_', $error: 'has-query::'```) - Empty if no query was found.
 - +is-query(```$name, $query-marker: '_at_'```) - Query reference or null if not a query
 - +spacing(```$params...```) - Spacing values list.
 - +str-initials(```$name, $separator: '-'```) - First char of each element separated as a joined string.
 - +str-split(```$string, $separator, $no-empty: true```) - Separated list of strings
 - +strip-unit(```$value```) - Unitless value

#### + util / colors  

Generates colors as custom properties including variants, with corresponding helper classes for usage.

 - *$class*: ```'ui-color'```
 - *$props*: ```'ui-color-'```
 - *$variant-complement*: ```'comp'```
 - *$variant-grayscale*: ```'gray'```
 - *$variant-alpha*: ```'op'```
 - *$variant-invert*: ```'inv'```
 - *$variant-adjust-hue*: ```'hue'```
 - *$variant-darken*: ```'dk'```
 - *$variant-lighten*: ```'lt'```
 - *$variant-saturate*: ```'sat'```
 - *$variant-desaturate*: ```'dsat'```
 - config(```$colors, $variants, $attributes```) - Sets available color references.
   ```scss
   /* Any number of colors using a named map with corresponding css/sass compatible color values */
   $colors: (
     red: #f00,
     green: rgb(0, 255, 0),
     blue: blue,
   );
   /* Variants to generate for colors */
   $variants: (
     alpha: (.5,.9),
     invert: (50%,100%),
     adjust-hue: (30deg,60deg,90deg,120deg,150deg,180deg,210deg,240deg,270deg,300deg,330deg),
     darken: (20%,50%),
     lighten: (20%,50%),
     saturate: (20%,50%),
     desaturate: (20%,50%,90%),
   );
   /* Class names and corresponding attributes to create */
   $attributes: (
     text: (color, (base-only)),
     bg: background-color,
     bdr: (border-color, (red,blue)),
   )
   ```
 - properties() - Outputs all custom properties in given context.
 - styles() - Outputs all attribute color classes in given context.

#### + util / font

Supplies font styles for injection and styles with corresponding helper classes for usage.

 - *$class*: ```'ui-font'```
 - *$style-prefix*: ```'--'```
 - *$fluid-attribute*: ```'fluid'```
 - *$no-max-attribute*: ```'no-max'```
 - config(```$styles```) - Sets available style declarations.
   ```scss
   $styles: (
     
     /**
      * Simple font declaration
      *  Generated helper:
      *  .ui-font--default {
      *    font-family: Oxygen, sans-serif;
      *    font-size: 14px;
      *    line-height: 1.33;
      *  }
      */
     default: (
       font-family: (Oxygen, sans-serif),
       font-size: 14px,
       line-height: 1.33,
     ),
      
     /**
      * Simple media query based declaration
      *  Generated helper:
      *  @media screen and (min-width: 768px) and (max-width: 1024px) {
      *    .ui-font--default { font-size: 16px; }
      *  }
      */
     default_at_tablet: (
       font-size: 16px,
     ),
      
     /**
      * Fluid font size declaration without a max
      *  Generated helper:
      *  .font--headline-fluid { font-weight: bold; }
      *  @media screen and (max-width: 767px) {
      *    .font--headline-fluid { font-size: 20px; }
      *  }
      *  @media screen and (min-width: 320px) {
      *    .font--headline-fluid { font-size: calc(20px + 10 * ((100vw - 320px) / 447)); }
      *  }
      */
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
     
     /**
      * Fluid font size declaration with a max
      *  Generated helper:
      *  @media screen and (min-width: 1025px) {
      *    .font--headline-fluid { font-size: 35px; }
      *  }
      *  @media screen and (min-width: 1025px) {
      *    .font--headline-fluid { font-size: calc(35px + 15 * ((100vw - 1025px) / 341)); }
      *  }
      *  @media screen and (min-width: 1366px) {
      *    .font--headline-fluid { font-size: 50px; }
      *  }
      */
     headline-fluid_at_desktop: (
       fluid: (
         min-vw : 1025px,
         max-vw : 1366px,
         min-size : 30px,
         max-size : 50px,
       ),
     ),
   );
   ```
 - get(```$style```) - Outputs selected font style in given context.
 - styles() - Outputs configured font styles as helper classes.

#### + util / images

Supplies asset helpers and decal styles and helper classes and properties for usage.

##### + util / images / assets

 - *$base*: ```'../img/'```
 - *$cache*: ```''```
 - get(```$asset```) - Asset url.

##### + util / images / decals

 - *$class*: ```'ui-decals'```
 - *$static*: ```'--static'```
 - *$props*: ```'ui-decals-'```
 - *$width*: ```0```
 - *$sizing-as-props*: ```false```
 - config(```$decals```) - Sets available decals declarations.
   ```scss
   $decals: (
     example: (
   
       /* One of, before or after, must be set true */
       before: true,
       after: true,

       /* Dimensions must be defined and larger than zero */
       width: 1,
       height: 1,
   
       /* Gets passed through assets.get() */
       url: 'example.jpg'
     ),
   );
   ```
 - properties() - Outputs all custom properties in given context.
 - styles() - Outputs configured decal styles as helper classes.

#### + util / list

Supplies list normalization and customizable styles with corresponding helper classes for usage.

##### + util / list / customize

 - *$prop*: ```'data-counter'```
 - *$counter*: ```'ui-ol-counter'```
 - *$style*: ```decimal```
 - *$suffix*: ```'.'```
 - *$space*: ```'\00a0'```
 - *$styles*: ```(decimal, decimal-leading-zero, lower-roman, lower-alpha, upper-alpha, lower-latin)```
 - *$custom*: ```()```
 - styles() - Outputs configured component styles.

##### + util / list / normalize

 - *$class*: ```'ui-list'```
 - *$props*: ```'ui-list-'```
 - config(```$options```) - Only sets config options
   ```scss
   $options: (
     /**
      * List wrapper margin
      * @type {margin} 1-4 margin values
      */
     margin: 1rem 0,
   
     /**
      * List wrapper padding
      * @type {padding} 1-3 padding values
      */
     padding: 0 0 0,
   
     /**
      * List wrapper left indent/padding
      * @type {number} number with unit
      */
     indent-width: 2rem,
   
     /**
      * List item margin
      * @type {margin} 1-4 margin values
      */
     item-margin: 0,

     /**
      * List item after item margin
      * @type {margin} 1-4 margin values
      */
     item-after-margin: 1rem 0 0,
   );
   ```
 - properties() - Adds components custom properties in current scope
 - styles() - Outputs configured component styles

#### + util / media

Supplies a media query helper mixin and configuration.

 - config(```$queries```) - Only sets or updates media query references.
   ```scss
   $queries: (
     custom-breakpoint: 'screen and (max-width: 10rem)',
   );
   ```
 - query(```$query```) - Wraps given content styles in a media query.

#### + util / mixins

Only mixins and helpers that produce output, none of these contain configuration.

 - +attr-isset(```$attribute: 'class', $error: 'attr-isset::'```) - Wraps given content styles to apply only if the current scope element has no class attribute or its empty.
 - +attr-none(```$attribute: 'class', $empty: true, $error: 'attr-none::'```) - Wraps given content styles to apply only if the current scope element has no class attribute or its empty.
 - +attr-set(```$attributes, $error: 'attr-set::'```) - Adds the given attributes in current scope.
 - +attr-set-map(```$name, $source, $error: 'attr-set-map::'```) - Adds the given attributes in current scope.
 - +bem-style(```$nested, $font-styles: null, $query-marker: '_at_', $error: 'bem-style::'```) - Creates BEM style structures from a map definition.
 - +break-pseudo
   - break-before() - Inserts a pseudo before with a break.
   - break-after() - Inserts a pseudo after with a break.
 - +clear-pseudo
   - clear-before() - Inserts a pseudo before with a clear both.
   - clear-after() - Inserts a pseudo after with a clear both.
 - +font(```$style, $styles```) - Adds the given font attributes in current scope.
 - +font-fluid(```$style, $styles: null, $base-query: null, $fluid-attribute: 'fluid', $no-max-attribute: 'no-max', $error: 'font-fluid::'```) - Adds the given font attributes and media queries in current scope.
 - +font-fluid-base(```$min-vw, $max-vw, $min-font-size, $max-font-size, $base-query: null, $no-max: false, $error: 'font-fluid-base::'```) - Adds the given font media queries in current scope, with an optional base query.
 - +hide-accessible() - Inserts attributes to hide the current scope visually only.
 - +no-select() - Inserts attributes to prevent text selection.
 - +properties(```$props, $prefix: '', $error: 'properties::'```) - Adds given custom properties in current scope.

#### + util / reset

Supplies a basic reset stylesheet, has no configuration options.

 - styles() - Outputs reset styles.

#### + util / text

Supplies text accessibility, alignment, break helpers and some normalization.

##### + util / text / a11y

 - *$class*: ```'ui-text'```
 - *$hide-a11y*: ```'--hide-a11y'```
 - *$no-select*: ```'--no-select'```
 - styles() - Outputs configured accessibility helpers.

##### + util / text / align

 - *$class*: ```'ui-text'```
 - *$center*: ```'--center'```
 - *$center-queries*: ```(mobile, mobile-tablet-portrait, tablet-portrait, tablet-landscape, tablet, tablet-desktop, tablet-landscape-desktop, desktop, desktop-medium)```
 - *$right*: ```'--right'```
 - *$right-queries*: ```(mobile, mobile-tablet-portrait, tablet-portrait, tablet-landscape, tablet, tablet-desktop, tablet-landscape-desktop, desktop, desktop-medium)```
 - *$left*: ```'--left'```
 - *$left-queries*: ```(mobile, mobile-tablet-portrait, tablet-portrait, tablet-landscape, tablet, tablet-desktop, tablet-landscape-desktop, desktop, desktop-medium)```
 - styles() - Outputs configured alignment helper styles.

##### + util / text / breaks

 - *$class*: ```'ui-text'```
 - *$break*: ```'--break'```
 - *$clear*: ```'--clear'```
 - *$always*: ```'--break-always'```
 - *$none*: ```'--no-wrap'```
 - *$word*: ```'--wbreak'```
 - *$word-queries*: ```(mobile, mobile-tablet-portrait, tablet-portrait, tablet-landscape, tablet, tablet-desktop, tablet-landscape-desktop, desktop, desktop-medium)```
 - *$global*: ```false```
 - *$element-class*: ```'ui-break--'```
 - *$element-wrap-class*: ```'ui-break-wrap'```
 - *$queries*: ```(mobile, mobile-tablet-portrait, tablet-portrait, tablet-landscape, tablet, tablet-desktop, tablet-landscape-desktop, desktop, desktop-medium)```
 - styles() - Outputs configured break helper styles.

##### + util / text / normalize

 - *$props*: ```'ui-text-normalize-'```
 - config(```$options```) - Only sets config options.
   ```scss
   $options: (
   
     /**
      * Headline margin
      * @type {margin} full margin value
      */
     headline-margin: 1rem 0,

     /**
      * Paragraph margin
      * @type {margin} full margin value
      */
     paragraph-margin: 1rem 0,

     /**
      * Mobile text size adjust
      * @type {number} percent number
      */
     size-adjust: 100%,
   );
   ```
 - properties() - Adds components custom properties in current scope.
 - styles() - Outputs configured component styles.

#### + util / wrap

Provides a simple wrapping helper system.

 - *$class*: ```'ui-wrap'```
 - *$no-flex*: ```'--no-flex'```
 - config(```$options```) - Only sets config options.
   ```scss
   $options: (
     /* BEM mixin style declarations */
   );
   ```
 - styles() - Outputs configured component styles.

## Notes

Following some notes on sass behaviours directly relevant to using the library and modules.

### Resetting configs

With any modules that allow extending, config mixins can be reset the maps index to an empty list by passing an explicit *null* value, as following:

```scss
/* Clear all previously defined decals */
@include util.images-decals-config(null);

/* Add a new data set */
@include util.images-decals-config((
  example: (
    before: true,
    after: true,
    width: 1,
    height: 1,
    url: 'example.jpg'
  ),
));
```

### Use syntax

When loading via the *@use* syntax versus the classic *@import* ,there are a few things to keep in mind.
Using the *with* keyword to set any configuration variables can only be done the first time a module is loaded with *@use*, any attempt to do it differently will produce an error.

#### Changing configuration for multiple usages

If you wish to change configuration variables in specific situations, note that anything that module will do afterwards will use the new value even when loaded in a different context within the same compile tree.

You can set values from the given use context as following:

```scss
@use '~@squirrel-forge/sass-util' as util with (
  $images-decals-props: 'decal-',
);
/* This renders the initial configration */
:root { @include util.images-decals-properties; }

/* Then we change a config value and the output changes */
util.$images-decals-props: 'foo-';
.context { @include util.images-decals-properties; }

/* If we use this module again later or in another file loaded after the above code, */
/* then we need to reset the value if we want the initial setting */
util.$images-decals-props: 'decal-';
```

### Sass maps

Inside map declarations to use comma or space separated, list values, wrap them in braces to make them an explicit list value, for example for font-family declarations:

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

Check the sourcecode on [github](https://github.com/squirrel-forge/sass-util) for extensive comments.
