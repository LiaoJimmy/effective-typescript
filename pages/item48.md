---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# Use TSDoc for API Comments

```ts {monaco}
/** Generate a greeting. Result is formatted for display. */
function greetJSDoc(name: string, title: string) {
  return `Hello ${title} ${name}`;
}
greetJSDoc('Haichiware', 'っ(^⦁᎑⦁^)੭');
```
<br/>

<v-click>
<h2> // comment is not TSDoc format</h2>
```ts {monaco}
// Generate a greeting. Result is formatted for display.
function greet(name: string, title: string) {
  return `Hello ${title} ${name}`;
}
greet('Haichiware', 'ฅ(^•᎑•^)ฅ');
```
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# TSDoc with type definitions

```ts {monaco}
/** A measurement performed at a time and place. */
interface Measurement {
  /** Where was the measurement made? */
  position: Vector3D;
  /** When was the measurement made? In seconds since epoch. */
  time: number;
  /** Observed momentum */
  momentum: Vector3D;
}
interface Vector3D { x: number; y: number; z: number; }

const measurement: Measurement = {
  position: { x: 1, y: 2, z: 3 },
  time: 1234567890,
  momentum: { x: 0.1, y: 0.2, z: 0.3 },
};
console.log(measurement);
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

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# TSDoc comments are formatted using Markdown

you can use **bold**, *italic*, or 
- bulleted lists

```ts {monaco}
/** A measurement performed at a time and place. */
interface Measurement {
  /** *Where* was the measurement made? */
  position: Vector3D;
  /** When was the measurement made? In **seconds** since epoch. */
  time: number;
  /** Observed momentum */
  momentum: Vector3D;
}
interface Vector3D { x: number; y: number; z: number; }

const measurement: Measurement = {
  position: { x: 1, y: 2, z: 3 },
  time: 1234567890,
  momentum: { x: 0.1, y: 0.2, z: 0.3 },
};
console.log(measurement);
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

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# @template tag to document type parameters for generic types.

```ts {monaco}
/**
 * Construct a new object type using a subset of the properties of another one
 * (same as the built-in `Pick` type).
 * @template T The original object type
 * @template K The keys to pick, typically a union of string literal types.
 */
type MyPick<T extends object, K extends keyof T> = {
  [P in K]: T[P]
};
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

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# Comment best practices


- Try to avoid writing essays in your documentation, though.
- The best comments are short and to the point.
- JSDoc includes some conventions for specifying type information (@param {string} name ...)
  - But you should avoid add type in TypeScript comment.

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 48

<HachiwareItem2e text="Item 68 (2e)"/>

:: content ::

# @deprecated tag

You should mark deprecated symbols using the @deprecated tag.

```ts {monaco}
/** @deprecated use getSecretGift instead */
export function getGift(): void {

}
getGift();
```

More TSDoc tags are available in the [TSDoc documentation](https://tsdoc.org/).