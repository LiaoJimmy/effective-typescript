---
transition: fade-out
layout: side-title
side: l
color: pink-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 47

<ChiikawaItem2e text="Item 67 (2e)"/>

:: content ::

# Export All Types That Appear in Public APIs

Your users will be able to extract them anyway, so you may as well make it easy for them.

```ts {monaco}
interface SecretName {
  first: string;
  last: string;
}

interface SecretSanta {
  name: SecretName;
  gift: string;
}

export function getGift(name: SecretName, gift: string): SecretSanta {
  return { name, gift };
}
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

# Item 47

<ChiikawaItem2e text="Item 67 (2e)"/>

:: content ::

# Export All Types That Appear in Public APIs

`ReturnType<T>` and `Parameters<T>`

```ts {monaco}
interface SecretName {
  first: string;
  last: string;
}

interface SecretSanta {
  name: SecretName;
  gift: string;
}

export function getGift(name: SecretName, gift: string): SecretSanta {
  return { name, gift };
}

type MySanta = ReturnType<typeof getGift>;
type MyName = Parameters<typeof getGift>[0];
```