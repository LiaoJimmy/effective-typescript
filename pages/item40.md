---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Hide unsafe type assertions in well-typed functions

```ts {monaco}
interface MountainPeak {
  name: string;
  elevationMeters: number;
}

declare function fetchJSON(url: string): Promise<unknown>;
	
export async function fetchPeak(peakId: string) {
  return fetchJSON(`/api/mountain-peaks/${peakId}`);
}

const sevenPeaks = [
  'aconcagua', 'denali', 'elbrus', 'everest', 'kilimanjaro', 'vinson', 'wilhelm'
];
async function getPeaksByHeight(): Promise<MountainPeak[]> {
  const peaks = await Promise.all(sevenPeaks.map(fetchPeak));
  return peaks.toSorted(
    (a, b) => b.elevationMeters - a.elevationMeters
  );
}
await getPeaksByHeight();
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

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Assert function return type

```ts {9}
interface MountainPeak {
  name: string;
  elevationMeters: number;
}

declare function fetchJSON(url: string): Promise<unknown>;
	
export async function fetchPeak(peakId: string) {
  return fetchJSON(`/api/mountain-peaks/${peakId}`) as Promise<MountainPeak>;
}

const sevenPeaks = [
  'aconcagua', 'denali', 'elbrus', 'everest', 'kilimanjaro', 'vinson', 'wilhelm'
];
async function getPeaksByHeight(): Promise<MountainPeak[]> {
  const peaks = await Promise.all(sevenPeaks.map(fetchPeak));
  return peaks.toSorted(
    (a, b) => b.elevationMeters - a.elevationMeters
  );
}
await getPeaksByHeight();
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

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Provide a single overload of the function

```ts {8}
interface MountainPeak {
  name: string;
  elevationMeters: number;
}

declare function fetchJSON(url: string): Promise<unknown>;
	
export async function fetchPeak(peakId: string): Promise<MountainPeak>;
export async function fetchPeak(peakId: string) {
  return fetchJSON(`/api/mountain-peaks/${peakId}`);
}

const sevenPeaks = [
  'aconcagua', 'denali', 'elbrus', 'everest', 'kilimanjaro', 'vinson', 'wilhelm'
];
async function getPeaksByHeight(): Promise<MountainPeak[]> {
  const peaks = await Promise.all(sevenPeaks.map(fetchPeak));
  return peaks.toSorted(
    (a, b) => b.elevationMeters - a.elevationMeters
  );
}
await getPeaksByHeight();
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

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Push into use type assertion

```ts {monaco}
function shallowObjectEqual(a: object, b: object): boolean {
  for (const [k, aVal] of Object.entries(a)) {
    if (!(k in b) || aVal !== b[k]) {
      return false;
    }
  }
  return Object.keys(a).length === Object.keys(b).length;
}
shallowObjectEqual({ a: 1 }, { b: 2 });
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

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Hide the any type inside the function

```ts {3}
function shallowObjectEqual(a: object, b: object): boolean {
  for (const [k, aVal] of Object.entries(a)) {
    if (!(k in b) || aVal !== (b as any)[k]) {
      return false;
    }
  }
  return Object.keys(a).length === Object.keys(b).length;
}
shallowObjectEqual({ a: 1 }, { b: 2 });
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

# Item 40

<HachiwareItem2e text="Item 45 (2e)"/>

:: content ::

# Don't expose any type outside the function

```ts {1,9}
function shallowObjectEqualBad(a: object, b: any): boolean {
  for (const [k, aVal] of Object.entries(a)) {
    if (!(k in b) || aVal !== b[k]) {  // ok
      return false;
    }
  }
  return Object.keys(a).length === Object.keys(b).length;
}
shallowObjectEqualBad({ a: 1 }, null);
```

---
transition: fade-out
layout: quote
color: sky-light
quotesize: text-m
authorsize: text-s
author: 'Effective TypeScript'

---

"Make sure you explain why your type assertions are valid, and unit test your code thoroughly."

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