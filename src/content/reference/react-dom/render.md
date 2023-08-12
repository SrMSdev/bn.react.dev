---
title: render
---

<Deprecated>

এই API ভবিষ্যতে React এর একটি মেজর ভার্সনে সরিয়ে ফেলা হবে।

React 18 এ, `render` এর জায়গায় এসেছে [`createRoot`।](/reference/react-dom/client/createRoot) React 18 এ `render` ব্যবহার করলে সতর্কতা দেখাবে যে আপনার অ্যাপ এমন আচরণ করবে যেন এতে React 17 চলছে। আরো জানুন [এখানে।](/blog/2022/03/08/react-18-upgrade-guide#updates-to-client-rendering-apis)

</Deprecated>

<Intro>

`render` ব্রাউজারের একটি DOM নোডে [JSX](/learn/writing-markup-with-jsx) ("React node") এর একটি অংশ রেন্ডার করে।

```js
render(reactNode, domNode, callback?)
```

</Intro>

<InlineToc />

---

## রেফারেন্স {/*reference*/}

### `render(reactNode, domNode, callback?)` {/*render*/}

একটি ব্রাউজার DOM এলিমেন্টের মধ্যে একটি React component দেখানোর জন্য `render` কল করুন।

```js
import { render } from 'react-dom';

const domNode = document.getElementById('root');
render(<App />, domNode);
```

React will display `<App />` in the `domNode`, and take over managing the DOM inside it.

An app fully built with React will usually only have one `render` call with its root component.  A page that uses "sprinkles" of React for parts of the page may have as many `render` calls as needed.

[See more examples below.](#usage)

#### Parameters {/*parameters*/}

* `reactNode`: A *React node* that you want to display. This will usually be a piece of JSX like `<App />`, but you can also pass a React element constructed with [`createElement()`](/reference/react/createElement), a string, a number, `null`, or `undefined`. 

* `domNode`: A [DOM element.](https://developer.mozilla.org/en-US/docs/Web/API/Element) React will display the `reactNode` you pass inside this DOM element. From this moment, React will manage the DOM inside the `domNode` and update it when your React tree changes.

* **optional** `callback`: A function. If passed, React will call it after your component is placed into the DOM.


#### রিটার্ন {/*returns*/}

`render` সাধারণত `null` রিটার্ন করে। তবে, আপনি যে `reactNode` পাস করছেন সেটা যদি *ক্লাস component* হয়, তাহলে এটা ওই component এর একটি ইন্সট্যান্স রিটার্ন করবে।

#### সতর্কতা {/*caveats*/}

* React 18 এ, `render` কে প্রতিস্থাপন করেছে [`createRoot`.](/reference/react-dom/client/createRoot) দয়া করে React 18 এবং তার পরবর্তী ভার্সনগুলোর জন্য `createRoot` ব্যবহার করবেন।

* আপনি প্রথম বার `render` কল করার সময়, React `domNode` এর ভেতরে React component রেন্ডার করার আগে এর ভেতরকার সকল HTML কনটেন্ট মুছে ফেলবে। যদি আপনার `domNode` এ সার্ভারের React দ্বারা তৈরি বা বিল্ডের সময় তৈরি HTML থাকে, বরং [`hydrate()`](/reference/react-dom/hydrate) ব্যবহার করুন, যা আগে থেকে থাকা HTML এর সাথে ইভেন্ট হ্যান্ডলার যুক্ত করে দেয়।

* আপনি যদি একই `domNode` এ একাধিক বার `render` কল করেন, React আপনার পাস করে সর্বশেষ JSX এর প্রতিফলন দেখানোর জন্য DOM আপডেট করে দেবে। React সিদ্ধান্ত নিবে যে DOM এর কোন কোন অংশ পুনরায় ব্যবহার করা জাবর এবং কোনগুলো আবার আগের বার রেন্ডার হওয়া ট্রি এর সাথে ["মিলানোর মাধ্যমে"](/learn/preserving-and-resetting-state) পুনরায় তৈরি করা দরকার। একই `domNode` এ একাধিক বার `render` কল করা রুট component এ [`set` function](/reference/react/useState#setstate) কল করার মতঃ React avoids অপ্রয়োজনীয় DOM আপডেট এড়িয়ে চলে।

* If your app is fully built with React, you'll likely have only one `render` call in your app. (If you use a framework, it might do this call for you.) When you want to render a piece of JSX in a different part of the DOM tree that isn't a child of your component (for example, a modal or a tooltip), use [`createPortal`](/reference/react-dom/createPortal) instead of `render`.

---

## ব্যবহার {/*usage*/}

একটি <CodeStep step={2}>ব্রাউজার DOM নোডের</CodeStep> ভেতর একটি <CodeStep step={1}>React component</CodeStep> দেখানোর জন্য `render` কল করুন।

```js [[1, 4, "<App />"], [2, 4, "document.getElementById('root')"]]
import { render } from 'react-dom';
import App from './App.js';

render(<App />, document.getElementById('root'));
```

### রুট component রেন্ডার করা {/*rendering-the-root-component*/}

সম্পূর্ণভাবে React দিয়ে তৈরি এমন অ্যাপের জন্য, **আপনি সাধারণত এটা startup এর সময় এক বার করবেন**--"root" component রেন্ডার করবার জন্য।

<Sandpack>

```js index.js active
import './styles.css';
import { render } from 'react-dom';
import App from './App.js';

render(<App />, document.getElementById('root'));
```

```js App.js
export default function App() {
  return <h1>Hello, world!</h1>;
}
```

</Sandpack>

সাধারণত আপনার `render` আবার কল দেবার বা আরো জায়গায় কল দেবার প্রয়োজন হবার কথা না। এই জায়গা থেকে, React আপনার অ্যাপ্লিকেশনের DOM ম্যানেজ করবে। UI আপডেটের জন্য, আপনার component গুলো [state ব্যবহার করবে।](/reference/react/useState)

---

### একাধিক রুট রেন্ডার করা {/*rendering-multiple-roots*/}

যদি আপনার পেইজ [সম্পূর্ণ রূপে React দিয়ে তৈরি না হয়ে থাকে](/learn/add-react-to-an-existing-project#using-react-for-a-part-of-your-existing-page), React ম্যানেজ করে এরকম সকল উচ্চ স্তরের UI এর জন্য `render` কল করুন।

<Sandpack>

```html public/index.html
<nav id="navigation"></nav>
<main>
  <p>This paragraph is not rendered by React (open index.html to verify).</p>
  <section id="comments"></section>
</main>
```

```js index.js active
import './styles.css';
import { render } from 'react-dom';
import { Comments, Navigation } from './Components.js';

render(
  <Navigation />,
  document.getElementById('navigation')
);

render(
  <Comments />,
  document.getElementById('comments')
);
```

```js Components.js
export function Navigation() {
  return (
    <ul>
      <NavLink href="/">Home</NavLink>
      <NavLink href="/about">About</NavLink>
    </ul>
  );
}

function NavLink({ href, children }) {
  return (
    <li>
      <a href={href}>{children}</a>
    </li>
  );
}

export function Comments() {
  return (
    <>
      <h2>Comments</h2>
      <Comment text="Hello!" author="Sophie" />
      <Comment text="How are you?" author="Sunil" />
    </>
  );
}

function Comment({ text, author }) {
  return (
    <p>{text} — <i>{author}</i></p>
  );
}
```

```css
nav ul { padding: 0; margin: 0; }
nav ul li { display: inline-block; margin-right: 20px; }
```

</Sandpack>

আপনি [`unmountComponentAtNode()`](/reference/react-dom/unmountComponentAtNode) ব্যবহার করে রেন্ডার হওয়া ট্রি আপডেট করতে পারেন।

---

### Render হওয়া ট্রি এর আপডেট {/*updating-the-rendered-tree*/}

আপনি একই DOM নোডে একাধিক বার `render` কল করতে পারেন। As long as the component tree structure matches up with what was previously rendered, React will [preserve the state.](/learn/preserving-and-resetting-state) Notice how you can type in the input, which means that the updates from repeated `render` calls every second are not destructive:

<Sandpack>

```js index.js active
import { render } from 'react-dom';
import './styles.css';
import App from './App.js';

let i = 0;
setInterval(() => {
  render(
    <App counter={i} />,
    document.getElementById('root')
  );
  i++;
}, 1000);
```

```js App.js
export default function App({counter}) {
  return (
    <>
      <h1>Hello, world! {counter}</h1>
      <input placeholder="Type something here" />
    </>
  );
}
```

</Sandpack>

`render` সাধারণত একাধিকবার কল দেওয়া হয় না। সাধারণত, আপনি তা না করে আপনার component এর মধ্যে [update state](/reference/react/useState) করবেন।
