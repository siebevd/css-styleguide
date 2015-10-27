# CSS Guidelines

Style guide for writing CSS.
Still a work in progress.

1. [Naming](#naming)
2. [Specific Class name prefixes](#classPrefixes)
3. [Selector Blocks](#selector)
4. [Basic Formatting](#formatting)
5. [Comments](#comments)
6. [Variable Naming](#variableNaming)
7. [Organization](#organization)

##<a name="naming"></a> Naming

Naming classes is one of the most difficult things, certainly when you start scaling your project. Using the BEM - Block, Element, Modifier - system makes this a lot easier.

- Block: the higher level of a component.
- Element: a descendant (child) of the block. Notation ex. ``block__element``
- Modifier: different state or version. Notation ex. ``block--modifier``

It uses double hyphens & underscores so we can still describe the block without having to use CamelCase. eg. ``modal-box__content--small``

eg. BEM Notation
```
<div class="gallery">
  <h1 class="gallery__title">Gallery</h1>
  <img class="gallery__image gallery__image--large" />
  <img class="gallery__image" />
  <img class="gallery__image" />
</div>
```
```
.gallery { background: #fff ; } /* Block */
.gallery__image { margin: 20px;} /* Element */
.gallery__image--large { width: 200%; } /* Modifier */

```

vs

```
<div class="gallery">
  <h1 class="title">Gallery</h1>
  <img class="image large" />
  <img class="image" />
  <img class="image" />
</div>
```

```
.gallery {
    background: #fff;

    .gallery__image {
        margin: 20px;
        &.large {
            width: 200%;
        }
    }
}
```

Thanks to BEM, the class names will make more sense and provide more context about the purpose of the class. It will also keep nesting as low as possible.
Also try to keep naming as short as possible while still keeping it understandable (eg. nav instead of navigation).


##<a name="classPrefixes"></a> Specific Class name prefixes

To make the code clearer, there are some prefixes we use in front of the classnames.

### Utility Classes
Utility classes are used for certain css properties that get used frequently. Some examples: Floats, Alignment. Start each utility class with  ``u-``, proceeding with clear naming to clarify the utility


```
<div class="u-textCenter">
  <div class="u-floatLeft"></div>
  <div class="u-floatLeft"></div>
  <div class="u-floatLeft"></div>
  <div class="u-clearFix"></div>
</div>
```


### State Classes


For state changes of components, use ``is-state`` class names. These classes shouldn't be used for basic styling, but only for minor changes depending on the state, they should always be used as an adjoining class.

They will mainly be used together with javascript. State Classes aren't be component specific, so each component should have it's own styling applied
```
<div class="menu">
    <a href="home" class="menu__link">Home</a>
    <a href="about" class="menu__link is-active">About</a>
    <a href="home" class="menu__link">Content</a>
</div>
```

##<a name="selector"></a>  Selector Blocks
- include a space before the opening bracket of a selector.
- end the selector block with a closing bracket on a seperate line.
- if you have multiple selectors for a ruleset, use one selector per line.
- Keep a blank line between blocks.

```
div {
    margin: 0;
}

a,
button,
.btn {
    border: 1px solid #000;
}
```


##<a name="formatting"></a> Basic Formatting
The code throughout the codebase should be written with the same formatting rules in mind too ensure that the code stays maintainable & easy to read.

- only use double quotes to keep it consistent.
- avoid specifying units for zero-values eg. ``padding: 0;``.
- include a space after each comma  eg. ``transform: translate3d(0, 0, 0);``.
- put spaces between every property and value and before the opening brace.
- include a semi-colon at the end of every declaration (including the last one).
- When selecting HTML elements, write the selector in lowercase.
- if there is only a single declaration, put it on one line, for better readability (put spaces before and after the declaration).
- Don't prefix property values or color parameters with a leading zero e.g. ``.5%``instead of ``0.5%``.
- lowercase all hex values, e.g., ``#fff. ``.
- try to keep nesting as low as possible

```
p { font-size: 20px; }

a {
  font-size: 15px;
  margin-bottom: 0;
  opacity: .5;
}
```


##<a name="comments"></a>  Comments
Comments are strongly encouraged, to make sure that the written code will still be understandable for new developers. The style of the comments should be consistent throughout the whole codebase.
There are 3 different types of comment blocks that you can use. Try to write them in full sentences, and don't simply retype the classname or component.

### The main comment block
Should be put at the top of every new file (Sass) to explain the purpose of that file and the styles in it. Or to include optional context for the component.
```
/*
 *
 * Some copy explaining this component
 *
 */
```

### Subsections
Everytime you start a new subsection in a file, give it a clear comment. This way the file will stay maintainable.
```
/* Sidebar header
----------------------------------*/
```

### Small comments
To clarify specific lines of code or write todo's
```
    /* TODO: clean up comments */
```


##<a name="variableNaming"></a>  Variable Naming
Variable naming often runs into the same problem as class naming. So it's best to have some guidelines for them as well, to keep it consistent. Always start with the property it affects, then go for the value and add it an modifier (like with BEM) for specific use cases.
User CamelCase notation for properties which have dashes in them (eg. font-family -> fontFamily)

examples

```
/* Color Variables
----------------------------------*/
$color-red: #ff0000;
$color-green: #00ff00;

/* Font Variables
----------------------------------*/
$fontFamily-base: 'Lato', sans-serif;
$fontFamily-serif: 'Times New Roman', serif;

$fontSize-title: 32px;
$fontSize-regular: 16px;

```

##<a name="organization"></a> Organization
Organization is really important to keep a codebase maintainable. Organize sections of code by component, if you are using sass, keep a clear file structure. Try to do as much as possible component related (ex. buttons, modal box), and try to stay away from page specific code.


### Media query placement
Place the media queries as close to the related css as possible (no unique responsive scss file), Try to group all the media queries together at the bottom of a file, don't use the same query twice in one file.


### Folder Structure
 - core
    - variables
    - utilities
    - mixins
    - animations
    - reset
    - base

- components
    - buttons
    - forms
    - modal
    - ...

- pages
    - home

- style.scss  // Base file with imports
