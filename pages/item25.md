---
transition: fade-out
layout: side-title
side: l
color: violet
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 25

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
```

<v-click>
<br>
<b> Question: what's the type of fetchPages()</b>
```ts {monaco}
function fetchPages() {
  fetch('url1').then(response1 => {
    return fetch('url2');
  }).catch(error => {
  
  })
}
```
</v-click>

---
transition: fade-out
layout: side-title
side: l
color: violet
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 25

:: content ::

# Top level await

<v-click>
You can use the await keyword on its own (outside of an async function) at the top level of a module.
```ts {monaco}
function findAnswer() {
  return new Promise((resolve, reject) => {
    resolve('answer');
  });
}

await findAnswer();
```
</v-click>