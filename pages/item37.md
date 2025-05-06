---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Surprising structural typing

```ts {monaco-run} {autorun:false}  
interface Vector2D {
  x: number;
  y: number;
}
function calculateNorm(p: Vector2D) {
  return Math.sqrt(p.x ** 2 + p.y ** 2);
}

const norm2D = calculateNorm({x: 3, y: 4});
const vec3D = {x: 3, y: 4, z: 1};
const norm3D = calculateNorm(vec3D);
console.log(norm2D, norm3D);
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Prevent other fields using an optional never property

```ts {monaco}
interface Vector2D {
  x: number;
  y: number;
  z?: never; // Optional and other type cannot assign to never
}
function calculateNorm(p: Vector2D) {
  return Math.sqrt(p.x ** 2 + p.y ** 2);
}

const norm2D = calculateNorm({x: 3, y: 4});
const vec3D = {x: 3, y: 4, z: 1};
const norm3D = calculateNorm(vec3D);
console.log(norm2D, norm3D);
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Nominal typing

```ts {1-2|4-5|all}
type Meters = number & {_brand: 'meters'};
type Seconds = number & {_brand: 'seconds'};

const meters = (m: number) => m as Meters;
const seconds = (s: number) => s as Seconds;

const oneKm = meters(1000);
const oneMin = seconds(60);
console.log(oneKm, oneMin);
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Nominal typing with calculating

```ts {monaco}
type Meters = number & {_brand: 'meters'};
type Seconds = number & {_brand: 'seconds'};

const meters = (m: number) => m as Meters;
const seconds = (s: number) => s as Seconds;

const oneKm = meters(1000);
const oneMin = seconds(60);

const tenKm = oneKm * 10;
const v = oneKm / oneMin;
console.log(tenKm, v);
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Nominal typing with unique symbol

```ts {1-2|all}
declare const brand: unique symbol;
type Meters = number & {[brand]: 'meters'};

const meters = (m: number) => m as Meters;
const oneKm = meters(1000);
console.log(oneKm);
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Unique symbol
- It treats symbols as unique literals a special type.
- it’s a subtype of symbol.
- It's only allowed on const declarations and readonly static properties


```ts {monaco}
declare const brand: unique symbol;
// const brand: unique symbol = Symbol('brand');

function processWithBrand(specificBrand: typeof brand) {
   console.log("Processing with the specific brand symbol", specificBrand);
}
processWithBrand(brand);
processWithBrand(Symbol('tag'));
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Binary search

```ts {1-9|11-20|all}
declare const isSortedList: unique symbol;
type SortedList<T> = T[] & {[isSortedList]: 'sorted'};

function isSorted<T>(list: T[]): list is SortedList<T> {
  for (let i = 0; i < list.length - 1; ++i) {
    if (list[i] > list[i + 1]) return false;
  }
  return true;
}

function binarySearch<T>(list: SortedList<T>, x: T): boolean {
  let low = 0, high = list.length - 1;
  while (high >= low) {
    const mid = low + Math.floor((high - low) / 2);
    const v = list[mid];
    if (v === x) return true;
    [low, high] = x > v ? [mid + 1, high] : [low, mid - 1];
  }
  return false;
}

const list = [1,2,3,4,5];
if (isSorted(list)) {
  const find = binarySearch(list, 3);
  console.log(find);
}
```

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

<BinarySearch />

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# More binary search
- lower bound
- upper bound
- Find min/max f(x) 

<Youtube id="v57lNF2mb_s" width="550px" height="300px"/>

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 37

<HachiwareItem2e text="Item 64 (2e)"/>

:: content ::

# Binary search in real world?

<v-click>
  <div class="mt-4">
    <h2>Git bisect</h2> 
    <img src="/images/GitBisect.webp" width="600px"/>
  </div>
</v-click>