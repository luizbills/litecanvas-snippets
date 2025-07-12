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
