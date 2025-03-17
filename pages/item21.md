---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 21

<ChiikawaItem2e text="Item 20 in 2e" />

:: content ::

<v-click>
<h1> Understand How a Variable Gets Its Type </h1>

```ts {monaco}
interface Vector3 {
  x: number;
  y: number;
  z: number;
}
function getVector(vector: Vector3, axis: 'x' | 'y' | 'z') {
  return vector[axis];
}

let x = 'x';
let vector = {x: 10, y: 20, z: 30};
getVector(vector, x);

```
</v-click>

<v-click>
<br>
If you declare a variable with const instead of let, it gets a narrowest type.
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 21

<ChiikawaItem2e text="Item 20 in 2e" />

:: content ::

# as const
When you write as const after a value, TypeScript will infer the narrowest possible type for it.

```ts {monaco}
const obj1 = { x: 1, y: 2 };

const obj2 = { x: 1 as const, y: 2 };

const obj3 = { x: 1, y: 2 } as const;

```

<v-click>
<br>
<b>Question: Nested as const</b>
```ts {monaco}
const obj4 = { x: 1, y: 2, nested: { z: 3 } } as const;
```
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 21

<ChiikawaItem2e text="Item 20 in 2e" />

:: content ::

# Object.freeze()
Object.freeze has introduced some readonly modifiers into the inferred types

```ts {monaco}
const frozenArray = Object.freeze([1, 2, 3]);

const frozenObj = Object.freeze({ x: 1, y: 2 });

```

<v-click>
<br>
<b>Question: Nested Object.freeze()</b>
```ts {monaco}
const forzeonNestedObj = Object.freeze({ x: 1, y: 2, nested: { z: 3 }});
forzeonNestedObj.nested.z;
```
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 21

<ChiikawaItem2e text="Item 20 in 2e" />

:: content ::

# satisfies
Satisfies operator ensures that a value, well, satisfies the requirements of a type and guides inference by preventing TypeScript from inferring a wider type.

```ts {monaco}
type Point = [number, number];

const capitalsBad = {
    ny: [-73.7562, 42.6526,],
    ca: [-121.4944, 38.5816],
} satisfies Record<string, Point>;

capitalsBad.ny;
```

---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 21

<ChiikawaItem2e text="Item 20 in 2e" />

:: content ::

# Satisfies operator in Storybook
Better in-editor type checking for <a href="https://storybook.js.org/blog/improved-type-safety-in-storybook-7/" target="_blank">Component Story Format 3</a>


```ts {monaco}
import type { Meta } from '@storybook/react';

const meta = {
  title: 'Components/Toast',
  tags: ['autodocs'],
} satisfies Meta;
```
