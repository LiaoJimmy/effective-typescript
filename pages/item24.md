---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 24

<ChiikawaItem2e text="Item 23 (2e)" />

:: content ::

# Aliasing can prevent TypeScript from narrowing types.

```ts {monaco}
interface Coordinate {
  x: number;
  y: number;
}

interface BoundingBox {
  x: [number, number];
  y: [number, number];
}

interface Polygon {
  boundingBox?: BoundingBox;
}

function isPointInPolygon(polygon: Polygon, pt: Coordinate) {
  const box = polygon.boundingBox;
  if (polygon.boundingBox) {
    if (pt.x < box.x[0] || pt.x > box.x[1] ||
        pt.y < box.y[0] || pt.y > box.y[1]) {
      return false;
    }
  }
}
isPointInPolygon({boundingBox: { x: [0, 10], y: [0, 10] }}, { x: 5, y: 5 });
```