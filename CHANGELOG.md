# Changelog

## 0.9.7
 - Changed filesystem structure for better imports and autocompletion.

## 0.9.6
 - Added more icons.
 - Some *button* module tweaks and improvements.

## 0.9.5
 - Added a basic button styles module, core and styled variant.
 - Added *all()* function to *font* module to get the full fonts map.

## 0.9.4
 - Added *merge-optional* abstract function.
 - Extended *properties* mixin with *media.query* support.
 - Removed the js placeholder.

## 0.9.3
 - Remove local css maps.
 - Move example *util.scss* to its own folder.

## 0.9.2
 - Updated build script arguments.
 - Fixed a flow control typo/deprecation.
 - Fixed a division deprecation and replaced with *math.div*. 

## 0.9.1
 - Added mixin *wordbreak*.
 - Added *icons* module with *styled* css icons and *images* icon helpers.
 - Added a bunch of default styles icons.

## 0.9.0
 - *Breaking changes!*
 - Complete module refactor, rebased all code for *use syntax* with configuration variables and mixins.
 - Improved error handling and namespacing.
 - Added *images.assets* and *images.decals* module.

## 0.8.8
 - Added *mobile.classic* default media query.
 - Added *button cursor* and *fieldset border* to reset styles.

## 0.8.7
 - Added *mobile-mini*, *mobile-medium*, *mobile-large*, *desktop-mini* and *desktop-classic* default media queries.
 - Added prototype *fn-spacing* dynamic padding/margin/inset list value generator.
 - Added *margin* and *padding* "0" to button/inputs reset.

## 0.8.6
 - Added *mobile-tablet* default media query.

## 0.8.5
 - Added media *desktop-nano* as 1152px break point.
 - Fixed example data query references for *small* to *mobile-small*.

## 0.8.4
 - Fixed *media* defaults to ensure unique initials.
 - Updated all corresponding default vars with *media* changes.

## 0.8.3
 - Fixed *util-break* class names missing dash separator. 

## 0.8.2
 - Fixed *util-prefix* default value.
 - Added basic util class customizations.
 - Added *details* and *summary* to reset styles.

## 0.8.1
 - Updated style export to use the minified build.
 - Updated dev dependencies.

## 0.8.0
 - Added colors generator, generates css vars and supplies a list of names generated.
 - Added color utilities, defaults include color, border-color and background-color.
 - Added *fn-dynamic-default-args* to handle dynamic default arguments.

## 0.7.1
 - Fixed *mx-bem* query issues and reduced to one query marker.
 - Migrated to new sass module functions.
 - Improved readme docs.

## 0.7.0
 - Added *fn-has-query* to check strings for query parts.
 - Added *fn-is-query* to check if string is a query.
 - Added *str-split* completed version with no-empty option.
 - Improved and extended nesting options for *mx-bem* mixin.
 - Added customizable query prefix and marker strings.
 - Added *no-max* option to *mx-font-fluid* and *mx-font-fluid-base* to prevent the upper min query from being rendered.
 - Improved font util declaration handling.
 - Added some work in progress default wrap styles.
 - Added some work in progress default font styles.

## 0.6.2
 - Added box-sizing for pseudo before and after elements.
 - Fixed some typos.

## 0.6.1
 - Added a readme overview of contents.

## 0.6.0
 - Switched builder to [@squirrel-forge/build-scss](https://www.npmjs.com/package/@squirrel-forge/build-scss).
 - Updated package data.
 - Added *.browserslistrc*

## 0.5.0
 - Core features prototype.
