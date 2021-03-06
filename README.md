# cs294-notes

# Future of CSS (Tab Atkins)

### Images

`image-set("something.jpg", 1x, "highres.png", 2x, "pring.png", 200dpi)`

Fade between two images: `coss-fade(<percentage>? <image> [, <image> | <color>])`

Allows browsers to do pixel art scaling in different ways `image-rendering(auto | pixelated | crip-edges)`


### Flexbox
Makes CSS actually handle layouts!

Layout direction: `flex-flow` will do layout direction! Woaaaahhh.

`order`: source order independence - let the currently clicked one go first

`justify-*`, `align-*`: actual alignment

`flex`: make elements grow

```css
grid-template: "a c"
               "c d";
grid-area: a;
```

Hella crazy for mobile!!

`something:nth(child of .foo)`

`table.foo :matches(td, th) p.bar`

### Variables!!
```css
:root {
--header-color: #006;
}
a {color: var(--main-color)}
```

### Colors!!

`#0f08`: `#rgba`

`hwb()`: hue-whiteness-blackness

`gray()`

`color()`: like `lighten, darken`

### Media Queries
Pointer: `course` or `fine`
Hover: `no` or `yes`

### Transforms
Motion path!

### Houdini task force
Works on making CSS extensible

`@custom-media foo (some media stuff)`
`@media ("foo") {}`

```javascript
CSS.customMedia.set("foo", true);
```
Also: custom pseudo classes, layouts, paints (!!)
