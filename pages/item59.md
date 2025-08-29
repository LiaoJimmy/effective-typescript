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

The never type is assignable to every type;   
However, no type is assignable to never (except never itself).

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

# Error of omission after adding one case

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

# No value is assignable to the never type

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
```

<v-click>
<br>
<b>Question: Do you use never to perform exhaustiveness checking?</b>
</v-click>