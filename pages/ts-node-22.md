---
transition: fade-out
layout: section
color: yellow-light
---


<div class="text-center">
  <h1> Running TypeScript code with Node.js 22</h1>
  <p>Since V22.6.0, Node.js has experimental support</p>
  <p>for some TypeScript syntax via "type stripping".</p>
  <div class="flex items-center justify-center mt-8">
    <img src="/images/Yaha.png" width="150px" />
  </div>
  <style>
    .section.slidecolor {
      background-color: white;
    }
  </style>
</div>

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Running TypeScript code with Node.js 22

:: content ::

# experimental-strip-types flag
From v23 onwards, the --experimental-strip-types flag is enabled by default

```ts {monaco}
function test(): string {
  return 'hello';
}

console.log(test());
```

```bash {monaco}
node --experimental-strip-types example.ts
```

<v-click>
<br />
<b>Question: Can we run this TypeScript code in Node.js?</b>
```ts {monaco}
function test(): number {
  return 'hello';
}

console.log(test());
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

# Running TypeScript code with Node.js 22

:: content ::

# Strip types, not check types  

````md magic-move
```ts
function test(): number {
  return 'hello';
}

console.log(test());
```
```ts
"use strict";
function test() {
    return 'hello';
}
console.log(test());
```
````

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Running TypeScript code with Node.js 22

:: content ::

# experimental-transform-types flag
In v22.7.0 this experimental support was extended to transform TypeScript-only syntax, like enums and namespace, with the addition of the --experimental-transform-types flag.

enum-example.ts

```ts {monaco-run} {autorun:false}
enum MyEnum {
  A,
  B,
}
console.log(MyEnum.A);
```

```bash {monaco}
node --experimental-transform-types enum-example.ts
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

# Running TypeScript code with Node.js 22

:: content ::

# Transform TypeScript-only syntax
````md magic-move
```ts
enum MyEnum {
  A,
  B,
}


console.log(MyEnum.A);
```
```ts
"use strict";
var MyEnum;
(function (MyEnum) {
    MyEnum[MyEnum["A"] = 0] = "A";
    MyEnum[MyEnum["B"] = 1] = "B";
})(MyEnum || (MyEnum = {}));
console.log(MyEnum.A);
```
````