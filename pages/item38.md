---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 38

<UsagiItem2e text="Item 43 (2e)"/>

:: content ::

# Use the narrowest possible scope for any Types

```ts {monaco}
type Pizza = {
  slice: () => void;
};
type Salad = {
  vegetables: string[];
};
declare function getPizza(): Pizza;
declare function eatSalad(salad: Salad): void;

function eatDinner() {
  const pizza = getPizza();
  eatSalad(pizza);
  pizza.slice();
}
eatDinner();
```

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 38

<UsagiItem2e text="Item 43 (2e)"/>

:: content ::

# any for entire lifetime

```ts {monaco}
type Pizza = {
  slice: () => void;
};
type Salad = {
  vegetables: string[];
};
declare function getPizza(): Pizza;
declare function eatSalad(salad: Salad): void;

function eatDinner1() {
  const pizza: any = getPizza();  // Don't do this
  eatSalad(pizza);  // ok
  pizza.slice();  // This call is unchecked!
}
eatDinner1();
```

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 38

<UsagiItem2e text="Item 43 (2e)"/>

:: content ::

# any type is scoped to a single expression

```ts {monaco}
type Pizza = {
  slice: () => void;
};
type Salad = {
  vegetables: string[];
};
declare function getPizza(): Pizza;
declare function eatSalad(salad: Salad): void;

function eatDinner2() {
  const pizza = getPizza();
  eatSalad(pizza as any);  // This is preferable
  pizza.slice();  // this is safe
}
eatDinner2();
```

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 38

<UsagiItem2e text="Item 43 (2e)"/>

:: content ::

# @ts-ignore and @ts-expect-error

```ts {monaco}
type Pizza = {
  slice: () => void;
};
type Salad = {
  vegetables: string[];
};
declare function getPizza(): Pizza;
declare function eatSalad(salad: Salad): void;

function eatDinner3() {
  const pizza = getPizza();
  // @ts-ignore
  eatSalad(pizza);
  pizza.slice();
}
eatDinner3();

function eatDinner4() {
  const pizza = getPizza();
  // @ts-expect-error
  eatSalad(pizza);
  pizza.slice();
}
eatDinner4();
```

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 38

<UsagiItem2e text="Item 43 (2e)"/>

:: content ::

# Reduce as any scope

```ts {monaco}
interface Config {
    a: number;
    b: number;
    c: {
        key: Key
    }
}
type Key = { k1: number, k2: number };
type MyKey = { k1: number };

const myKey: MyKey = { k1: 0 };
const config: Config = {
  a: 1,
  b: 2,
  c: {
    key: myKey // Option 1: as any
  }
};  // Option 2: as any
console.log(config);
```