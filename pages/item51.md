---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# Mirror Types to Sever Dependencies


```ts
// parse-csv.ts
import { Buffer } from 'node:buffer';

function parseCSV(contents: string | Buffer): {[column: string]: string}[] {
  if (typeof contents === 'object') {
    // It's a buffer
    return parseCSV(contents.toString('utf8'));
  }
  return [];
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

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# Generate type declarations by
# `--declaration`
<br />

```ts
// parse-csv.d.ts
import { Buffer } from 'node:buffer';
export declare function parseCSV(contents: string | Buffer): {
    [column: string]: string;
}[];
```
<br />

<v-click>
<h2>TypeScript developer:</h2>
Cannot find module 'node:buffer' or its corresponding type declarations.
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

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# Make @types/node a dependency?

- JavaScript developers will wonder what these @types modules are that they’re depending on.

<v-clicks>

- TypeScript web developers will wonder why they’re depending on Node.js.
- TypeScript developers using a different version of Node.js will wonder why they have duplicated type definitions.

</v-clicks>

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# TypeScript’s structural typing

```ts {2-4|2-4,7|all}
import { Buffer } from 'node:buffer';
export interface CsvBuffer {
  toString(encoding?: string): string;
}

export function parseCSV(
  contents: string | CsvBuffer
): {[column: string]: string}[]  {
  // ...
}

const buffer = new Buffer("column1,column2\nval1,val2", "utf-8");
parseCSV(buffer);  // OK
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

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# Write a unit test to verify

```ts {1,2,4-13|1,2,14-23}
import { Buffer } from 'node:buffer';
import { parseCSV } from './parse-csv';

test('parse CSV in a buffer', () => {
  const nodeJSBuffer = new Buffer("column1,column2\nval1,val2", "utf-8")

  const csv = parseCSV(nodeJSBuffer);

  expect(csv).toEqual(
    [{column1: 'val1', column2: 'val2'}]
  );
});

test('parse CSV in a string', () => {
  const string = "column1,column2\nval1,val2";

  const csv = parseCSV(string);

  expect(csv).toEqual(
    [{column1: 'val1', column2: 'val2'}]
  );
});
```

---
transition: fade-out
layout: quote
color: sky-light
quotesize: text-m
authorsize: text-s
author: Go Proverbs

---

"A little copying is better than a little dependency."

<div class="flex justify-center mt-8">
  <img src="/images/ChikawaDraw.png" width="300px" />
  <style>
    .quote_author {
      font-size: 32px;
      font-weight: bold;
    }
    .slidev-layout.quote {
      padding-left: 3.5rem;
    }
  </style>
</div>

---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 51

<HachiwareItem2e text="Item 70 (2e)"/>

:: content ::

# Go Proverbs

https://go-proverbs.github.io/

<br />

<v-click>

<h1>Zen of Python</h1>

```bash
python3
import this
``` 

<br />
<a href="https://upload.wikimedia.org/wikipedia/commons/d/dc/The_Zen_of_Python_illustrated.png" target="_blank">
The Zen of Python Illustrated
</a>

</v-click>
