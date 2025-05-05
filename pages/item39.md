---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 39

<ChiikawaItem2e text="Item 44 (2e)" />

:: content ::

# Prefer more precise variants of any to plain any

```ts {monaco}
function getLengthBad(array: any) {  // Don't do this!
  return array.length;
}
function getLength(array: any[]) {  // This is better
  return array.length;
}

getLengthBad(/123/);  // No error, returns undefined
getLength(/123/); // Argument of type 'RegExp' is not assignable to parameter of type 'any[]'.

getLengthBad(null);  // No error, throws at runtime
getLength(null); // Argument of type 'null' is not assignable to parameter of type 'any[]'.
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

# Item 39

<ChiikawaItem2e text="Item 44 (2e)" />

:: content ::

# Use unknown instead of any

```ts {monaco}
declare function getAny(): any;
declare function getUnknown(): unknown;

const anyValue = getAny();
const unknownValue = getUnknown();
anyValue(); // ok
unknownValue(); // error, not callable
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

# Item 39

<ChiikawaItem2e text="Item 44 (2e)" />

:: content ::

# Avoid using any if you expect a function type.

```ts {1-5|7-8}
type FnAny = any;  // any for what?
type Fn0 = () => any;  // any function callable with no params
type Fn1 = (arg: any) => any;  // With one param
type FnN = (...args: any[]) => any;  // With any number of params
                                     // same as "Function" type
                                     
type numArgsBad = (...args: any) => number;
type numArgsGood = (...args: any[]) => number; // This is better
```