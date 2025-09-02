---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 71

<UsagiItem2e />

:: content ::

# Item 71: Use Module Augmentation to Improve Types

<b>JSON.parse() return type</b>
```ts {monaco}
declare let apiResponse: string;
const response = JSON.parse(apiResponse);
const cacheExpirationTime = response.lastModified + 3600;
//    ^? const cacheExpirationTime: any
console.log(cacheExpirationTime);
```

<v-click>
<br />
The <i>unknown</i> type was only introduced in TypeScript 3.0, which came out in July of 2018. Enormous amounts of TypeScript code had been written before then, and changing the return type of JSON.parse would have been extremely disruptive.
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

# Item 71

<UsagiItem2e />

:: content ::

<b>JSON.parse() return type</b>
```ts {1-9|1-19|21-25}
// lib.es5.d.ts
interface JSON {
  parse(
    text: string,
    reviver?: (this: any, key: string, value: any) => any
  ): any;
  // ...
}
declare var JSON: JSON;

// declarations/safe-json.d.ts
namespace declarations {
  interface JSON {
    parse(
      text: string,
      reviver?: (this: any, key: string, value: any) => any
    ): unknown;
  }
}

declare let apiResponse: string;
const response = JSON.parse(apiResponse);
//    ^? const response: unknown
const cacheExpirationTime = response.lastModified + 3600;
//                          ~~~~~~~~ response is of type 'unknown'.
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

# Item 71

<UsagiItem2e />

:: content ::

# Type unknown requires a type assertion
<br />
```ts {all|4}
interface ApiResponse {
  lastModified: number;
}
const response = JSON.parse(apiResponse) as ApiResponse;
const cacheExpirationTime = response.lastModified + 3600;  // ok
//    ^? const cacheExpirationTime: number
```

<br />
<v-click>
<b>Practice: Change fetch API’s Response.prototype.json() return unknown</b>
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

# Item 71

<UsagiItem2e />

:: content ::

# Disallow certain usage by “Declaration Merging”

<br />

```ts {monaco-run} {autorun:false}
const abc = new Set('abc');
console.log(abc);
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

# Item 71

<UsagiItem2e />

:: content ::

# “knock out” methods and mark them @deprecated

<br />

```ts {1-5|all}
// declarations/ban-set-string-constructor.d.ts:
interface SetConstructor {
  /** @deprecated */
  new (str: string): 'Error! new Set(string) is banned.';
}

const s = new Set('abc');
//    ^? const s: "Error! new Set(string) is banned."
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

# Item 71

<UsagiItem2e />

:: content ::

# Improve the built-in types in the ts-reset npm package

<a href="https://www.totaltypescript.com/ts-reset" target="_blank"> ts-reset </a>
: Improve TypeScript's Built-In typings

<br />
<v-click>
```sh
npm i -D @total-typescript/ts-reset;

echo 'import "@total-typescript/ts-reset";' > reset.d.ts;
# Do not add any other lines of code to this file!
```
</v-click>