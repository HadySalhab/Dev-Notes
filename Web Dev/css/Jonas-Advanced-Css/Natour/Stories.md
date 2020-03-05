# Natour

## <u>Building the story section</u>

### Note Mentioned

- Use `transform:translate` property on a floated element instead of `margin`

#### what we learned:

```scss
backface-visibility: hidden; // used to remove bugs that results from animation

filter: blur(3px) brightness(80%); //make the image blury and any value passed to brightness less than 100% will darken the image

//clip the image at the shape specified
//in this case its a circle
-webkit-clip-path: circle(50% at 50% 50%);
clip-path: circle(50% at 50% 50%); //radius is 50% the width of the parent,

//this is a handy property to create a shape outside of an element
//was used to create a circle shape on the text around the image
-webkit-shape-outside: circle(50% at 50% 50%);
shape-outside: circle(50% at 50% 50%);
```
