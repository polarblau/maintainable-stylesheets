# Best practices

## CSS & Sass

### General

* Keep one empty line between rules
* Keep the opening bracket for style definitions on the same line as the selector, the closing bracket on it's on line (CSS only)
* Use two spaces for indentation with Sass and one tab with CSS
* Don't prefix IDs with tag selectors


### Headers

* Add headers to each new CSS file which identify
** the author of the file
** the purpose

### Comments

* Use comments to group sections where applicable. 
* Insert comments before selectors rather then within styledefinitions.


### Fonts

* Define font sizes in `em`
* Use mixins to define and re-use styles for custom fonts
* Avoid weight definitions like `font-weight: strong` with custom fonts, but use the correct weight instead


### Images

* Use absolute image paths if possible.


### Hacks

* Avoid so called "CSS hacks" targeting specific browsers, rather use conditional comments in combination with separte stylesheets or html/body classes.
* If you feel that you absolutely must use a "hack", try to target legacy browsers with major version numbers of two and more lower than the current. In these cases it's pretty save to assume that the vendors are aware of the "hack" and have fixed the flaw that makes it possible in later versions.


### Sass 


#### Selectors

* Don't nest selectors deeper than 5 levels max -- makes longer stretches of styles harder to read and produces overly verbose CSS


#### Variables

* Use variables sparsely and for clearly define purposes only (e.g. for colors)
* Keep all variable definitions in a separate file


#### Mixins

* Define mixins in separate files, sorted according to their purpose


#### Scripting

* Try to avoid scripting within style definitions, rather use mixins