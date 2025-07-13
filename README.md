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

## Draw a grid (useful in tile-based games)

```js
function drawGrid(cellWidth = 32, cellHeight = 32, color = 4) {
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

[Live Demo](https://litecanvas.js.org?c=eJx1jr0OgyAUhXee4oxQTart1p%2B5voGzQawkBBKkdWh894JYNZpOHE6%2B%2B92rpBO80u%2Bqox8C9LJ27QXnU0YGRkjz0txJo1HbqqcMAQnxYWVNGRk2xFhzoVQZNLh7T4rwL4R8tu5XGGVsyNHHje5cKDvfNcoYS0scMWsYEuQzZ02%2FcMXERX0EPdl4PVXCQXoyv%2FrnNvp9SpK4FFBSCypxWBalyFJsmmI6l%2FmZ4Z873LR3r2TxvhTlvlrZhy%2FdwnRX)
