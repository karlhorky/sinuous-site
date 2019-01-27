# 🇨🇭element + [lit-html](https://github.com/Polymer/lit-html)

```js
import { element, useState, renderer } from 'swiss-element';
import { html, render } from 'lit-html';

function dispatch(el, first, last) {
  let event = new CustomEvent('change', {
    detail: first + ' ' + last
  });
  el.dispatchEvent(event);
}

function App() {
  const [name, setName] = useState('');

  return html`
    <h2>User Page</h2>

    <h3>${name}</h3>

    <p>Change name:</p>
    <full-name @change="${ev => ev.detail && setName(ev.detail)}"> </full-name>
  `;
}

element('my-app', App, renderer(render));

function FullName(el) {
  const [first, setFirst] = useState('Swiss');
  const [last, setLast] = useState('Cheese 🧀');

  dispatch(el, first, last);

  return html`
    <div class="container">
      <label for="first">First</label>
      <input
        value="${first}"
        @keyup="${ev => setFirst(ev.target.value)}"
        type="text"
        name="first"
      />

      <label for="last">Last</label>
      <input
        value="${last}"
        @keyup="${ev => setLast(ev.target.value)}"
        type="text"
        name="last"
      />
    </div>

    <style>
      .container {
        border: none;
        display: grid;
        grid-template-columns: 20% 80%;
      }

      input {
        border: 1px solid #e5e5e5;
        padding: 6px 10px;
        margin-bottom: 1em;
      }
    </style>
  `;
}

element('full-name', FullName, renderer(render));
```
