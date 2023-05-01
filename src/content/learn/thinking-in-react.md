---
title: Thinking in React
---

<Intro>

React আপনার দেখা ডিজাইন এবং তৈরী করা অ্যাপসগুলি সম্বন্ধে আপনার চিন্তাভাবনা পরিবর্তন করতে পারে। React দিয়ে আপনি যখন একটি ইউজার ইন্টারফেস তৈরি করবেন, প্রথমে আপনি এটি কম্পোনেন্ট নামে বিভিন্ন অংশে ভাগ করে ফেলবেন। তারপর, আপনি আপনার প্রতিটি কম্পোনেন্টের জন্য বিভিন্ন দৃশ্যমান state বর্ণনা করবেন। সবশেষে, আপনি আপনার কম্পোনেন্টগুলি এমনভাবে সংযুক্ত করবেন যাতে তাদের মাঝে ডেটা প্রবাহিত হয়। এই টিউটোরিয়ালে, আমরা রিয়্যাক্ট দিয়ে একটি অনুসন্ধানযোগ্য পণ্যের ডেটা টেবিল তৈরীর চিন্তা প্রক্রিয়া কেমন হবে সে বিষয়ে ধারণা করাতে আপনাকে সহায়তা করব।

</Intro>

## মকাপ দিয়ে শুরু করুন {/*start-with-the-mockup*/}

ধরে নিন, আপনার কাছে ইতোমধ্যে একজন ডিজাইনারের কাছ থেকে পাওয়া মকাপ আছে এবং একটি JSON API ও আছে। 

JSON API যে তথ্য রিটার্ন করে সেটা কিছুটা এমন দেখতেঃ

```json
[
  { category: "Fruits", price: "$1", stocked: true, name: "Apple" },
  { category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit" },
  { category: "Fruits", price: "$2", stocked: false, name: "Passionfruit" },
  { category: "Vegetables", price: "$2", stocked: true, name: "Spinach" },
  { category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin" },
  { category: "Vegetables", price: "$1", stocked: true, name: "Peas" }
]
```

মকাপটা দেখতে এমনঃ

<img src="/images/docs/s_thinking-in-react_ui.png" width="300" style={{margin: '0 auto'}} />

React এ একটি UI ইমপ্লিমেন্ট করতে আপনাকে সাধারণত নিম্নের ৫টি ধাপ অনুসরণ করতে হবে।

## ধাপ ১ঃ UI কে একটি কম্পোনেন্ট hierarchy তে বিন্যস্ত করুন {/*step-1-break-the-ui-into-a-component-hierarchy*/}

মকাপে সবগুলো কম্পোনেন্ট এবং সাবকম্পোনেন্ট এর চারিদিকে বক্স আঁকার মাধ্যমে শুরু করেন। সেগুলোর নামকরণ করুন। যদি আপনি একজন ডিজাইনারের সাথে কাজ করে থাকেন, দেখা যেতে পারে উনি ইতোমধ্যে তার ডিজাইনে এই কম্পোনেন্টগুলোর নামকরণ করে রেখেছেন। উনার কাছ থেকে জেনে নিন।

একটি ডিজাইনের কম্পোনেন্ট গুলোকে বিভিন্ন ভাবে আপনি ভাগ করতে পারেন। কীভাবে করবেন সেটা নির্ভর করবে আপনার কাজের ক্ষেত্রের উপর।

* **Programming**--একটি নতুন function বা object তৈরী করবেন কি না এই সিদ্ধান্তটি যেভাবে নিতেন, ঠিক একই পদ্ধতিতে সিদ্ধান্ত নিন। এমন একটি পদ্ধতি হচ্ছে [single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle), যা অনুসারে, একটা কম্পোনেন্ট আদর্শত কেবল একটি কাজই করবে। যদি সেটা বড় হয়ে যায় তাহলে ছোট ছোট সাবকম্পোনেন্ট এ ভাগ করে ফেলতে হবে। 
* **CSS**--আপনি class selector কীসের জন্য তৈরী করতেন সেটা বিবেচনায় রাখুন (যদিও কম্পোনেন্ট আরেকটু কম granular)।
* **Design**--চিন্তা করুন আপনি আপনার ডিজাইনের layer গুলো কীভাবে করতেন।

যদি আপনার JSON গোছানো থাকে, আপনি দেখবেন বেশির ভাগ সময় এটা স্বাভাবিকতই আপনার UI এর কম্পোনেন্ট এর গঠন বিন্যাসের সাথে মিলে যাবে। এর কারণ UI এবং ডেটা মডেলগুলো সাধারণত একই information architecture ব্যবহার করে, অর্থাৎ একই আকারে বিন্যস্ত হয়। আপনার UI কে এমন ভাবে কম্পোনেন্ট এ ভাগ করুন যেন প্রতিটি কম্পোনেন্ট আপনার ডেটা মডেলের একটি অংশের সাথে মিলে যায়। 

এখানে ৫টি কম্পোনেন্ট রয়েছেঃ

<FullWidth>

<CodeDiagram flip>

<img src="/images/docs/s_thinking-in-react_ui_outline.png" width="500" style={{margin: '0 auto'}} />

1. `FilterableProductTable` (grey) পুরো অ্যাপটিকে ধারণ করে।
2. `SearchBar` (blue) ইউজারের ইনপুট নেয়।
3. `ProductTable` (lavender) ফিল্টারগুলো দেখায় এবং ইউজারের ইনপুটের হিসেবে তালিকা দেখায়।
4. `ProductCategoryRow` (green) প্রতিটি ক্যাটাগরির জন্য একটি শিরোনাম দেখায়।
5. `ProductRow`	(yellow) প্রতিটি পণের জন্য একটি সারি দেখায়।

</CodeDiagram>

</FullWidth>

আপনি যদি `ProductTable` (lavender) খেয়াল করেন, আপনি দেখবেন যে টেবিল হেডারে (যার মধ্যে "Name" এবং "Price" লেবেলগুলো রয়েছে) নিজেই নিজের কম্পোনেন্ট না। এটা আপনার পছন্দ অনুযায়ী সিদ্ধান্তের বিষয়। আপনি যেকোন দিকে যেতে পারেন। এই উদাহরণে, এটা `ProductTable` এর অংশ কারণ এটা `ProductTable`এর তালিকার মধ্যে দেখা যায়। কিন্তু, এই হেডার যদি জটিল আকার ধারণ করে (উদাহরণস্বরূপ, আপনি যদি সর্টিং যুক্ত করতে চান), আপনি এটাকে এর নিজের `ProductTableHeader` কম্পোনেন্টে নিয়ে যেতে পারেন।

এখন যেহেতু আপনি মকাপে কম্পোনেন্টগুলো চিনে ফেলেছেন, সেগুলোকে একটা hierarchy তে সাজিয়ে ফেলুন। মকাপে যেই কম্পোনেন্টগুলো অন্য একটি কম্পোনেন্ট এর মধ্যে রয়েছে সেগুলো hierarchy তে child component হিসেবে দেখানো উচিত।

* `FilterableProductTable`
    * `SearchBar`
    * `ProductTable`
        * `ProductCategoryRow`
        * `ProductRow`

## ধাপ ২ঃ React এ একটি স্ট্যাটিক ভার্সন তৈরী করুন {/*step-2-build-a-static-version-in-react*/}

Now that you have your component hierarchy, it's time to implement your app. The most straightforward approach is to build a version that renders the UI from your data model without adding any interactivity... yet! It's often easier to build the static version first and add interactivity later. Building a static version requires a lot of typing and no thinking, but adding interactivity requires a lot of thinking and not a lot of typing.
এখন যেহেতু আপনার কাছে কম্পোনেন্ট hierarchy আছে, এখন সময় অ্যাপ ইমপ্লিমেন্ট করার। সবচেয়ে সোজাসাপ্টা পথ হল এমন একটা ভার্সন তৈরী করা যেটা নতুন কোন interactivity যুক্ত না করে আপনার ডেটা মডেল থেকে UI তৈরী করতে পারে...কেবল মাত্র শুরুর জন্য! বেশিরভাগ সময়ে প্রথমে একটি স্ট্যাটিক ভার্সন তৈরী করা এবং পরে এর সাথে interactivity যুক্ত করা সহজ হয়। স্ট্যাটিক ভার্সন তৈরী করতে প্রচুর কোড লেখবার দরকার পড়ে এবং চিন্তা করতে হয় কম। অন্যদিকে interactivity যুক্ত করার জন্য চিন্তা করতে হয় অনেক এবং এত বেশি লেখার দরকার পড়ে না।     

To build a static version of your app that renders your data model, you'll want to build [components](/learn/your-first-component) that reuse other components and pass data using [props.](/learn/passing-props-to-a-component) Props are a way of passing data from parent to child. (If you're familiar with the concept of [state](/learn/state-a-components-memory), don't use state at all to build this static version. State is reserved only for interactivity, that is, data that changes over time. Since this is a static version of the app, you don't need it.)

প্রথমে বানাতে হবে আপনার অ্যাপের একটা স্ট্যাটিক ভার্সন যা আপনার ডেটা মডেল প্রদর্শন করতে পারে। এজন্য আপনি এমন [components](/learn/your-first-component) বানাতে চাইবেন যা অন্যান্য কম্পোনেন্ট ব্যবহার করবে এবং ন [props](/learn/passing-props-to-a-component) ব্যবহার করে ডেটা আদান প্রদান করবে। Parent থেকে child এ ডেটা পাঠাতে props ব্যবহার করা হয়। (যদি আপনার [state](/learn/state-a-components-memory)এর বিষয়ে জানাশোনা থাকে, এই স্ট্যাটিক ভার্সন বানাতে গিয়ে state এর কথা একদমই মাথায় আনবেন না। State শুধুমাত্র interactivityর জন্য অর্থাৎ সেই ডেটা যা সময়ের সাথে সাথে বদলায়। যেহেতু এইটা আপনার অ্যাপের একটি স্ট্যাটিক ভার্সন, আপনার state এর প্রয়োজন নেই।)


You can either build "top down" by starting with building the components higher up in the hierarchy (like `FilterableProductTable`) or "bottom up" by working from components lower down (like `ProductRow`). In simpler examples, it’s usually easier to go top-down, and on larger projects, it’s easier to go bottom-up.
আপনি "top down" পন্থায় যেতে পারেন, যেখানে hierarchy উপর থেকে নিচের দিকে কম্পোনেন্টগুলো আপনি বানাতে থাকবেন (যেমন `FilterableProductTable`) অথবা "bottom up" পদ্ধতি ব্যবহার করতে পারেন যেক্ষেত্রে  আগে নিচের দিকের কম্পোনেন্টগুলো বানাতে হবে এবং পর্যায়ক্রমে উপরের দিকে যাবেন (যেমন `ProductRow`)।  সরল একটা অ্যাপের ক্ষেত্রে top-down করাই সাধারণত সহজতর হয়, একটু জটিল বড় প্রজেক্টের ক্ষেত্রে bottom-up করা সুবিধাজনক হয়।

<Sandpack>

```jsx App.js
function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar() {
  return (
    <form>
      <input type="text" placeholder="Search..." />
      <label>
        <input type="checkbox" />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

function FilterableProductTable({ products }) {
  return (
    <div>
      <SearchBar />
      <ProductTable products={products} />
    </div>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 10px;
}
td {
  padding: 2px;
  padding-right: 40px;
}
```

</Sandpack>

(If this code looks intimidating, go through the [Quick Start](/learn/) first!)
(এই কোডটি বেশি জটিল মনে হলে, [Quick Start](/learn/) আগে দেখে নিন!)

After building your components, you'll have a library of reusable components that render your data model. Because this is a static app, the components will only return JSX. The component at the top of the hierarchy (`FilterableProductTable`) will take your data model as a prop. This is called _one-way data flow_ because the data flows down from the top-level component to the ones at the bottom of the tree.
কম্পোনেন্ট বানানো হয়ে গেলে, আপনার কাছে একটি লাইব্রেরি থাকবে যেখানে এমন কম্পোনেন্ট থাকবে যা আপনার ডেটা মডেলকে প্রদর্শন করে এবং যা পুনরায় ব্যবহারযোগ্য। যেহেতু এটি একটি স্ট্যাটিক অ্যাপ, সুতরাং কম্পোনেন্টগুলি কেবল JSX রিটার্ন করবে। আপনার hierarchyর একদম শীর্ষে থাকা কম্পোনেন্ট (`FilterableProductTable`) আপনার ডেটা মডলকে prop হিসেবে গ্রহণ করবে। একে বলা হয় _one-way data flow_ কারণ এক্ষেত্রে tree-তে উপরের দিকে থাকা কম্পোনেন্টগুলো থেকে নিচের দিকে থাকা কম্পোনেন্টের দিকে ডেটা প্রবাহিত হয়।

<Pitfall>

At this point, you should not be using any state values. That’s for the next step!
এ পর্যন্ত আপনার কোন state value ব্যবহার করা উচিত হবে না। সেটা পরবর্তী ধাপের জন্য!

</Pitfall>

## Step 3: Find the minimal but complete representation of UI state {/*step-3-find-the-minimal-but-complete-representation-of-ui-state*/}

To make the UI interactive, you need to let users change your underlying data model. You will use *state* for this.

Think of state as the minimal set of changing data that your app needs to remember. The most important principle for structuring state is to keep it [DRY (Don't Repeat Yourself).](https://en.wikipedia.org/wiki/Don%27t_repeat_yourself) Figure out the absolute minimal representation of the state your application needs and compute everything else on-demand. For example, if you're building a shopping list, you can store the items as an array in state. If you want to also display the number of items in the list, don't store the number of items as another state value--instead, read the length of your array.

Now think of all of the pieces of data in this example application:

1. The original list of products
2. The search text the user has entered
3. The value of the checkbox
4. The filtered list of products

Which of these are state? Identify the ones that are not:

* Does it **remain unchanged** over time? If so, it isn't state.
* Is it **passed in from a parent** via props? If so, it isn't state.
* **Can you compute it** based on existing state or props in your component? If so, it *definitely* isn't state!

What's left is probably state.

Let's go through them one by one again:

1. The original list of products is **passed in as props, so it's not state.** 
2. The search text seems to be state since it changes over time and can't be computed from anything.
3. The value of the checkbox seems to be state since it changes over time and can't be computed from anything.
4. The filtered list of products **isn't state because it can be computed** by taking the original list of products and filtering it according to the search text and value of the checkbox.

This means only the search text and the value of the checkbox are state! Nicely done!

<DeepDive>

#### Props vs State {/*props-vs-state*/}

There are two types of "model" data in React: props and state. The two are very different:

* [**Props** are like arguments you pass](/learn/passing-props-to-a-component) to a function. They let a parent component pass data to a child component and customize its appearance. For example, a `Form` can pass a `color` prop to a `Button`.
* [**State** is like a component’s memory.](/learn/state-a-components-memory) It lets a component keep track of some information and change it in response to interactions. For example, a `Button` might keep track of `isHovered` state.

Props and state are different, but they work together. A parent component will often keep some information in state (so that it can change it), and *pass it down* to child components as their props. It's okay if the difference still feels fuzzy on the first read. It takes a bit of practice for it to really stick!

</DeepDive>

## Step 4: Identify where your state should live {/*step-4-identify-where-your-state-should-live*/}

After identifying your app’s minimal state data, you need to identify which component is responsible for changing this state, or *owns* the state. Remember: React uses one-way data flow, passing data down the component hierarchy from parent to child component. It may not be immediately clear which component should own what state. This can be challenging if you’re new to this concept, but you can figure it out by following these steps!

For each piece of state in your application:

1. Identify *every* component that renders something based on that state.
2. Find their closest common parent component--a component above them all in the hierarchy.
3. Decide where the state should live:
    1. Often, you can put the state directly into their common parent.
    2. You can also put the state into some component above their common parent.
    3. If you can't find a component where it makes sense to own the state, create a new component solely for holding the state and add it somewhere in the hierarchy above the common parent component.

In the previous step, you found two pieces of state in this application: the search input text, and the value of the checkbox. In this example, they always appear together, so it makes sense to put them into the same place.

Now let's run through our strategy for them:

1. **Identify components that use state:**
    * `ProductTable` needs to filter the product list based on that state (search text and checkbox value). 
    * `SearchBar` needs to display that state (search text and checkbox value).
1. **Find their common parent:** The first parent component both components share is `FilterableProductTable`.
2. **Decide where the state lives**: We'll keep the filter text and checked state values in `FilterableProductTable`.

So the state values will live in `FilterableProductTable`. 

Add state to the component with the [`useState()` Hook.](/reference/react/useState) Hooks are special functions that let you "hook into" React. Add two state variables at the top of `FilterableProductTable` and specify their initial state:

```js
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);  
```

Then, pass `filterText` and `inStockOnly` to `ProductTable` and `SearchBar` as props:

```js
<div>
  <SearchBar 
    filterText={filterText} 
    inStockOnly={inStockOnly} />
  <ProductTable 
    products={products}
    filterText={filterText}
    inStockOnly={inStockOnly} />
</div>
```

You can start seeing how your application will behave. Edit the `filterText` initial value from `useState('')` to `useState('fruit')` in the sandbox code below. You'll see both the search input text and the table update:

<Sandpack>

```jsx App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} />
      <ProductTable 
        products={products}
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding-top: 5px;
}
td {
  padding: 2px;
}
```

</Sandpack>

Notice that editing the form doesn't work yet. There is a console error in the sandbox above explaining why:

<ConsoleBlock level="error">

You provided a \`value\` prop to a form field without an \`onChange\` handler. This will render a read-only field.

</ConsoleBlock>

In the sandbox above, `ProductTable` and `SearchBar` read the `filterText` and `inStockOnly` props to render the table, the input, and the checkbox. For example, here is how `SearchBar` populates the input value:

```js {1,6}
function SearchBar({ filterText, inStockOnly }) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} 
        placeholder="Search..."/>
```

However, you haven't added any code to respond to the user actions like typing yet. This will be your final step.


## Step 5: Add inverse data flow {/*step-5-add-inverse-data-flow*/}

Currently your app renders correctly with props and state flowing down the hierarchy. But to change the state according to user input, you will need to support data flowing the other way: the form components deep in the hierarchy need to update the state in `FilterableProductTable`. 

React makes this data flow explicit, but it requires a little more typing than two-way data binding. If you try to type or check the box in the example above, you'll see that React ignores your input. This is intentional. By writing `<input value={filterText} />`, you've set the `value` prop of the `input` to always be equal to the `filterText` state passed in from `FilterableProductTable`. Since `filterText` state is never set, the input never changes.

You want to make it so whenever the user changes the form inputs, the state updates to reflect those changes. The state is owned by `FilterableProductTable`, so only it can call `setFilterText` and `setInStockOnly`. To let `SearchBar` update the `FilterableProductTable`'s state, you need to pass these functions down to `SearchBar`:

```js {2,3,10,11}
function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly}
        onFilterTextChange={setFilterText}
        onInStockOnlyChange={setInStockOnly} />
```

Inside the `SearchBar`, you will add the `onChange` event handlers and set the parent state from them:

```js {5}
<input 
  type="text" 
  value={filterText} 
  placeholder="Search..." 
  onChange={(e) => onFilterTextChange(e.target.value)} />
```

Now the application fully works!

<Sandpack>

```jsx App.js
import { useState } from 'react';

function FilterableProductTable({ products }) {
  const [filterText, setFilterText] = useState('');
  const [inStockOnly, setInStockOnly] = useState(false);

  return (
    <div>
      <SearchBar 
        filterText={filterText} 
        inStockOnly={inStockOnly} 
        onFilterTextChange={setFilterText} 
        onInStockOnlyChange={setInStockOnly} />
      <ProductTable 
        products={products} 
        filterText={filterText}
        inStockOnly={inStockOnly} />
    </div>
  );
}

function ProductCategoryRow({ category }) {
  return (
    <tr>
      <th colSpan="2">
        {category}
      </th>
    </tr>
  );
}

function ProductRow({ product }) {
  const name = product.stocked ? product.name :
    <span style={{ color: 'red' }}>
      {product.name}
    </span>;

  return (
    <tr>
      <td>{name}</td>
      <td>{product.price}</td>
    </tr>
  );
}

function ProductTable({ products, filterText, inStockOnly }) {
  const rows = [];
  let lastCategory = null;

  products.forEach((product) => {
    if (
      product.name.toLowerCase().indexOf(
        filterText.toLowerCase()
      ) === -1
    ) {
      return;
    }
    if (inStockOnly && !product.stocked) {
      return;
    }
    if (product.category !== lastCategory) {
      rows.push(
        <ProductCategoryRow
          category={product.category}
          key={product.category} />
      );
    }
    rows.push(
      <ProductRow
        product={product}
        key={product.name} />
    );
    lastCategory = product.category;
  });

  return (
    <table>
      <thead>
        <tr>
          <th>Name</th>
          <th>Price</th>
        </tr>
      </thead>
      <tbody>{rows}</tbody>
    </table>
  );
}

function SearchBar({
  filterText,
  inStockOnly,
  onFilterTextChange,
  onInStockOnlyChange
}) {
  return (
    <form>
      <input 
        type="text" 
        value={filterText} placeholder="Search..." 
        onChange={(e) => onFilterTextChange(e.target.value)} />
      <label>
        <input 
          type="checkbox" 
          checked={inStockOnly} 
          onChange={(e) => onInStockOnlyChange(e.target.checked)} />
        {' '}
        Only show products in stock
      </label>
    </form>
  );
}

const PRODUCTS = [
  {category: "Fruits", price: "$1", stocked: true, name: "Apple"},
  {category: "Fruits", price: "$1", stocked: true, name: "Dragonfruit"},
  {category: "Fruits", price: "$2", stocked: false, name: "Passionfruit"},
  {category: "Vegetables", price: "$2", stocked: true, name: "Spinach"},
  {category: "Vegetables", price: "$4", stocked: false, name: "Pumpkin"},
  {category: "Vegetables", price: "$1", stocked: true, name: "Peas"}
];

export default function App() {
  return <FilterableProductTable products={PRODUCTS} />;
}
```

```css
body {
  padding: 5px
}
label {
  display: block;
  margin-top: 5px;
  margin-bottom: 5px;
}
th {
  padding: 4px;
}
td {
  padding: 2px;
}
```

</Sandpack>

You can learn all about handling events and updating state in the [Adding Interactivity](/learn/adding-interactivity) section.

## Where to go from here {/*where-to-go-from-here*/}

This was a very brief introduction to how to think about building components and applications with React. You can [start a React project](/learn/installation) right now or [dive deeper on all the syntax](/learn/describing-the-ui) used in this tutorial.
