---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 36

<ChiikawaItem2e text="Item 41 (2e)" />

:: content ::

# There are a few naming issues here

```ts {monaco}
interface Animal {
  name: string;
  endangered: boolean;
  habitat: string;
}

const leopard: Animal = {
  name: 'Snow Leopard',
  endangered: false,
  habitat: 'tundra',
};
console.log(leopard);
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

# Item 36

<ChiikawaItem2e text="Item 41 (2e)" />

:: content ::

# Type declaration and value with less ambiguity

```ts {monaco}
interface Animal {
  commonName: string;
  genus: string;
  species: string;
  status: ConservationStatus;
  climates: KoppenClimate[];
}
type ConservationStatus = 'EX' | 'EW' | 'CR' | 'EN' | 'VU' | 'NT' | 'LC';
type KoppenClimate = |
  'Af' | 'Am' | 'As' | 'Aw' |
  'BSh' | 'BSk' | 'BWh' | 'BWk' |
  'Cfa' | 'Cfb' | 'Cfc' | 'Csa' | 'Csb' | 'Csc' | 'Cwa' | 'Cwb' | 'Cwc' |
  'Dfa' | 'Dfb' | 'Dfc' | 'Dfd' |
  'Dsa' | 'Dsb' | 'Dsc' | 'Dwa' | 'Dwb' | 'Dwc' | 'Dwd' |
  'EF' | 'ET';
const snowLeopard: Animal = {
  commonName: 'Snow Leopard',
  genus: 'Panthera',
  species: 'Uncia',
  status: 'VU',  // vulnerable
  climates: ['ET', 'EF', 'Dfd'],  // alpine or subalpine
};
console.log(snowLeopard);
```

---
transition: fade-out
layout: quote
color: pink-light
quotesize: text-m
authorsize: text-s
author: '​Phil Karlton'

---

"There are only two hard problems in Computer Science: cache invalidation and naming things."

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
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 36

<ChiikawaItem2e text="Item 41 (2e)" />

:: content ::

<img src="/images/CleanCodeName.png" />

<p>Names are everywhere in software. We name our variables, our functions, our arguments, classes, and packages. We name our source files and the directories that contain them.
</p>
<p>Because we do so much of it, we’d better do it well.</p>