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
  return Math.sqrt((x2 - x1)**2 + (y2 - y1)**2)
}
```

> See: [Pythagorean theorem](https://en.wikipedia.org/wiki/Pythagorean_theorem)

## The magnitude, or length, of a vector

```js
function mag(x, y) {
  return Math.sqrt(x**2 + y**2)
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

## Simple 2D topdown (4-way) movement

```js
let x, y, speed

litecanvas()

function init() {
  x = W/2
  y = H/2
  speed = 250
}

function update(dt) {
  // use the ARROWS keys to move
  x += speed * dt * (iskeydown('ArrowRight') - iskeydown('ArrowLeft'))
  y += speed * dt * (iskeydown('ArrowDown') - iskeydown('ArrowUp'))
}

function draw() {
  cls(0)
  rectfill(x, y, 32, 32, 4)
}
```

> Note: With this code moving moving diagonally will always be more faster (search for "normalize 2d movement" to fix this). But this might not be a big deal in small games or prototypes.

## Simple Camera

```js
// the camera' snippets function
function camera(x, y) {
  translate(W/2 - x , H/2 - y)
}

// usage example
litecanvas()

let objs = [],
  player = {x: 0, y: 0}

function init() {
  // lets create map objects
  for (let i = 0; i < 20; i++) {
    objs.push({x: rand(-W, W), y: rand(-H, H)})
  }
  player = {x: W/2, y: H/2}
}

function update(dt) {
  // move the player with WASD keys
  player.x += 200 * dt * (iskeydown('D') - iskeydown('A'))
  player.y += 200 * dt * (iskeydown('S') - iskeydown('W'))
}

function draw() {
  cls(0)

  push()
  // make the camera follows the player
  camera(player.x, player.y)

  // draw the map objects (green rects)
  for (const o of objs) {
    rectfill(o.x, o.y, 128, 128, 8)
  }

  // draw the player (red circle)
  circfill(player.x, player.y, 32, 4)
  pop()

  // draw all UI after the pop()
  text(10, 10, `Time: ${round(T,1)}`)
}
```

> Note: for a more complete camera (which zooms, shakes, rotates, etc) use the camera module of https://github.com/litecanvas/utils

## Improve `spr()` performance

The `spr()` function draws a sprite pixel by pixel and this can hurt your game's performance if you decide to draw a lot of sprites this way.

One solution is to use paint to create images of your sprites:

```js
litecanvas({ width: 128 })

// a 3x4 sprite of the letter "A"
let spriteA = `
  .3.
  3.3
  333
  3.3`

// first create the sprite image
let imageA = paint(3, 4, () => spr(0, 0, 3, 4, spriteA))

function draw() {
  cls(0)

  // now draw the sprite with image()
  image(0, 0, imageA)

  // but you can still draw with spr()
  spr(40, 40, 3, 4, spriteA)
}
```
