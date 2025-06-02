---
transition: fade-out
layout: side-title
side: l
color: yellow-light
titlewidth: is-4
align: rm-lm

---
:: title ::

# Item 49

<UsagiItem2e text="Item 69 (2e)"/>

:: content ::

# Provide a Type for this in Callbacks if It’s Part of Their API

this in class and method

```ts {monaco-run} {autorun:false}  
class MyMath {
  values = [1, 2, 3];
  logSquares() {
    for (const value of this.values) {
      console.log(value ** 2);
    }
  }
}

const math = new MyMath();
const logSquares = math.logSquares;
logSquares();
```

<v-click>
<h2>Question</h2>
What is this in method?
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

# Item 49

<UsagiItem2e text="Item 69 (2e)"/>

:: content ::

# this in event handlers

```ts {monaco}
document.querySelector('input')
  ?.addEventListener('change', function(e) {
    console.log(this);
  }
);
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

# Item 49

<UsagiItem2e text="Item 69 (2e)"/>

:: content ::

# this in React class component

```tsx {all|6,18}
import React from 'react';
class Car extends React.Component {
  constructor(props) {
    super(props);
    this.state = { color: "red", };
    this.changeColor = this.changeColor.bind(this);
  }

  changeColor() {
    this.setState({ color: "blue"});
  }

  render() {
    return (
      <div>
        <button
          type="button"
          onClick={this.changeColor}
        >
          Change color
        </button>
      </div>
    );
  }
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

# Item 49

<UsagiItem2e text="Item 69 (2e)"/>

:: content ::

# Add a this parameter to your callback

```ts {monaco}
function addKeyListener(
  el: HTMLElement,
  listener: (this: HTMLElement, event: KeyboardEvent) => void
) {
  el.addEventListener('keydown', event => {
    listener.call(el, event);
  });
}
```
<br />

<v-click>
<h2>Don’t forget about this!</h2>
If you set the value of this in your callbacks, then it’s part of your API, and you should include it in your type declarations.
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

# Item 49

<UsagiItem2e text="Item 69 (2e)"/>

:: content ::

# What IS this?

<Youtube id="yV53mkoOW1E" width="550px" height="300px"/>


---
transition: fade-out
layout: quote
color: yellow-light
quotesize: text-m
authorsize: text-s

---

"If you’re designing a new API, try not to use dynamic this binding. While it was historically popular, it has always been a source of confusion, and the prevalence of arrow functions makes this sort of API much harder to use in modern JavaScript."

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
