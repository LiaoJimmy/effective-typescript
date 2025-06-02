---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 50

<ChiikawaItem2e text="Item 45 (2e)"/>

:: content ::

# How would you write a type declaration for this JavaScript function?

```js {monaco}
function double(x) {
  return x + x;
}
console.log(double(12));
```

<v-click>
<br />

## Make the function generic

```ts {monaco}
function double<T extends string | number>(x: T): T {
  return x + x; // Question: why does this not work?
}

const num = double(12);
const str = double('x');
console.log(num, str);
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

# Item 50

<ChiikawaItem2e text="Item 45 (2e)"/>

:: content ::

# Function signatures


```ts {monaco}
function double<T extends string | number>(x: T): T extends string ? string : number;
function double(x: string | number): string | number {
  return typeof x === 'string' ? x + x : x + x;
}

const num = double(12);
const str = double('x');
const numOrStr = double(Math.random() > 0.5 ? num : str);
console.log(num, str, numOrStr);
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

# Item 50

<ChiikawaItem2e text="Item 45 (2e)"/>

:: content ::

# Conditional types distribute over unions

```
(string|number) extends string ? string : number
→ (string extends string ? string : number) |
  (number extends string ? string : number)
→ string | number
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

# Item 50

<ChiikawaItem2e text="Item 45 (2e)"/>

:: content ::

# Distinct overloads separate is more readable

```ts {monaco}
function double(x: number): number;
function double(x: string): string;
function double(x: string | number): string | number;
function double(x: string | number): string | number {
  return typeof x === 'string' ? x + x : x + x;
}

const num = double(12);
const str = double('x');
const numOrStr = double(Math.random() > 0.5 ? num : str);
console.log(num, str, numOrStr);
```
