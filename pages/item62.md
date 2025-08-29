---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 62

<UsagiItem2e />

:: content ::

# Item 62: Use Rest Parameters and Tuple Types to Model Variadic Functions

```ts {monaco}
interface RouteQueryParams {
  '/': null,
  '/search': { query: string; language?: string; }
  // ...
}

function buildURL<Path extends keyof RouteQueryParams>(
  route: Path,
  params: RouteQueryParams[Path]
) {
  return route + (params ? `?${new URLSearchParams(params)}` : '');
}

buildURL('/search', {query: 'do a barrel roll'})
buildURL('/search', {query: 'do a barrel roll', language: 'en'})
buildURL('/', {query: 'recursion'});  // error, good!
//            ~~~~~~~~~~~~~~~~~~~~ Argument of type '{ query: string; }' is
//                                 not assignable to parameter of type 'null'
buildURL('/', null);  // ok
buildURL('/');  // we'd like this to be allowed
// ~~~~~ Expected 2 arguments, but got 1.
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

# Item 62

<UsagiItem2e />

:: content ::

# Use a conditional type and rest parameters

```ts {monaco}
interface RouteQueryParams {
  '/': null,
  '/search': { query: string; language?: string; }
  // ...
}

function buildURL<Path extends keyof RouteQueryParams>(
  route: Path,
  ...args: (
      RouteQueryParams[Path] extends null
      ? []
      : [params: RouteQueryParams[Path]]
    )
) {
  const params = args ? args[0] : null;
  return route + (params ? `?${new URLSearchParams(params)}` : '');
}

buildURL('/', {query: 'recursion'});
//            ~~~~~~~~~~~~~~~~~~~~ Expected 1 arguments, but got 2.
buildURL('/', null);
//            ~~~~ Expected 1 arguments, but got 2.
buildURL('/');  // ok
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

# Item 62

<UsagiItem2e />

:: content ::

# Label parameter name

```ts {3-7}
function buildURL<Path extends keyof RouteQueryParams>(
  route: Path,
  ...args: (
      RouteQueryParams[Path] extends null
      ? []
      : [params: RouteQueryParams[Path]]
    )
) {
  const params = args ? args[0] : null;
  return route + (params ? `?${new URLSearchParams(params)}` : '');
}
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

# Item 62

<UsagiItem2e />

:: content ::

# Remove label parameter name

```ts {monaco}
interface RouteQueryParams {
  '/': null,
  '/search': { query: string; language?: string; }
  // ...
}

function buildURL<Path extends keyof RouteQueryParams>(
  route: Path,
  ...args: (
      RouteQueryParams[Path] extends null
      ? []
      : [RouteQueryParams[Path]]
    )
) {
  const params = args ? args[0] : null;
  return route + (params ? `?${new URLSearchParams(params)}` : '');
}

buildURL('/', {query: 'recursion'});
//            ~~~~~~~~~~~~~~~~~~~~ Expected 1 arguments, but got 2.
buildURL('/', null);
//            ~~~~ Expected 1 arguments, but got 2.
buildURL('/');  // ok
```