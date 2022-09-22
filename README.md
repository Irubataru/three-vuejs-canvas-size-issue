# three-pixel-issue

Minimal repro to debug an issue I have where the `<div>` owning the `<canvas>`
element used by three.js is 2 px taller than the canvas, resulting in an
unwanted scroll bar.

## Resolution

The issue was caused by the `<canvas>` element being an inline element which
added the unwanted pixels. This was solved by chaning its style to be block

```css
canvas {
  display: block;
}
```
