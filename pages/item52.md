---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Write Tests for Your Types

Write tests until fear is transformed into boredom. ​—​Phlip (quoted in Kent Beck, Test Driven Development: By Example)

<v-click>

## Why do we need test in TypeScript
- TypeScript lets you put an enormous amount of logic in the types. Where there’s logic, there might be bugs
- For JavaScript libraries and, to some extent, TypeScript code, you can define your types independently of the runtime implementation. This means that the two can get out of sync,

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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Assign the result to a variable with a declared type

```ts {monaco}
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];

const lengths: number[] = map(['john', 'paul'], name => name.length);
```
<br />

<v-click>
Named variable that is likely to be unused. This adds boilerplate, and also means that you’ll have to disable any linter rules that warn about unused variables.
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Define a helper to assert

```ts {monaco}
function assertType<T>(x: T) { }

assertType<number[]>(map(['john', 'paul'], name => name.length));
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Checking assignability rather than equality

Object

```ts {monaco}
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];
function assertType<T>(x: T) { }

const beatles = ['john', 'paul', 'george', 'ringo'];
assertType<{name: string}[]>(
  map(beatles, name => ({
    name,
    inYellowSubmarine: name === 'ringo'
  }))
);  // OK!?
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Checking assignability rather than equality

Function

```ts {monaco}
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];
function assertType<T>(x: T) { }

const double = (x: number) => 2 * x;
assertType<(a: number, b: number) => number>(double);  // OK!?
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# `Parameters<F>` and `ReturnType<F>`

```ts {4-6|8-9}
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];
function assertType<T>(x: T) { }

const double = (x: number) => 2 * x;
declare let p: Parameters<typeof double>;
assertType<[number, number]>(p);

declare let r: ReturnType<typeof double>;
assertType<number>(r);  // OK
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# expect-type

You can use it on its own or via the vitest testing framework, which bundles it.

<a href="https://vitest.dev/api/expect-typeof.html" target="_blank">Vitest expect-typeof</a>

```ts {monaco}
import { expectTypeOf } from 'expect-type';
declare function map<U, V>(array: U[], fn: (u: U) => V): V[];

const beatles = ['john', 'paul', 'george', 'ringo'];
expectTypeOf(map(
  beatles,
  function(name, i, array) {
    expectTypeOf(name).toEqualTypeOf<string>();
    expectTypeOf(i).toEqualTypeOf<number>();
    expectTypeOf(array).toEqualTypeOf<string[]>();
    expectTypeOf(this).toEqualTypeOf<string[]>();
    return name.length;
  }
)).toEqualTypeOf<number[]>();
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Equals<X, Y> in Type Challenges repo

<a href="https://github.com/type-challenges/type-challenges" target="_blank">Type Challenges</a>

```ts {monaco}
export type Equals<X, Y> =
  (<T>() => T extends X ? 1 : 2) extends
  (<T>() => T extends Y ? 1 : 2) ? true : false;

export type Expect<T extends true> = T;

const double = (x: number) => 2 * x;
type Test1 = Expect<Equals<typeof double, (x: number) => number>>;
type Test2 = Expect<Equals<typeof double, (x: string) => number>>;
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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# dtslint

make sure a package is correct for DT

<a href="https://github.com/microsoft/DefinitelyTyped-tools" target="_blank">DefinitelyTyped-tools</a>

```ts {monaco}
declare function map<U, V>
  (array: U[],
  fn: (this: U[], u: U, i: number, array: U[]) => V)
: V[];

const beatles = ['john', 'paul', 'george', 'ringo'];
map(beatles, function(
  name,  // $ExpectType string
  i,     // $ExpectType number
  array  // $ExpectType string[]
) {
  this;   // $ExpectType string[]
  console.log(this, i, array);
  return name.length;
});  // $ExpectType number[]
```

<v-click>

eslint-plugin-expect-type works in a similar way, but as an ESLint plugin.

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

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Tool can’t help you check autocomplete

```ts {monaco}
type Game = 'wordle' | 'crossword' | (string & {});
const spellingBee: Game = 'spelling bee';
let game: Game = '';
console.log(game);
```

[Playground Link](https://www.typescriptlang.org/play/?#code/C4TwDgpgBA4ghgW2gXigcgO4HsBOATAGwjSgB90BjHLAZxu3xPIAobgcBLAOwHMoAyKAG8AvgEoA3ACgKWLmyg1IBAtx4AhCBABcsRCnRKIKtVABGWtNKLAoPfbvhIoqNFZlyaWIgDoCWHmZ7JEkgA)

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 52

<UsagiItem2e text="Item 55 (2e)"/>

:: content ::

# Don’t roll your own type testing system

- dtslint: DefinitelyTyped standard tool in that setting
- vitest, expect-type, or tsd: testing your own type
- eslint-plugin-expect-type: sensitive type tests, not just its structure
