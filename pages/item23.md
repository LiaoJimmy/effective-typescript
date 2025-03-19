---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 23

<UsagiItem2e text="Item 21 (2e)"/>

:: content ::

# Create Objects All at Once

```ts {monaco}
const point = {};
point.x = 3;
point.y = 4;
```

<v-click>
<br>
Object spread syntax to build up objects field by field in a type-safe way.
```ts {monaco}
interface Point { x: number, y: number }
const point: Point = {
  x: 3,
  y: 4
};
```
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 23

<UsagiItem2e text="Item 21 (2e)"/>

:: content ::

# Conditionally add a property in a type-safe way

```ts {monaco}
const getPresidentName = (hasMiddle = true) => {
  const firstLast = { first: 'Harry', last: 'Truman' };
  const president = {
    ...firstLast,
    ...(hasMiddle ? { middle: 'S' } : {})
  };
  return president;
}
getPresidentName();
```