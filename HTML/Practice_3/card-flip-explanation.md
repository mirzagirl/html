# How the card flip works

Both cards occupy the same area because they use:

```css
.container .card {
  position: absolute;
  width: 100%;
  height: 100%;
}
```

They overlap like two physical cards placed on top of each other.

## Before hover

```css
.card.back-face {
  transform: rotateY(180deg);
}
```

- The front face has no rotation, so it faces you at `0deg`.
- The back face starts at `180deg`, so it faces away from you.
- `backface-visibility: hidden` hides the reversed side of each card.

```text
front face -> you
back face  -> away
```

## On hover

```css
.container:hover {
  transform: rotateY(180deg);
}
```

The parent container rotates by 180 degrees.

- Front face: `0deg + 180deg = 180deg`, so it turns away and is hidden.
- Back face: `180deg + 180deg = 360deg`, so it faces you and becomes visible.

```text
front face -> away
back face  -> you
```

## Why the flip is smooth

```css
.container {
  transition: transform 0.6s;
}
```

`transition` animates a changed CSS property instead of changing it immediately.

- `transform` is the property that will animate.
- `0.6s` is the animation duration: 0.6 seconds.

Without this rule, hovering changes `rotateY(180deg)` instantly. With it, the card gradually rotates for 0.6 seconds.

```css
transition: transform 0.6s ease;
```

`ease` is optional. It makes the motion start and end gently. It is the default timing function when no value is written.

## 3D rules

```css
section {
  perspective: 1000px;
}

.container {
  transform-style: preserve-3d;
}
```

- `perspective` gives the rotation depth, making it look three-dimensional.
- `preserve-3d` keeps the front and back cards as separate 3D layers while the container rotates.
