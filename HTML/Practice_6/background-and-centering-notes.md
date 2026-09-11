# Background images and centering text

These notes explain the questions from Practice_6.

## Why was the background image invisible?

The image path was correct, but the empty `.main-container` used `height: 100%` without a defined parent height. Its height therefore collapsed to zero.

A background image does not give an element height. The element needs content or a height/minimum height of its own.

```css
.main-container {
  background-image: url("./image.png");
  min-height: calc(100vh - 50px);
}
```

`100vh` means the full viewport height. Subtracting `50px` leaves space for the header. Using `100vh` for the main area alone makes the header plus main area taller than one screen.

With `position: relative`, setting `top`, `right`, `bottom`, and `left` to zero does not stretch the element to fill its parent.

## What does background-size do?

It controls the size of the background image, not the size of the element.

| Value | Effect |
|---|---|
| `cover` | Fills the area while preserving the image proportions; some parts may be cropped. |
| `contain` | Fits the entire image inside the area while preserving its proportions; empty space may remain. |
| `100% 100%` | Matches the area's width and height, potentially stretching the image. |
| `200px 100px` | Sets an exact image width and height. |

If the image and screen have different proportions, you cannot always fill the screen and show the entire image without cropping or stretching.

## Why was the image repeating?

Background images repeat by default. Your CSS had an image but no size or repeat rule.

```css
.main-container {
  background-image: url("./image.png");
  background-size: cover;
  background-repeat: no-repeat;
  background-position: center;
}
```

- `cover` scales the image to fill the element.
- `no-repeat` prevents extra copies.
- `center` centers the background image within the element.

To cover the page behind the header as well, put the background on `body` instead of `.main-container`. A solid header background will still cover the image underneath it.

## Why did text-align: center not center the text box?

`text-align: center` centers text inside its box. It does not position that box in the middle of its parent.

Your content box used absolute positioning:

```css
.main-container {
  position: relative;
}

.content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
}
```

The parent uses `position: relative` so it becomes the positioning reference for `.content`. The content uses `position: absolute` so it can be placed within that area independently of normal layout.

## What is the difference between top, left, and transform?

`top` and `left` set the positioned box's location. `transform: translate()` visually shifts it from that location.

In this absolute-positioning example:

| Rule | Meaning |
|---|---|
| `top: 50%` | Places the box's top edge halfway down the parent's height. |
| `left: 50%` | Places the box's left edge halfway across the parent's width. |
| `translateX(-50%)` | Shifts left by half the box's own width. |
| `translateY(-50%)` | Shifts up by half the box's own height. |

These descriptions assume no margins on the content box, as in this example.

The percentages refer to different boxes: `top` and `left` use the containing block (your positioned parent); translation percentages normally use the transformed element's own border box.

### Numerical example

Suppose the parent is `1000px` wide and the text box is `400px` wide.

```text
left: 50%         -> left edge starts at 500px
translateX(-50%) -> moves left by 200px
Final left edge  -> 300px
Final right edge -> 700px
Box center       -> 500px
```

The same calculation applies vertically. This is why both rules together center the content box.

## Can transform do anything else?

Yes. Translation is only one type of transform:

```css
transform: translate(20px, 10px); /* Move right and down */
transform: rotate(30deg);        /* Rotate */
transform: scale(1.2);           /* Enlarge */
transform: skewX(10deg);         /* Slant */
```

These are separate examples. If placed in the same rule, the last `transform` declaration wins. To combine effects, use one declaration:

```css
transform: translate(20px, 10px) rotate(30deg);
```

Transforms change the visual appearance without making surrounding elements rearrange to accommodate that change. Unlike `top` and `left`, a transform does not require `position: relative` or `position: absolute` to work on a normal block element.
