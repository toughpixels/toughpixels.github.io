---
title: "Using SASS to Create a Lean Utility Library"
date: 2021-03-02T21:15:55-06:00
tags: 
description: "Write mixins with SASS to generate utility classes that speed up the development of your site."
draft: false
---

## An alternative to Tailwind CSS

Tailwind CSS is great but requires precious build minutes when using a service like Netlify.  This is especially true when using Purge CSS.  A faster alternative is to decide which utility classes are useful for your project, and build those with the power of SASS mixins and functions.

## Useful Utility Classes

Here are some examples of the types of utlity classes you may want.

### Color Classes
Like these:

```
.bg-light {
  background-color: #fafafa; }

.bg-dark {
  background-color: #030303; }

.bg-primary {
  background-color: #9100b6; }

.c-light {
  color: #fafafa; }

.c-dark {
  color: #030303; }

.c-primary {
  color: #9100b6; }
```

First create an array of arrays of properties you want to add colors to.

```
$colorProperties: (
    ('bg-', 'background-color')
    ('c-', 'color')
);
```

Then decide what your color options are (these can be a simple 1-1 map):

```
$colorOptions: (
  light: #fafafa,
  dark: #030303,
  primary: #9100b6
);
```

Here's what our mixin looks like:

```
@mixin generateUtilityClasses($properties, $options) {
  @each $item in $properties {
    $classPropertyText: nth($item, 1);
    $cssProperty: nth($item, 2);
    @each $classValueText, $cssValue in $options {
      .#{$classPropertyText}#{$classValueText} {
        #{$cssProperty}: $cssValue;
      }
    }
  }
}
```
### Spacing Utility Classes

Sometimes we want to generate some utility classes like this:

```
.space-y-xs > * + * {
  margin-top: 0.5rem; }

.space-y-sm > * + * {
  margin-top: 1rem; }

.space-y-md > * + * {
  margin-top: 2rem; }

.space-x-xs > * + * {
  margin-left: 0.5rem; }

.space-x-sm > * + * {
  margin-left: 1rem; }

.space-x-md > * + * {
  margin-left: 2rem; }
```

Note that after every utility class, there is a `> * + *` part of the selector.  This is what we'll add to a new, 3rd part of our array:

```
$gapProperties: (
    ('space-y-', 'margin-top', '> * + *'),
    ('space-x-', 'margin-left', '> * + *')
);
```
And our properties look like this:

```
$gapOptions: (
  'xs' : 0.5rem,
  'sm' : 1rem,
  'md' : 2rem
);
```

Now we'll include a `$selectorAdditional` variable as a part of the new mixin:

```
@mixin generateUtilityClasses($properties, $options) {
  @each $item in $properties {
    $classPropertyText: nth($item, 1);
    $cssProperty: nth($item, 2);
    $selectorAdditional: nth($item, 3);
    @each $classValueText, $cssValue in $options {
      .#{$classPropertyText}#{$classValueText} #{$selectorAdditional} {
        #{$cssProperty}: $cssValue;
      }
    }
  }
}
```
{{< aside type="note" >}}
#### Note
Now that our mixin expects `nth($item, 3)`, we have to update our colors array to:
```
$colorProperties: (
    ('bg-', 'background-color', '')
    ('c-', 'color', '')
);
```
{{< /aside >}}

### Display Utility Classes

Some utility classes don't need a CSS class prefix like these:
```
.none {
  display: none; }

.inline {
  display: inline; }

.inline-block {
  display: inline-block; }

.block {
  display: block; }

.flex {
  display: flex; }

.grid {
  display: grid; }
```

Here are the related properties / options vars:

```
$displayProperty: (
  ('', 'display', ''),
);
$displayOptions: (
  none: none,
  inline: inline,
  inline-block: inline-block,
  block: block,
  flex: flex,
  grid: grid
);
```
{{< aside >}}
### Note 
`('', 'display', ''),` has a trailing comma.  SASS will give you an error if it's not there.
{{< /aside >}}


### Responsive Utility Classes

It's also nice to have classes like these:

```
.none {
  display: none; }

.block {
  display: block; }

@media (min-width: 768px) {
  .sm\:none {
    display: none; }
  .sm\:block {
    display: block; } }
```

Here's the associated property and options arrays:

```
$displayProperty: (
  ('', 'display', ''),
);
$displayOptions: (
  none: none,
  block: block,
);
```

But now we also want to create a breakpoints map:
```
$breakpoints: (
    sm: 768px
);
```

And use another mixin:

```
@mixin respond($media) {
	@each $name, $width in $breakpoints {
		@if $media == $name {
			@media (min-width: $width) { @content; }
		}
	}
}
```

{{< aside >}}
### Bonus
Using this mixin, you can create CSS like this:

```
img {
  width: 100%;
}
@media (min-width: 768px) {
  img {
    float:right;
    max-width: 50%;
  }
}
@media (min-width: 1040px) {
  img {
    max-width: 30%;
  }
}
```
... by starting with a breakpoints map like this:
```
$breakpoints: (
    sm: 768px,
    md: 1040px
);
```
... and SASS like this:

```
img {
  width: 100%;
  @include respond(sm) {
    float:right;
    max-width: 50%;
  }
  @include respond(md) {
    max-width: 30%;
  }
}
```
{{< /aside >}}

{{< aside >}}
### Tip
Try to use one or two breakpoint options if any at all.  Fewer breakpoint options means a smaller CSS file size!
{{< /aside >}}

Here's our new mixin, now incorporating the `responsive` mixin:

```
@mixin generateUtilityClasses($properties, $options, $responsive: false) {
  @each $item in $properties {
    $classPropertyText: nth($item, 1);
    $cssProperty: nth($item, 2);
    $selectorAdditional: nth($item, 3);

    @each $classValueText, $cssValue in $options {
      .#{$classPropertyText}#{$classValueText} #{$selectorAdditional} {
        #{$cssProperty}: $cssValue;
      }
    }
    @if($responsive) {
      @each $breakpointName, $width in $breakpoints {
        @include respond($breakpointName) {
          @each $classValueText, $cssValue in $options {
            .#{$breakpointName}\:#{$classPropertyText}#{$classValueText} #{$selectorAdditional} {
              #{$cssProperty}: $cssValue;
            }
          }
        }
      }
    }
  }
}
```

### Fancy Utility Classes
Some utility classes are too complex for the above mixin to generate.  But we can write custom mixins for custom needs.  
#### For example:

Sometimes you might want to visually shift an element

{{< containerPull type="left" >}}over here{{< /containerPull >}}

or 

{{< containerPull type="right" >}}over here!{{< /containerPull >}}

The classes that are pulling that text are built based on the max-width of the `.container` element, so this is a great opportunity to make all these classes with a single mixin:

```
@mixin generateContainerOverrides($containerMaxWidth) {
  .container {
    padding: 0 15px;
    margin: 0 auto;
    max-width: $containerMaxWidth;
  }
  .containerPull {
    &-left {
      margin-left: -15px;
      @media screen and (min-width: $containerMaxWidth) {
        margin-left: calc($containerMaxWidth/2 - 50vw);
      }
    }
    &-right {
      margin-right: -15px;
      @media screen and (min-width: $containerMaxWidth) {
        margin-right: calc($containerMaxWidth/2 - 50vw);
      }
    }
    &-both {
      margin: 0 -15px;
      @media screen and (min-width: $containerMaxWidth) {
        margin: 0 calc($containerMaxWidth/2 - 50vw);
      }
    }
  }
}
```
You would then generate these classes by running:
```
@include generateContainerOverrides(70rem);
```

## Abstracting Classes
Once you have your utility clsses, you can optionally abstract them out using SASS extends like this:

```
.btn {
  @extend .inline-block, .bg-primary, .c-dark;
}
```

{{< aside >}}
### Bonus
Challenge yourself to abstract out your HTML instead!  For example, you could make a "btn" shortcode in Hugo and add all these utility classes there as HTML classes.  You'll get the same styles but will save a little bit of CSS.
{{< /aside >}}

