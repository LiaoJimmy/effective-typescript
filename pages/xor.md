---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm
---
:: title ::

# XOR

<HachiwareItem2e />

:: content ::

# Xor Properties
<br />
```{1-2|4-5|7-8|10-11|13-14|16-17}
1 ^ 1 = 0
0 ^ 1 = 1

Commutative Law（交換律）:
p ^ q = q ^ p

Associative Law（結合律）:
p ^ (q ^ r) = (p ^ q) ^ r

Identity Law（恆等律）:
p ^ 0 = p

Zero Law（歸零律）:
p ^ p = 0

Involution（對合運算）:
p ^ q ^ q = p ^ 0 = p
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

# XOR

<HachiwareItem2e />

:: content ::

# Toggle a bit
<br />
```ts
// 1 ^ 1 = 0
// 0 ^ 1 = 1

const num = 6; // (110)2
num ^ (1 << 0); // (111)2 = 7
num ^ (1 << 1); // (100)2 = 4
num ^ (1 << 2); // (010)2 = 2
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

# XOR

<HachiwareItem2e />

:: content ::

# Toggle a bit
<br />
```ts
// 1 ^ 1 = 0
// 0 ^ 1 = 1

const num = 6; // (110)2
num ^ (1 << 0); // (111)2 = 7
num ^ (1 << 1); // (100)2 = 4
num ^ (1 << 2); // (010)2 = 2
```

<v-click>
<br />
<h2> Practice </h2>
<ul>
    <li>
        <a href="https://leetcode.com/problems/reverse-bits/" target="_blank">
            190. Reverse Bits (Easy)
        </a>
    </li>
    <li>
        <a href="https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array" target="_blank">
            421. Maximum XOR of Two Numbers in an Array (Medium)
        </a>
    </li>
    <li>
        <a href="https://leetcode.com/problems/xor-queries-of-a-subarray" target="_blank">
            1310. XOR Queries of a Subarray (Medium)
        </a>
    </li>
</ul>
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

# XOR

<HachiwareItem2e />

:: content ::

# JavaScript Bitwise Limitation

Numbers with more than 32 bits get their most significant bits discarded.   

For example, the following integer with more than 32 bits will be converted to a 32-bit integer:

```
Before: 1110 0110 1111 1010 0000 0000 0000 0110 0000 0000 0001
// 15_872_588_537_857

After:                 1010 0000 0000 0000 0110 0000 0000 0001
// 2_684_379_137

1 << 31; // (10000000000000000000000000000000)2 = 2 ** 31
-2147483648

1 << 30  // (1000000000000000000000000000000)2 = 2 ** 30
1073741824
```

<v-click>
<br />
<h2> Question: What's about 1 << 32? </h2>
</v-click>

<v-click>
1 << 32 will be treated as 1 << 0, which is 1.
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

<HachiwareItem2e />

:: content ::
# Bitwise in real world
Bitwise is often used in performance-critical code to store multiple boolean flags in a single integer.

<b>React.js</b>
```ts
// react-dom-bindings/src/events/EventSystemFlags.js
export const IS_EVENT_HANDLE_NON_MANAGED_NODE = 1;
export const IS_NON_DELEGATED = 1 << 1;
export const IS_CAPTURE_PHASE = 1 << 2;
export const IS_PASSIVE = 1 << 3;
export const IS_LEGACY_FB_SUPPORT_MODE = 1 << 4;
```

<b>Vue.js</b>
```ts
// core/packages/shared/src/patchFlags.ts
export enum PatchFlags {
  TEXT = 1,
  CLASS = 1 << 1,
  STYLE = 1 << 2,
  PROPS = 1 << 3,
  FULL_PROPS = 1 << 4,
  // ...
}
```