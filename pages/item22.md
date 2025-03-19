---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# Use in keyword to narrow

```ts {monaco}
interface Apple { isGoodForBaking: boolean; }
interface Orange { numSlices: number; }

function pickFruit(fruit: Apple | Orange) {
  if ('isGoodForBaking' in fruit) {
    fruit
  } else {
    fruit
  }
  fruit
}
pickFruit({ isGoodForBaking: true });
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

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# null is object

```ts {monaco}
const elem = document.getElementById('what-time-is-it');
if (typeof elem === 'object') {
  elem;
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

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# Why object is null?

<v-click>
The type tags were stored in the lower bits of the units. There were five of them:

- 000: object. The data is a reference to an object.
- 001: int. The data is a 31 bit signed integer.
- 010: double. The data is a reference to a double floating point number.
- 100: string. The data is a reference to a string.
- 110: boolean. The data is a boolean.
</v-click>

<v-click>
null (JSVAL_NULL) was the machine code NULL pointer. Or: an object type tag plus a reference that is zero.
It can’t be fixed because it would break the existing code.
</v-click>

---
transition: fade-out
layout: quote
color: sky-light
quotesize: text-m
authorsize: text-s
author: 'Hyrum''s Law'

---

"With a sufficient number of users of an API,
it does not matter what you promise in the contract:
all observable behaviors of your system
will be depended on by somebody."

<div class="flex justify-center mt-4">
  <img src="/images/ChikawaDraw.png" width="300px" />
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

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# Falsy primitive values

```ts {monaco}
function maybeLogX(x?: number | string | null) {
  if (!x) {
    x
  }
}
maybeLogX();

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

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# Discriminated union

```ts {monaco}
type NetworkLoadingState = {
  state: 'loading';
};
type NetworkFailedState = {
  state: 'failed';
  code: number;
};
type NetworkSuccessState = {
  state: 'success';
  response: {
    title: string;
    duration: number;
    summary: string;
  };
};
type NetworkState =
  | NetworkLoadingState
  | NetworkFailedState
  | NetworkSuccessState;

function checkNetwork (network: NetworkState){
  if (network.state === 'loading') {
    network
  }
}
checkNetwork({ state: 'loading' });
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

# Item 22

<HachiwareItem2e text="Item 22 (2e)"/>

:: content ::

# User-defined type guard

```ts {monaco}
function isInputElement(element: Element): element is HTMLInputElement {
  return 'value' in element;
}

function getElementContent(element: HTMLElement) {
  if (isInputElement(element)) {
    return element.value;
  }
  return element.textContent;
}
getElementContent(document.getElementById('submit')!);

const formElements = document.querySelectorAll('.register-form *');
const formInputElements = [...formElements].filter(isInputElement);
```