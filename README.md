# Tequilla

If everyone else can name their sass modules after alcoholic beverages, why don't I
do it too?

## Whats under the hood?

### Basic mixins

#### Define type scale
```
@include define-type-scale((
    scale: 1.414,
    base-size: 1,
    base-weight: 400,
    line-height: 1.45
));
```
Requires [math module](https://github.com/sass-eyeglass/eyeglass-math)

Set up font scaling on your webapp using http://type-scale.com/
If you have a designer, ask them to provide you with a link from this site (if not, grab it yourself) - it should resemble:
http://type-scale.com/?size=16&scale=1.414&text=CSS%20Architecture%20for%20large-scale&webfont=Libre+Baskerville&font-family=gotham&font-weight=400&font-family-headers=&font-weight-headers=inherit&background-color=white&font-color=%23333
The options array takes the same parameters as $type-scale, defaults are defined in $type-scale-base;

### Generators

#### Angle
```
.class-name {
    @include angle(after, false, 1.5deg);
}
```
Angle is a mixin for drawing slanted boxes (because svgs are annoying to maintain).
It takes 3 parameters, the first is the pseudo selector that the slanted section
should be placed onto; before, after or both.

The second parameter if whether the angle should be flipped or not, depending on
which direction you want the slant to go.

The third and final parameter is the angle at which you want the slant to go.

This feature was taken from
[here](https://viget.com/inspire/angled-edges-with-css-masks-and-transforms)

#### Arrow
```
.class-name {
    @include arrow(up, 10px, red);
}
```
This mixin is used to draw arrows on blocks, and takes the parameters: the direction:
which way you want the arrow to point (up, down, left or right); the size:
how big you want the arrow to be and the color that you want the arrow to be.

#### Color set
```
@include color-set(btn, $color-map, true);
```
Color set is a mixin for generating a set of something e.g. buttons. The first
argument is what you want to prepend all of your color scheme classes with (for
buttons it could be btn), the second parameter is a map of all of the different
colors that this component can be (e.g. ( "primary": red, "secondary": blue) for
generating "btn-primary" and "btn-secondary classes"). The third param is whether
this block has a hover state, if your component has hover states you will need to
assign two colors to your map, the first being the neutral state and the second
being the hover state.

### Bullets
```
ul {
    @include bullets(circle, 2em, pink);
}
```
UNSTABLE

Bullets is a mixin to style bullet points, because CSS does not let us style bullet
points easily. With this mixin you can easily style bullet points, changing their color,
size and shape simply by changing the three parameters in the mixin.

As I have mentioned, this feature is really unstable and the maths behind it is pretty weird.

### Utilities

#### Ghost vertical align
```
.class-name {
    @extend ghost-vertical-align;
    ...
}
```
Used for aligning the unknown to the center of a container.
More info can be [found here](https://css-tricks.com/centering-in-the-unknown/)


#### Psuedos

```
.class-name{
    ...
    @include pseudos() {
        color: red;
        ...
    }
}
```
For applying styles to the hover, focus and active pseudo selectors at the same time.
Styles for these are placed within the curly braces after the parentheses.


#### Selection

```
@include selection() {
    color: red;
    ...
}
```
For manipulating the visual styling of the `:selection` pseudo element.


#### Text hide
```
.class-name {
    @include text-hide();
    ...
}
```
For hiding the text within a container
(good for icons set on backgrounds for screen readers)

#### Hex RGBA

```
.class-name {
    background-color: hex-rgba(#eeeeee, .5);
}
```
This function is for adding alpha to a color that you only have the hex value
for.


### Other

#### Parse font families
```
@include parse-font-families($font-1, $font-2, ...)
```

Takes infinite font families and makes sure they all have at least one fallback.
