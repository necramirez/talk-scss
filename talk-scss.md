# SCSS

Most of the content are lifted verbatim from: [Sass Guidelines](https://sass-guidelin.es/)


## Allows us to

### Avoid magic numbers

### Do calculations

### Do color operations
  - `lighten()` / `darken()`

### Use nesting

#### `&`, current selector reference

##### Parent selector


## Notable features


### Variables

#### Use when
- the value is repeated at least twice
- the value is likely to be updated at least once
- all occurrences of the value are tied to the variable (i.e. not by coincidence)

#### `!default` flag
- allows a variable to be overwritten
- used when writing a library or framework

In `your-library.scss`:

```scss
// Library declaration
$baseline: 1em !default;
```

In `your-app.scss`:

```scss
// Your own variable
$baseline: 2em;

// Your library declaring `$baseline`
@import 'your-library';

// Inside `your-library`, $baseline == 2em
```


### Extend

#### Recommendations
- Use with placeholders (e.g. `%my-placeholder`)
- If used with actual selectors, only extend selectors that are logically related

#### Cons
- not possible across media contexts
- not flexible
- messes up ordering of rules
  - [Watch Out for Selector Order](https://css-tricks.com/the-extend-concept/#article-header-id-7)
  - See _Preserving source order_ section of [What Nobody Told You About Sass’s @extend](https://www.sitepoint.com/sass-extend-nobody-told-you/)
- groups together all extending selectors, so unrelated selectors might be grouped together

#### Understand

From [When to use @extend](https://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/#when-to-use-extend):
> `@extend` creates relationships

> misusing `@extend` can create relationships around the wrong criterion


### Functions


### Mixins

- more flexible than `@extend`
- can have arguments
  - with optional default values
  - with names

```scss
@mixin axa-button($button-bg-color: #777, $button-text-color: #fff) {
    background-color: $button-bg-color;
    color: $button-text-color;
}

.quote-form {
    .submit-button {
        // "normal" usage
        @include axa-button(#0f0);
    }

    .cancel-button {
        // passing no arguments would use the default parameter values
        @include axa-button;

        // same as doing this
        @include axa-button(#777, #fff);
    }

    .ok-button {
        // using names makes it more readable
        @include axa-button($button-bg-color: #00f, $button-text-color: #eee);

        // and allows you to skip some parameters
        @include axa-button($button-text-color: #ff0);
    }
}
```

One of the most popular examples (as featured in the [official documentation for mixins](http://sass-lang.com/guide#topic-6)) deals with vendor prefixes:

```scss
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box {
    @include border-radius(10px);
}
```


# References

- [The Extend Concept](https://css-tricks.com/the-extend-concept/) by Chris Coyier, CSS-Tricks
- [Why You Should Avoid Sass @extend](https://www.sitepoint.com/avoid-sass-extend/) by Hugo Giraudel, Sass Guidelines
- [When to use @extend; when to use a mixin](https://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/) by Harry Roberts, CSS Wizardry
- [What Nobody Told You About Sass’s @extend](https://www.sitepoint.com/sass-extend-nobody-told-you/) by Hugo Giraudel, Sass Guidelines


# Other CSS processors
- Post-processors
    - [PostCSS](https://github.com/postcss/postcss)
        - [Autoprefixer](https://github.com/postcss/autoprefixer)
