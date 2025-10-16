# @squirrel-forge/sass-util

Collection of sass abstracts, mixins, globals and utilities.
Built for the dart-sass *@use module syntax*, allowing for full and individual feature usage.

*Please Note* that from version **0.9.0** the package is fully based on the *@use module syntax*, if you are looking for the old version using the @import syntax install version **0.8.x**, but consider migrating to the **0.9.x** standard to avoid missing out on updates. 

## Installation

```
npm i @squirrel-forge/sass-util
```

## Usage

Make use of your IDE's autocompletion or checkout the [docs example](https://squirrel-forge.github.io/sass-util), [example scss sheet](example/util.scss) and the [generated output](docs/util.css).  
Note that the *@use* syntax works differently than the classic *@import*, check the [use syntax notes](#use-syntax) for relevant details and or refer to the [official sass docs](https://sass-lang.com/documentation/at-rules/use).

```scss
/**
 * Using the full library
 */
@use '~@squirrel-forge/sass-util' as util;

/**
 * You may use only the modules or submodules you require
 */
@use '~@squirrel-forge/sass-util/media';
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
@use '~@squirrel-forge/sass-util/media';
@include media.config((
  custom-breakpoint: 'screen and (max-width: 10rem)',
));
@include media.query('custom-breakpoint') {
  // @content
}
```

Not recommended, but possible: If you wish to use modules more than once and require configuration changes,
then you need to modify the namespaces variables directly, but keep in mind that the values change permanently even for other contexts and need to be reset manually, since modules are only loaded once.

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

When loading via the *@use* syntax versus the classic *@import*, there are a few things to keep in mind.
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
