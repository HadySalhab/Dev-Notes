# General Notes

- All elements in css their heights behave as wrap-content by default
- Use `transform:translate` property on a floated element instead of `margin`
- Always good practise to include everything related to default font styling in the `body` element, that way its going to be inherited by all elements in the html.

  - font-family
  - font-weight
  - font-size
  - line-hegiht
  - color

Example:

```css
body {
  font-family: "Lato", sans-serif;
  font-size: 16px;
  font-weight: 400;
  line-height: 1.7;
  color: #777;
  padding: 30px;
}
```

## Common Images Properties

```css
background-size: cover; /* whatever the width is, will always try to cover the area of its box*/
background-position: top; /*will always ensure that the top of the image is always visible no matter what,  we can use bottom,center...*/

background-image/*can set more than one image to it*/

linear-gradient(to-where or degree,color-stop1,color-stop2...)
linear-gradient(to right bottom , rgba(..),rgba(..),...)
linear-gradient(45deg,red,blue,...)

background-image: linear-gradient(to-where, color-stop1, color-stop2...),
  url(""); /*will set two images (linear-gradient and the url)*/

clip-path: polygon(
  first-point-x first-point-y,
  second-point-x second-point-y,
  third-point-x third-point-y,
  ...
);
```

### [clip-path resource](https://bennettfeely.com/clippy/)

## Responsive Web Design

### Main Ingredient

- Fuild Grid : all layout elements are sized in relative unites: % , rem...(Float layouts,Flexbox,CSS Grid)
- Flexible Images: all images should be sized using relative unites
- Media queries

---

- Always good practise to put an inline element like image inside a block level element

```css
letter-spacing: 35px; //creates spacing among letters
```

### Animation

Animation in css is created using `@keyframes` and `animation` property

```css
animation-name: slideUpBottom;
animation-duration: 1s;
animation-timing-function: ease-out;
animation-delay: 0.75s;
animation-fill-mode: backwards; /*will apply the style of the 0% animation before the animation starts*/
```

Bugs Can result from animations, like shaking, common way to solve these bugs is to apply `backface-visibility: hidden;` on the element which the animation is being applied on

## pseudo selector for link

```css
:hover {
} //when the mouse is hovered over an element
:active {
} //when the element is clicked (mouse down)
```

## box-shadow

```css
box-shadow: none|h-offset v-offset blur spread color |inset|initial|inherit;
```

## Tips

- Inline elements cannot be style with box-model properties
- since inline elements behave like a text, to center them inside a block element , we can use `text-align:center`
- to target the ::after element when the element itself is in hover state -> `element:hover::after`
- if 2/more elements share the same styling, combine these styles in 1 common class then create a different style for each that hold the unique styling (we are composing the styling of an element)
- good practice to include the general reset to `after` and `before` pseudo selectors
- Always use % to size images in your css.

```css
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}
```

## CSS CODE COMPONENT

- Responsive Design
- Maintainable And Scalable code
- Web performance

## BEM

- Block: standalone component that is meaningful on its own
- Element: part of a block that has no standalone meaning
- Modifier: a diff version of a block or an element.

- `.block{}`
- `.block__element{}`
- `.block__element--modifier{}`

## CSS Architect

- base/
- components/
- layout/
- pages/
- themes/
- abstracts/
- vendors/

## SASS Features

- Variables: for reusable values such as colors, font-sizes, spacing, etc.
- Nesting: to nest selectors inside of one another, allowing us to writes less code.
- Operators: for mathematical operations
- Partials And Imports: to write CSS in different files and import
- Mixins: to write reusable pieces of CSS code
- Functions: like mixins but they produce value that can be used
- Extends: to make diff selectors inherit declarations that are common
- Control Directives: for writing complex code using conditionals and loops

```scss
.header {
  &-main {
    // ".header-main"
  }
  &-about {
    // ".header-about"
  }

  li {
    //".header li"
    a {
      // ".header li a

      &:hover {
        // ".header li a:hover"  and NOT ".header li a a:hover"
      }
    }
  }
}

// & does not append a selector , it replace the parent selector instead
```
