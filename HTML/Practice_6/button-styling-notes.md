# Transparent button backgrounds

## Why does my button have an opaque background?

This rule gives the button a solid gray background:

```css
background-color: #7e7e7e;
```

The background image behind the button cannot show through a solid color.

## How can Get Started look like the outlined Learn More button?

With the current HTML, Get Started is the first button inside its parent:

```html
<div>
  <button class="btn">Get Started</button>
  <button class="btn">Our Services</button>
</div>
```

Add this after your shared button styles:

```css
.btn:first-child {
  background: transparent;
  color: white;
  border: 2px solid white;
  border-radius: 5px;
  backdrop-filter: none;
  padding: 12px 24px;
}
```

- `background: transparent` lets the image behind the button show through.
- `color: white` sets the text color.
- `border` creates the white outline.
- `border-radius` rounds the corners.
- `backdrop-filter: none` removes the background blur.
- `padding` adds space between the text and border: 12px vertically and 24px horizontally.

`.btn:first-child` selects an element with class `btn` only when it is the first element child of its parent. It does not mean the first element with that class anywhere on the page.

## Why not use opacity?

```css
opacity: 0.5;
```

This fades the entire button, including its text and border. Use a transparent background when you want the text and border to remain fully visible.

For a slightly tinted background instead of full transparency, use a color with an alpha value:

```css
background: rgba(0, 0, 0, 0.2);
```

This makes only the background color 20% opaque.

## Is backdrop-filter necessary?

No. `backdrop-filter: blur(5px)` blurs the scene behind the button; it does not make a solid background transparent. For the clear outlined look, use `background: transparent` and remove the blur.
