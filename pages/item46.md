---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 46

<UsagiItem2e text="Item 66 (2e)"/>

:: content ::

# Understand the Three Versions Involved in Type Declarations

- The version of the package
- The version of its type declarations (@types)
- The version of TypeScript

# And also your IDE
- The version of TypeScript in your IDE (VSCode)

<v-click>
If any of these versions get out of sync with one another, you can run into errors that may not be clearly related to dependency management.
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

# Item 46

<UsagiItem2e text="Item 66 (2e)"/>

:: content ::

# Install types as a dev dependency

```bash {1-2|all}
npm install react
# + react@18.2.0

npm install --save-dev @types/react
# + @types/react@18.2.23
```

<v-click>
<p>The patch versions of the @types module correspond to these sorts of fixes and additions.</p>
<p>In this case, there were many more updates to the type declarations than the library itself (23 versus 0).</p>
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

# Item 46

<UsagiItem2e text="Item 66 (2e)"/>

:: content ::

# Version matching can go wrong

- Update a library but forget to update its type declarations.
  - Auto update library by Dependabot
- Your type declarations might get ahead of your library.
- The type declarations might require a newer version of TypeScript

<v-click>
<h2>Question</h2>
Do you use Dependabot in your projects?
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

# Item 46

<UsagiItem2e text="Item 66 (2e)"/>

:: content ::

# Different type declarations for different versions of TypeScript

Install @types for a specific version of TypeScript

```bash
npm install --save-dev @types/react@ts4.9
```

(Under 1% of packages on DefinitelyTyped do)

---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 46

<UsagiItem2e text="Item 66 (2e)"/>

:: content ::

# Bundling type declarations
If the library is written in TypeScript, this works well in practice since tsc can automatically generate type declarations for you

```bash
tsc --declaration

```
<br/>

<v-click>

# Publishing them on DefinitelyTyped.
For JavaScript libraries, handcrafted type declarations are more likely to contain errors, and they’ll require more updates.
</v-click>