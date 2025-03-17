---
transition: fade-out
layout: section
color: yellow-light
---

# Running TypeScript code with Node.js 22

Since V22.6.0, Node.js has experimental support for some TypeScript syntax via "type stripping". You can write code that's valid TypeScript directly in Node.js without the need to transpile it first.

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

example.ts

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
<b>Question: How about this TS code in Node.js?</b>
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