---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm
---
:: title ::

# Item 63

<ChiikawaItem2e />

:: content ::

# Item 63: Use Optional Never Properties to Model Exclusive Or

With two inputs, XOR is true if and only if the inputs differ (one is true, one is false).

```ts {monaco}
interface ThingOne {
  shirtColor: string;
}
interface ThingTwo {
  hairColor: string;
}

const bothThings = {
  shirtColor: 'red',
  hairColor: 'blue',
};
const thing1: ThingOne = bothThings;  // ok
const thing2: ThingTwo = bothThings;  // ok
console.log(thing1, thing2);
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

# Item 63

<ChiikawaItem2e />

:: content ::

# Use an optional never type to disallow a property

```ts {monaco}
interface OnlyThingOne {
  shirtColor: string;
  hairColor?: never;
}
interface OnlyThingTwo {
  hairColor: string;
  shirtColor?: never;
}
const bothThings = {
  shirtColor: 'red',
  hairColor: 'blue',
};

const thing1: OnlyThingOne = bothThings;
//    ~~~~~~ Types of property 'hairColor' are incompatible.
const thing2: OnlyThingTwo = bothThings;
//    ~~~~~~ Types of property 'shirtColor' are incompatible.
console.log(thing1, thing2);
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

# Item 63

<ChiikawaItem2e />

:: content ::

# Use an optional never type to model Exclusive Or

```ts {monaco}
interface OnlyThingOne {
  shirtColor: string;
  hairColor?: never;
}
interface OnlyThingTwo {
  hairColor: string;
  shirtColor?: never;
}

type ExclusiveThing = OnlyThingOne | OnlyThingTwo;
const allThings: ExclusiveThing = {
  //  ~~~~~~~~~ Types of property 'hairColor' are incompatible.
  shirtColor: 'red',
  hairColor: 'blue',
};
console.log(allThings);
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

# Item 63

<ChiikawaItem2e />

:: content ::

# Use a tagged union to achieve an exclusive or

```ts {monaco}
interface ThingOneTag {
  type: 'one';
  shirtColor: string;
}
interface ThingTwoTag {
  type: 'two';
  hairColor: string;
}
type Thing = ThingOneTag | ThingTwoTag;
const thing: Thing = {
  type: 'one',
  shirtColor: 'blue',
  hairColor: 'red',
  // Object literal may only specify known properties, but 'hairColor' does not exist in type 'ThingOneTag'. Did you mean to write 'shirtColor'?
}
console.log(thing);
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

# Item 63

<ChiikawaItem2e />

:: content ::

# Define a generic exclusive or (XOR) helper

```ts {monaco}
interface ThingOne {
  shirtColor: string;
}
interface ThingTwo {
  hairColor: string;
}

type XOR<T1, T2> =
    (T1 & {[k in Exclude<keyof T2, keyof T1>]?: never}) |
    (T2 & {[k in Exclude<keyof T1, keyof T2>]?: never});

type ExclusiveThing = XOR<ThingOne, ThingTwo>;
const allThings: ExclusiveThing = {
  //  ~~~~~~~~~ Types of property 'hairColor' are incompatible.
  shirtColor: 'red',
  hairColor: 'blue',
};
console.log(allThings);
```
