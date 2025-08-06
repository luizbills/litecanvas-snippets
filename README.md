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

> **Note**: use `translate()` to draw the grid lines with an offset.

[Live Demo](https://litecanvas.js.org?c=eJx1kD0PwiAURXd%2BxR3BNrHq5sdsB%2FfODaWWhEACaAfT%2F%2B7DVmtsnHhcTs67weioZG3vdeAPBvS6id0eu23BBsFYe7MyamfR%2BLrnAgmRJvBC0JCys9fNRVsVuGDDDz%2B%2FSWVMlcw4kTpHupdKX7v4DpxxPs3TCmdDTGGgrDXOeV5hjY9GIMPmw3nXz1w5caN%2BBIlsSc%2BNitBEbg50HF9%2BmrJsXAoYKss1VvOiHEWOn6Sc6qYvGP65U6el%2B0s29stRLaMv%2B%2FAEUXd6Wg%3D%3D)

## Quick way to make time based events

For time-based events, I recommend using the [Timers plugin](https://github.com/litecanvas/plugin-timers). But for quick tests, you can use one of these two techniques.

```js
// you need declare a variable for each event
let nextTime = 0

function update(dt) {
  if (T >= nextTime) {
    nextTime = T + 5
    // do something every 5 seconds
  }
}
```

```js
// without variables, but not accurate
function update(dt) {
  if (T % 5 < dt) {
    // do something every 5 seconds
  }
}
```

## Enable MX/MY (mouse cursor coordinates) in mobile

By default, `MX` and `MY` is `-1` until the mouse moves (something that doesn't usually happen on mobile devices).

```js
litecanvas()

function draw() {
  cls(0)
  circfill(MX, MY, 8, 4)
}

function tapped (x, y, touchId) {
  if (touchId > 0) {
    updateMouse(x, y)
  }
}

function tapping (x, y, touchId) {
  if (touchId > 0) {
    updateMouse(x, y)
  }
}

function updateMouse(x, y) {
  def('MX', x)
  def('MY', y)
}
```
