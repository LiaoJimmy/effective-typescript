---
transition: fade-out
layout: side-title
side: l
color: sky-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 25

<HachiwareItem2e text="Item 27 (2e)"/>

:: content ::

# Prefer async/await to raw Promises
It enforces that async functions always return Promises.

```ts {monaco}
async function fetchPages() {
  try {
    const response1 = await fetch('url1');
    const response2 = await fetch('url2');
    // ...
  } catch (error) {
    // ...
  }
}
await fetchPages();
```

<v-click>
<br>
<b> Question: what's the type of fetchPages()</b>
```ts {monaco}
function fetchPages() {
  fetch('url1').then(response1 => {
    return fetch('url2');
  }).catch(error => {
  
  });
}
fetchPages();
```
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

# Item 25

<HachiwareItem2e text="Item 27 (2e)"/>

:: content ::

# Top level await

<v-click>
You can use the await keyword on its own (outside of an async function) at the top level of a module.
```ts {monaco}
const findAnswer = async () => {
  return new Promise<string>((resolve, _) => {
    resolve('answer');
  });
}

await findAnswer();
```
</v-click>