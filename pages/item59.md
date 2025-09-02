---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm
---
:: title ::

# Item 59

<HachiwareItem2e />

:: content ::

# Item 59: Use Never Types to Perform Exhaustiveness Checking

No type is assignable to never (except never itself).

```ts {monaco}
interface Box { type: 'box'; }
interface Circle { type: 'circle'; }
type Shape = Box | Circle;

function drawShape(shape: Shape) {
  switch (shape.type) {
    case 'box':
      shape;
      break;
    case 'circle':
      shape;
      break;
    default:
      shape;
  }
}
drawShape({ type: 'box' });
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

# Item 59

<HachiwareItem2e />

:: content ::

# Error of omission after adding one type

```ts {monaco}
interface Box { type: 'box'; }
interface Circle { type: 'circle'; }
interface Line { type: 'line'; }
type Shape = Box | Circle | Line;

function drawShape(shape: Shape) {
  switch (shape.type) {
    case 'box':
      shape;
      break;
    case 'circle':
      shape;
      break;
    default:
      shape;
  }
}
drawShape({ type: 'box' });
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

# Item 59

<HachiwareItem2e />

:: content ::

# Exhaustiveness Checking

```ts {monaco}
interface Box { type: 'box'; }
interface Circle { type: 'circle'; }
interface Line { type: 'line'; }
type Shape = Box | Circle | Line;

function assertUnreachable(value: never): never {
  throw new Error(`Missed a case! ${value}`);
}

function drawShape(shape: Shape) {
  switch (shape.type) {
    case 'box':
      shape;
      break;
    case 'circle':
      shape;
      break;
    default:
      assertUnreachable(shape);
  }
}
drawShape({ type: 'box' });
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

# Item 59

<HachiwareItem2e />

:: content ::

# Throwing an exception
It protects us from surprise values at runtime, not just during type checking.

```ts {monaco}
function assertUnreachable(value: never): never {
  throw new Error(`Missed a case! ${value}`);
}

declare const NeverShape: never;
assertUnreachable(NeverShape);
```

<v-click>
<br>
<b>Question: Do you use never to perform exhaustiveness checking?</b>
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

# Item 59

<HachiwareItem2e />

:: content ::

# Return never
Since never is assignable to all other types, you can safely return it, regardless of the return type of the function:

```ts {monaco}
interface Box { type: 'box'; }
interface Circle { type: 'circle'; }
interface Line { type: 'line'; }

type Shape = Box | Circle | Line;
const calc = (shape: Shape) => 0;
function assertUnreachable(value: never): never {
  throw new Error(`Missed a case! ${value}`);
}

function getArea(shape: Shape): number {
  switch (shape.type) {
    case 'box':
      return calc(shape);
    case 'circle':
      return calc(shape);
    case 'line':
      return calc(shape);
    default:
      return assertUnreachable(shape);  // ok
  }
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

# Item 59

<HachiwareItem2e />

:: content ::

# Make sure you handle all pairs of two types

Question: Do you find a bug in this shoot function?

```ts {monaco}
type Play = 'rock' | 'paper' | 'scissors';

function shoot(a: Play, b: Play) {
  if (a === b) {
    console.log('draw');
  } else if (
    (a === 'rock' && b === 'scissors') ||
    (a === 'paper' && b === 'rock')
  ) {
    console.log('A wins');
  } else {
    console.log('B wins');
  }
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

# Item 59

<HachiwareItem2e />

:: content ::

# Template literal type and exhaustiveness checking

```ts {monaco}
type Play = 'rock' | 'paper' | 'scissors';
function assertUnreachable(value: never): never { throw new Error(`Missed a case! ${value}`); }

function shoot(a: Play, b: Play) {
  const pair = `${a},${b}` as `${Play},${Play}`;  // or: as const
  switch (pair) {
    case 'rock,rock':
    case 'paper,paper':
    case 'scissors,scissors':
      console.log('draw');
      break;
    case 'rock,scissors':
    case 'paper,rock':
      console.log('A wins');
      break;
    case 'rock,paper':
    case 'paper,scissors':
    case 'scissors,rock':
      console.log('B wins');
      break;
    default:
      assertUnreachable(pair);
  }
}
shoot('rock', 'paper');
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

# Item 59

<HachiwareItem2e />

:: content ::

# switch-exhaustiveness-check

This TypeScript ESLint rule <a href="https://typescript-eslint.io/rules/switch-exhaustiveness-check"  target="_blank">switch-exhaustiveness-check</a> reports when a switch statement over a value typed as a union of literals or as an enum is missing a case for any of those literal types and does not have a default clause.
