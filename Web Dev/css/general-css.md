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

- Fuild Grid : all layout elements are sized in relative unites: % , rem...
- Flexible Images: all images should be sized using relative unites
- Media queries
