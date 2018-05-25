<!--
  This file was generated by emdaer

  Its template can be found at /Users/flipactual/Dev/la-rado/.emdaer/README.emdaer.md
-->

<!--
  emdaerHash:4c728162d38b79d005a56ec548d665eb
-->

<p align="center"><img src="https://raw.githubusercontent.com/flipactual/la-rado/master/banner.svg?sanitize=true" alt="La Rado"></p>

<h1 id="la-rado-travis-bundlephobia-node-npm">la-rado · <a href="https://travis-ci.org/flipactual/la-rado/"><img src="https://img.shields.io/travis/flipactual/la-rado.svg?style=flat-square" alt="Travis"></a> <a href="https://bundlephobia.com/result?p=la-rado"><img src="https://img.shields.io/bundlephobia/minzip/la-rado.svg?style=flat-square" alt="bundlephobia"></a> <a href="http://npmjs.com/package/la-rado"><img src="https://img.shields.io/node/v/la-rado.svg?style=flat-square" alt="Node"></a> <a href="http://npmjs.com/package/la-rado"><img src="https://img.shields.io/npm/v/la-rado.svg?style=flat-square" alt="NPM"></a></h1>
<blockquote>
<p>La Rado is Esperanto for “The Wheel” 😉</p>
</blockquote>
<h2 id="why">Why</h2>
<p>It’s a good question — why did I need to roll my own state management library?</p>
<p>First of all, I didn’t need to and other options may very well better suit your needs</p>
<p>But, since you asked:</p>
<ul>
<li>🐣 it’s tiny (~¼kB last time I checked) </li>
<li>🔤 it’s simple (one class whose instances surface only two methods)</li>
<li>🚀 it’s op af (caveat being that there’s no hand-holding whatsoever)</li>
</ul>
<h2 id="how">How</h2>
<p>If you’re wondering how state management can be over-powered…</p>
<h3 id="1-let-s-create-a-new-store-">1. Let’s create a new store…</h3>
<p>Describe the initial state… may as well save it somewhere, right?</p>

```js
const INITIAL_STATE = Object.freeze({ on: false });
```
<p>Create the store by passing the initial state into the constructor</p>

```js
const Store = new LaRado(INITIAL_STATE);
```
<p>Now you have a store</p>
<h3 id="2-and-subscribe-to-the-store-">2. And subscribe to the store…</h3>
<p>We’ll just send state updates to the console for now</p>

```js
const subscriber = console.log;
```
<p>Passing a subscriber to the store returns a function which cancels the subscription… let’s hang onto that</p>

```js
const cancel = Store.subscribe(subscriber);
// => { on: false }
```
<p>All subscribers receive the current state when added to the store</p>
<h3 id="3-and-update-the-state-">3. And update the state…</h3>
<p>This is where La Rado likely diverges from state managers you’ve used before</p>
<p>You may notice that we haven’t talked at all about updating state yet</p>
<p>That’s because you can update state in anyway that you like at any point because actions are simply functions passed to the store which take the current state as their argument and return the new state</p>
<p>So let’s create an action</p>

```js
const toggleOn = state => ({ ...state, on: !state.on });
```
<p>And perform an update</p>

```js
Store.update(toggleOn);
// => { on: true }
```
<p>And that’s La Rado!</p>
<h3 id="4-and-clean-up">4. And clean up</h3>
<p>You can add and remove subscribers at any point</p>
<p>So let’s cancel our subscription now that we’re done</p>

```js
cancel();
```
<h3 id="5-then-read-the-docs-">5. <a href="https://flipactual.github.io/la-rado/">Then read the docs!</a></h3>
<hr>
<p>la-rado is <a href="./LICENSE">MIT licensed</a>.</p>
