# Litecanvas Snippets

Many useful pieces of code to use with [Litecanvas](https://github.com/litecanvas/game-engine).

## Hide mouse cursor

```js
function init() {
  canvas().style.cursor = 'none'
}
```

## The distance between two points

```js
function dist(x1, y1, x2, y2) {
  return Math.hypot(x2 - x1, y2 - y1)
}
```

## The magnitude, or length, of a vector

```js
function mag(x, y) {
  return Math.hypot(x, y);
}
```

## Draw grid lines (useful in tile-based games)

```js
function draw() {
  cls(0)

  drawGridLines()
}

function drawGridLines(cellWidth = 32, cellHeight = 32, color = 3) {
  const cols = floor(W / cellWidth) + 1
  const rows = floor(H / cellHeight) + 1

  for (let i = 1; i < cols; i++) {
    line(i * cellWidth, 0, i * cellWidth, H, color)
  }

  for (let i = 1; i < rows; i++) {
    line(0, i * cellHeight, W, i * cellHeight, color)
  }
}
```

> Note: use `translate()` to draw the grid lines with an offset.

[Live Demo](https://litecanvas.js.org?c=eJx1jj0PgjAURff%2Biju2QiLo5scsgzszgaJNmjYpVQbDf%2FfVIhCMU19vT8%2B7WnlZV%2BZZdfzFgF41%2Fn7AfpexQTDWPkztlTVoXNVzgYCE8eJUc1VGdlywYYXNb7XUugxCnMmYItwLqW53%2Fw2sti7M0Vxb0%2FkQdpS12lrHS2wxaQQS5BPnbD9zxchFfQSJbEnPtfRQROZHOk4fP01JEpcCmspyhc28KEWWYpUUY11Bf4Z%2F7tDp172QxX4pyt9oYR%2Fe4Ch4TQ%3D%3D)
