# CSS Position Property

The CSS `position` property controls how an HTML element is placed on a webpage.

The five main position values are:

```css
position: static;
position: relative;
position: absolute;
position: fixed;
position: sticky;
```

The following offset properties can be used with positioned elements:

```css
top: 10px;
right: 10px;
bottom: 10px;
left: 10px;
```

## 1. Static Position

`position: static` is the default value for HTML elements. The element remains in the normal document flow.

The properties `top`, `right`, `bottom`, and `left` do not move a statically positioned element.

```html
<div class="static-box">Static box</div>
```

```css
.static-box {
  position: static;
  top: 20px; /* No effect */
  background: lightgray;
}
```

Use `static` when the element does not need any special positioning.

## 2. Relative Position

`position: relative` keeps the element in the normal document flow, but lets you move it relative to its original position.

The element's original space remains reserved.

```html
<div class="relative-box">Relative box</div>
```

```css
.relative-box {
  position: relative;
  top: 20px;
  left: 30px;
  background: lightblue;
}
```

This moves the element 20 pixels down and 30 pixels to the right.

`position: relative` is also commonly placed on a parent so that an absolutely positioned child uses that parent as its reference.

## 3. Absolute Position

`position: absolute` removes the element from the normal document flow.

The element is positioned relative to its nearest ancestor whose `position` is `relative`, `absolute`, `fixed`, or `sticky`.

```html
<div class="card">
  Product
  <span class="badge">New</span>
</div>
```

```css
.card {
  position: relative;
  width: 250px;
  height: 150px;
  border: 1px solid black;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 4px 8px;
  background: red;
  color: white;
}
```

The badge appears 10 pixels from the top-right corner of the card.

If there is no positioned ancestor, the element is positioned relative to the page's initial containing block.

## 4. Fixed Position

`position: fixed` removes the element from the normal document flow and positions it relative to the browser viewport.

It remains in the same place when the user scrolls.

```html
<button class="help-button">Help</button>
```

```css
.help-button {
  position: fixed;
  right: 20px;
  bottom: 20px;
  padding: 10px 16px;
  background: navy;
  color: white;
}
```

Fixed positioning is commonly used for:

- Chat buttons
- Back-to-top buttons
- Fixed navigation bars
- Cookie notices

## 5. Sticky Position

`position: sticky` behaves like a normal element until the page reaches a specified scrolling point. It then sticks at that position.

```html
<header class="navbar">Navigation</header>
```

```css
.navbar {
  position: sticky;
  top: 0;
  padding: 15px;
  background: white;
  z-index: 10;
}
```

The navigation bar scrolls normally at first and then stays at the top of its scrolling container.

A sticky element normally needs at least one offset, such as:

```css
top: 0;
```

Its behavior can be affected by the height and `overflow` properties of its parent elements.

## Example 1: Notification Badge

```html
<div class="notification">
  🔔
  <span class="count">3</span>
</div>
```

```css
.notification {
  position: relative;
  display: inline-block;
  font-size: 40px;
}

.count {
  position: absolute;
  top: -5px;
  right: -10px;
  padding: 2px 7px;
  border-radius: 50%;
  background: red;
  color: white;
  font-size: 14px;
}
```

The parent uses `relative`, and the badge uses `absolute`. Therefore, the badge is positioned relative to the notification element.

## Example 2: Fixed Back-to-Top Button

```html
<a href="#top" class="back-to-top">↑ Top</a>
```

```css
.back-to-top {
  position: fixed;
  right: 20px;
  bottom: 20px;
  padding: 10px;
  background: navy;
  color: white;
  text-decoration: none;
}
```

The button stays in the bottom-right corner while the page scrolls.

## Example 3: Sticky Table Header

```html
<div class="table-container">
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Score</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>Aisha</td><td>90</td></tr>
      <tr><td>Rahul</td><td>85</td></tr>
      <tr><td>Sara</td><td>92</td></tr>
    </tbody>
  </table>
</div>
```

```css
.table-container {
  height: 200px;
  overflow-y: auto;
}

th {
  position: sticky;
  top: 0;
  background: white;
}
```

The table header stays visible while the table rows scroll.

## Position Comparison

| Value | Keeps original space? | Positioned relative to | Scroll behavior |
|---|---:|---|---|
| `static` | Yes | Normal document flow | Scrolls normally |
| `relative` | Yes | Its original position | Scrolls normally |
| `absolute` | No | Nearest positioned ancestor | Scrolls with its container |
| `fixed` | No | Browser viewport | Stays in the same viewport position |
| `sticky` | Yes | Its scrolling container | Sticks after reaching an offset |

## The `z-index` Property

When elements overlap, `z-index` helps control which element appears in front.

```css
.box-one {
  position: absolute;
  z-index: 1;
}

.box-two {
  position: absolute;
  z-index: 2;
}
```

In this example, `.box-two` normally appears in front because it has the larger `z-index`.

`z-index` works within stacking contexts, so a large number does not always place an element above every element on the page.

## Common Mistakes

### Forgetting to position the parent

```css
.parent {
  position: relative;
}

.child {
  position: absolute;
  top: 0;
  right: 0;
}
```

Without a positioned parent, the absolute child may be placed relative to a larger container or the page.

### Using offsets with `static`

```css
.box {
  position: static;
  top: 20px; /* Does not move the box */
}
```

Use `relative`, `absolute`, `fixed`, or `sticky` when you need offsets.

### Forgetting an offset for `sticky`

```css
.navbar {
  position: sticky;
  top: 0;
}
```

Without `top`, `bottom`, `left`, or `right`, the browser has no sticking point.

## Easy Way to Remember

```text
static   = normal position
relative = moved from its original position
absolute = positioned inside a positioned ancestor
fixed    = fixed to the browser viewport
sticky   = scrolls first, then sticks
```
