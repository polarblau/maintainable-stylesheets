# Best practices

## CSS & Sass

### Headers

Add headers to each file which identify for the least 
* the author(s) 
* the intended purpose (the more detailed the better)

### General

* Keep one empty line between rules
* Keep the opening bracket for style definitions on the same line as the selector, the closing bracket on it's on line (CSS only)
* Use two spaces for indentation with SASS and one tab with CSS
* Don't prefix IDs with tag selectors


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


### SASS 


#### Selectors

* Don't nest selectors deeper than 5 levels max -- makes longer stretches of styles harder to read and produces overly verbose CSS


#### Variables

* Use variables sparsely and for clearly define purposes only (e.g. for colors)
* Keep all variable definitions in a separate file


#### Mixins

* Define mixins in separate files, sorted according to their purpose


#### Scripting

* Try to avoid scripting within style definitions, rather use mixins



## HTML & Haml

### General

* Separate content, style and behaviour categorically:
** Don't use tables for layout purposes
** Select tags exclusively according to the content you're trying to mark-up, never because their visual appearance (which anyways is fully depending on the browser used unless a altered using stylesheets)


#### Doctype

* All mark-up are written following the HTML5 specifications (--at least to a degree reasonable, given that the specifications are incomplete to date): Always use the proper docytype:

*HTML*

```HTML
<!DOCTYPE html>
```

*Haml*

```Haml
!!! 5
```


#### Tags

(The following does apply to actual HTML only.)

* All tags are written lowercase.
* Close all tags (the HTML5 specs don't require this anymore in all cases, but ensure backwards compatibility we stick to closed tags for now).
* Validate (at least in case of errors and problems). Use an IDE extension or one of the existing online services to ensure your mark-up is standard compliant.


**Lists**

* HTML allows three different list types (ordered, unordered and definition lists). Use the right type for the job at hand based on the content.
* Wrap navigational links into unordered lists where appropriate.
* Supply headers to lists where appropriate.
* Don't nest lists deeper than three levels


**Headings**

* Keep headings in a hierarchial order (h1, h2, h3, ...)
* Don't skip levels
* Use the H1 heading as the main heading (usually the page title)


**Links**

* Use descriptive links (avoid "click here" and the likes)


**Images**

* Provide a meaningful description in a alt attribute
* Define size using width/height attribute if possible (usually not the case with responsive layouts)


**Forms**

* Group input elements logically using fieldset
* Each form should contain at least one fieldset
* Use `<legend />` to describe a fieldset
* Wrap asterisks marking a required field into an `<abbr />` tag with appropriate `title` attribute (e.g. "required")
* Display validation errors (as well) inline, not only at the top of the form in a big list
* Highlight fields which failed validation clearly
* Define tabindices where appropriate
* Implement client side validation in addition to server side validation whereever possible


**Input elements**

* Prefer `<button/>` tags over `<input />` tags when possible
* Define a `name` attribute, no need to define an ID in every case, especially if the value matches the `name`
* Use labels and assign them using the `for` attribute to the input they're describing
* Don't rely on the `placeholder attribute to describe which type of data an input expects
* Define `rows` and `columns` attributes on textareas
* Use the `<optgroup />` tag to group options in selects
* Always define complete attributes, use e.g. `checked="checked"` instead of simply `checked`
* Define an `accesskey` attribute where appropriate (e.g. for the searh field)
 

#### Presentation

**Use semantically meaningful elements**

Remind yourself that your mark-up has the main purpose of structuring content. Choose the elements of this structure therefore according to the content, never the layout.
Consider the many devices and application which will consume the content in many different ways and the influence mark-up can have on the look will fade into the background.

Use a browser tool to turn of all CSS styles every now and then to simply check the structure. 


**Separate content and presentation**

Content first: Chose the structure of your mark-up based on your content, not the look of your site.
Add semantically meaningless wrappers to achieve the layout you want, but sparingly only. Deeply nested `<div />` tags are often an indication of a bad design.
Don't use purely presentational (and deprecated) mark-up such as `<font />`, `<b />` or `<i />`.
Avoid content which really only serves a presentational purpose as mark-up.


### Attributes

#### IDs

IDs are called **unique** identifiers for a reason. Each ID must not be used more than once per page to avoid unexpected results across the stack.


#### Class names

**General**

It's incredibly easy to end with a mess when working on HTML and CSS documents with more than one person (often even one is  enough). Hence, select class names foremost for your fellow developers and your own bad memory. Contrary to what some believe, class names are irrelevant for search engine optimization and even screen readers.

* Keep all class names fully lower case only. 
* Only use alpha-numeric characters. 
* Don't start class names with numbers.
* Don't abbreviate.


**Keep it short and clear**

Try to keep class names as concise and clear as possible. Use semantically meaningful names, but don't go too far - sometimes overly descriptive class names prevent re-use.
Brevity is often the first step to clarity. If you can guess a class names someone else on your team has selected, you're on the right track.


**Don't name classes after visual appearance**

A class name should have semantic meaning just as much as the mark-up. A class name such as `.big-headline-red` becomes meaningless as soon as the CSS rules change, the scope for the content switches (consider the e-use of partials with different layouts) but especially in conjuctional use with media queries in responsive layouts.


**Dashes as separators**

If you find yourself in the need to construct CSS class names of two or more words, use dashes (`-`) to join them, *not underscores*. Stay consistent.


**Stay clear of variations wherever possible**

Class names like `.foo-1, .foo-2, .foo-3, ...` should raise a red flag. Chances are that you can achive the desired outcome through a different selector or that your mark-up and/or design is flawed. Consider this a soft rule.


**Avoid overuse**

Avoid the overuse of classes, especially for the use with stylesheets. Instead make use of CSS tag selectors.
If you find yourself writing the same class name over and over (especially on sibling elements), chances are that you doing wrong:

*Avoid this:*

```HTML
<ul class="my-list">
	<li class="list-element">Foo</li>
	<li class="list-element">Bar</li>
	<li class="list-element">Baz</li>
	<li class="list-element">Bat</li>
</ul>
		
```

```CSS
.list-element {
	color: red;	
}
```

*But rather do this:*
```HTML
<ul class="my-list">
	<li>Foo</li>
	<li>Bar</li>
	<li>Baz</li>
	<li>Bat</li>
</ul>
		
```

```CSS
ul.my-list li {
	color: red;	
}
```


#### Titles

Title attributes can improve accessiblity dramatically for *all* users. Use them whenever appropriate. 
Don't just copy the content of a link or the alt tag of an image, though -- only add a title attribute, if you have something additional to say, which isn't already visible to the user. 


#### Alt attributs for images

Depending on device, browser and user not everyone will actually be able to "see" images. Supply meaningful and descriptive alt attributes for all (content) images as a text-only fallback for such cases.


### CSS and javascript

**Style**

Simply avoid `<style />` tags and `<script />` tags without source attribute, because it's an unexpected location for this type of code, not to mention more technical side effects increase in filesize, blocking, etc.. 

Even more hazardous are `style` attributes for tags. Inline CSS is very specific and therefore can be overriden in most cases only by using `!important` declarations, which makes it really hard to find bugs.

Simply avoid javascript in your HTML/Haml files alltogether.
We're using jQuery to target HTML elements and bind events -- no need to attach events through e.g. `onclick` attributes or worse by `javascript:` definitions in e.g. link locations.


### Comments

Comments sparsely. Rarely to never you'll need or even want the end-user to read your comments. Comments are targeted at your fellow developers and yourself.
So, when using Haml, use a comment type your parser will strip out when compiling to HTML. 

For Ruby use e.g.:

```Haml
-# Comment 
%h1 Foobar
%p Lorem ipsum...
```