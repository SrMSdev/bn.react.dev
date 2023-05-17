---
title: 'Referencing Values with Refs'
---

<Intro>

যখন আপনি চান যে একটা কম্পোনেন্ট কোন একটা তথ্য "মনে রাখুক", কিন্তু আপনি চান না যে এই তথ্য নতুন কোন [রেন্ডার চালু করে দিক](/learn/render-and-commit), আপনি একটা *ref* ব্যবহার করতে পারেন।

</Intro>

<YouWillLearn>

- কীভাবে কম্পোনেন্টে ref যুক্ত করবেন
- কীভাবে একটি ref এর মান পরিবর্তন করবেন
- state এর সাথে ref এর তফাৎ কোথায়
- কীভাবে নিরাপদভাবে ref ব্যবহার করা যায়

</YouWillLearn>

## আপনার কম্পোনেন্টে ref এর সংযুক্তি {/*adding-a-ref-to-your-component*/}

React থেকে `useRef` hook ইম্পোর্ট করার মাধ্যমে আপনার কম্পোনেন্টে একটি ref যুক্ত করতে পারেনঃ

```js
import { useRef } from 'react';
```

আপনার কম্পোনেন্টের মধ্যে, `useRef` hook-টি কল করুন এবং এর মধ্যে আপনি যেই প্রাথমিক মান reference হিসেবে দিতে চান সেটা একমাত্র argument হিসেবে পাঠিয়ে দিন। উদাহরণস্বরূপ, এখানে  `0` মানটির একটি ref রয়েছে।

```js
const ref = useRef(0);
```

`useRef` এমন একটি অবজেক্ট রিটার্ন করেঃ

```js
{ 
  current: 0 // The value you passed to useRef
}
```

<Illustration src="/images/docs/illustrations/i_ref.png" alt="An arrow with 'current' written on it stuffed into a pocket with 'ref' written on it." />

আপনি `ref.current` property-র মাধ্যমে ঐ ref এর বর্তমান মান অ্যাক্সেস করতে পারেন। এই মানটি ইচ্ছাকৃতভাবে পরিবর্তনশীল, অর্থাৎ আপনি এটি read এবং write করতে পারেন। এটি আপনার কম্পোনেন্টের একটি গোপন পকেটের মতো যা React ট্র্যাক করে না। (এই বৈশিষ্ট্যটাই একে React এর একমুখী ডেটা প্রবাহ থেকে একটি "escape hatch" বানায়--নিচে এটি সম্পর্কে আরও তথ্য রয়েছে!)

এখানে, একটি বাটন প্রতিটি ক্লিকে `ref.current` এর মান বাড়াবে:

<Sandpack>

```js
import { useRef } from 'react';

export default function Counter() {
  let ref = useRef(0);

  function handleClick() {
    ref.current = ref.current + 1;
    alert('You clicked ' + ref.current + ' times!');
  }

  return (
    <button onClick={handleClick}>
      Click me!
    </button>
  );
}
```

</Sandpack>

ref একটি সংখ্যা নির্দেশ করে, তবে, [state](/learn/state-a-components-memory) এর মত, আপনি যে কোন কিছুর দিকে নির্দেশ করতে পারেন: একটি স্ট্রিং, একটি অবজেক্ট, বা এমনকি একটি ফাংশন। state এর বিপরীতে, ref একটি সাধারণ জাভাস্ক্রিপ্ট অবজেক্ট যার `current` property রয়েছে, যা আপনি read করতে এবং পরিবর্তন করতে পারেন।

লক্ষ্য করুন যে **প্রতি increment এর সাথে কম্পোনেন্টটি পুনরায় রেন্ডার হয় না।** state এর মত, রেন্ডারের ফাঁকে ফাঁকে React ref-কে সংরক্ষণ করে। তবে, state সেট করলে একটি কম্পোনেন্ট পুনরায় রেন্ডার হয়। ref এর পরিবর্তনে সেটা হয় না!

## উদাহরণঃ একটি স্টপওয়াচ যেভাবে বানাবেন {/*example-building-a-stopwatch*/}

আপনি একটি কম্পোনেন্টের মধ্যে refs এবং state একসাথে সমন্বয় করতে পারেন। উদাহরণস্বরূপ, চলেন একটি স্টপওয়াচ তৈরি করি যেটি ব্যবহারকারী একটি বাটন চাপের মাধ্যমে শুরু বা বন্ধ করতে পারবে। ব্যবহারকারী "Start" চাপার পরে কতটা সময় পার হয়েছে তা প্রদর্শন করার জন্য, আপনাকে স্টার্ট বোতাম চাপা হয়েছে তার সময় এবং বর্তমান সময় কী তা হিসেব রাখতে হবে। **এই তথ্যটি রেন্ডারিং এর জন্য ব্যবহৃত হয়, তাই আপনি এটি state এ রাখবেন:**

```js
const [startTime, setStartTime] = useState(null);
const [now, setNow] = useState(null);
```

ব্যবহারকারী যখন "Start" চাপবে, আপনি প্রতি 10 মিলিসেকেন্ড পর পর সময় আপডেট করার জন্য [`setInterval`](https://developer.mozilla.org/docs/Web/API/setInterval) ব্যবহার করবেন:

<Sandpack>

```js
import { useState } from 'react';

export default function Stopwatch() {
  const [startTime, setStartTime] = useState(null);
  const [now, setNow] = useState(null);

  function handleStart() {
    // Start counting.
    setStartTime(Date.now());
    setNow(Date.now());

    setInterval(() => {
      // Update the current time every 10ms.
      setNow(Date.now());
    }, 10);
  }

  let secondsPassed = 0;
  if (startTime != null && now != null) {
    secondsPassed = (now - startTime) / 1000;
  }

  return (
    <>
      <h1>Time passed: {secondsPassed.toFixed(3)}</h1>
      <button onClick={handleStart}>
        Start
      </button>
    </>
  );
}
```

</Sandpack>

"Stop" বোতাম চাপা হলে, আপনাকে বিদ্যমান interval বাতিল করতে হবে যাতে এটি state ভেরিয়েবল `now` আপডেট করা বন্ধ করে। আপনি এটি [`clearInterval`](https://developer.mozilla.org/en-US/docs/Web/API/clearInterval) কল করে করতে পারেন, কিন্তু আপনাকে এটিকে সেই interval ID দিতে হবে যা ব্যবহারকারী Start চাপলে পূর্বে `setInterval` কল থেকে return পাওয়া গিয়েছিল। আপনাকে interval ID-টি কোথাও রাখতে হবে। **যেহেতু interval ID রেন্ডারিং এর জন্য ব্যবহৃত হয় না, আপনি এটিকে একটি ref এ রাখতে পারেন:**

<Sandpack>

```js
import { useState, useRef } from 'react';

export default function Stopwatch() {
  const [startTime, setStartTime] = useState(null);
  const [now, setNow] = useState(null);
  const intervalRef = useRef(null);

  function handleStart() {
    setStartTime(Date.now());
    setNow(Date.now());

    clearInterval(intervalRef.current);
    intervalRef.current = setInterval(() => {
      setNow(Date.now());
    }, 10);
  }

  function handleStop() {
    clearInterval(intervalRef.current);
  }

  let secondsPassed = 0;
  if (startTime != null && now != null) {
    secondsPassed = (now - startTime) / 1000;
  }

  return (
    <>
      <h1>Time passed: {secondsPassed.toFixed(3)}</h1>
      <button onClick={handleStart}>
        Start
      </button>
      <button onClick={handleStop}>
        Stop
      </button>
    </>
  );
}
```

</Sandpack>

রেন্ডারিং এর জন্য একটি তথ্য ব্যবহার করা হলে, এটি state এ রাখুন। যখন কোন তথ্য কেবলমাত্র event handler-গুলি দ্বারা প্রয়োজন হয় এবং এর পরিবর্তনে পুনরায় রেন্ডার করা প্রয়োজন হয় না, সেক্ষেত্রে ref ব্যবহার করা অধিক কার্যকর হতে পারে।

## ref এবং state এর মধ্যকার পার্থক্য {/*differences-between-refs-and-state*/}

হয়তো আপনি মনে করছেন ref, state এর তুলনায় কম "কঠোর" - উদাহরণস্বরূপ, আপনি এগুলোকে পরিবর্তন করতে পারেন যেখানে state-এর ক্ষেত্রে সর্বদা state সেটিং ফাংশন ব্যবহার করার প্রয়োজন। কিন্তু বেশিরভাগ ক্ষেত্রে, আপনি state-ই ব্যবহার করতে চাইবেন। Ref গুলো একটি "escape hatch" যা আপনার খুব একটা প্রয়োজন হবে না। এখানে state এবং ref এর তুলনা কিভাবে হয় তা দেখুনঃ

| refs                                                                                  | state                                                                                                                     |
| ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `useRef(initialValue)` রিটার্ন করে `{ current: initialValue }`                            | `useState(initialValue)` রিটার্ন করে একটি stat variable এর বর্তমান মান এবং একটি state setter function ( `[value, setValue]`) |
|  যখন আপনি এর পরিবর্তন করেন, re-render trigger করে না।                                   | এর পরিবর্তন করা হলে re-render trigger করে                                                                                    |
| পরিবর্তনযোগ্য—রেন্ডারিং প্রক্রিয়ার বাইরে আপনি `current` এর মান পরিবর্তন করে আপডেট করতে পারবেন।| "পরিবর্তনযোগ্য নয়"—একটা re-render, queue এ ঢুকানোর জন্য আপনাকে অবশ্যই state setting function ব্যবহার করে state variable পরিবর্তন করতে হবে।                       |
| রেন্ডারিং এর সময় `current` এর মান আপনার read বা write করা উচিত নয়। | আপনি যেকোন সময়ে state read করতে পারেন। কিন্তু প্রতি রেন্ডারের নিজের state এর [snapshot](/learn/state-as-a-snapshot) আছে যা বদলায় না।

এখানে state ব্যবহার করে বানানো একটি counter বাটন দেখুনঃ

<Sandpack>

```js
import { useState } from 'react';

export default function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);
  }

  return (
    <button onClick={handleClick}>
      You clicked {count} times
    </button>
  );
}
```

</Sandpack>

যেহেতু `count` এর মানটি দেখানো হয়, এর জন্য একটি state মান ব্যবহার করা যুক্তিযুক্ত। যখন counter-এর মানটি `setCount()` দিয়ে সেট করা হয়, React কম্পোনেন্টটি পুনরায় রেন্ডার করে এবং স্ক্রিন নতুন কাউন্ট দেখানোর জন্য আপডেট হয়।

যদি আপনি এটি ref দিয়ে বানানোর করার চেষ্টা করতেন, তাহলে React কখনই কম্পোনেন্টটি পুনরায় রেন্ডার করত না, তাই আপনি কখনই কাউন্টের পরিবর্তন দেখতেন না! দেখুন এই বাটনে ক্লিক করলে কীভাবে এর **টেক্সট আপডেট হয় নাঃ**

<Sandpack>

```js
import { useRef } from 'react';

export default function Counter() {
  let countRef = useRef(0);

  function handleClick() {
    // This doesn't re-render the component!
    countRef.current = countRef.current + 1;
  }

  return (
    <button onClick={handleClick}>
      You clicked {countRef.current} times
    </button>
  );
}
```

</Sandpack>

এ কারণেই রেন্ডারের সময় `ref.current` read করলে সেটা কোডের নির্ভরযোগ্যতা কমিয়ে ফেলে। যদি আপনার সেটা করার প্রয়োজন হয়, বরং state ব্যবহার করেন।

<DeepDive>

#### useRef ভিতরে ভিতরে কীভাবে কাজ করে? {/*how-does-use-ref-work-inside*/}

যদিও `useState` এবং `useRef` উভয়ই React দেয়, মূলত `useRef`,  `useState` এর _উপরে_ ব্যবহার করা যেতে পারে। আপনি কল্পনা করতে পারেন যে React এর মধ্যে, `useRef` এর বাস্তবায়ন এরকমঃ

```js
// Inside of React
function useRef(initialValue) {
  const [ref, unused] = useState({ current: initialValue });
  return ref;
}
```

প্রথম রেন্ডারের সময় `useRef` রিটার্ন করে `{ current: initialValue }`। এই অবজেক্টটি React সংরক্ষণ করে, সুতরাং পরবর্তী রেন্ডারের সময় একই অবজেক্টটি return করে। লক্ষ্য করুন যে এই উদাহরণে state setter ব্যবহার করা হয়নি। এটি অপ্রয়োজনীয় কারণ `useRef` এর সর্বদা একই অবজেক্ট ফিরিয়ে দেওয়া প্রয়োজন!

React একটি built-in `useRef` দেয় কারণ সাধারণত এর ব্যবহার বেশ ভালই হয়। কিন্তু আপনি এটিকে একটি সাধারণ state ভেরিয়েবল হিসাবে চিন্তা করতে পারেন যার কোনও সেটার নেই। যদি আপনি object-oriented programming এর সাথে পরিচিত হন, তাহলে ref আপনাকে instance fields এর কথা মনে করিয়ে দিতে পারে -- কিন্তু `this.something` এর পরিবর্তে আপনি এক্ষেত্রে `somethingRef.current` লিখছেন।

</DeepDive>

## কখন ref ব্যবহার করবেন {/*when-to-use-refs*/}

সাধারণত, আপনি একটি ref ব্যবহার করবেন যখন আপনার component এর React এর বাইরে "পা রাখতে হবে" এবং বাইরের API এর সাথে যোগাযোগ করতে হবে - প্রায়শই এটা হবে একটি ব্রাউজার API যা কম্পোনেন্টের চেহারার উপর প্রভাব ফেলবে না। এখানে কিছু পরিস্থিতির উদাহরণ দেওয়া হচ্ছে যা্র দেখা খুব হঠাতই হয়ত মিলবেঃ

- [timeout IDs](https://developer.mozilla.org/docs/Web/API/setTimeout) store করতে।
- [DOM elements](https://developer.mozilla.org/docs/Web/API/Element) store করা এবং সেখানে পরিবর্তন আনা, এটা আমরা [পরের পাতায়](/learn/manipulating-the-dom-with-refs) বর্ণনা করেছি।
- অন্যান্য অব্জেক্ট store করা যা JSX হিসেব করতে প্রয়োজন পড়ে না।

যদি আপনার কম্পোনেন্টে কোন মান store করার দরকার পড়ে, এবং এটা রেন্ডার করার হিসেবে কোন প্রভাব না ফেলে তবে ref ব্যবহার করুন।

## ref ব্যবহারের ক্ষেত্রে যা যা মেনে চলা ভাল {/*best-practices-for-refs*/}

নিম্নোক্ত মূলনীতিগুলো মাথায় রাখলে আপনার কম্পোনেন্টগুলো আরো বেশি নির্ভরযোগ্য আচরণ করবেঃ

- **ref কে escape hatch হিসেবে ব্যবহার করুন।** যখন আপনি বাইরের কোন সিস্টেম বা ব্রাউজার API ব্যবহার করছেন তখন ref বেশ কাজের। যদি আপনার অ্যাপ্লিকেশনের বেশিরভাগ লজিক এবং ডেটা প্রবার ref এর উপর নির্ভরশীল হয় তবে আপনার উচিত আপনার আগানোর প্রক্রিয়া নিয়ে আবার ভাবা।
- **রেন্ডারিং এর সময় `ref.current` read বা write করবেন না।** যদি রেন্ডারিং এর সময় কোন তথ্যের প্রয়োজন পড়ে, তখন বরঞ্চ [state](/learn/state-a-components-memory) ব্যবহার করুন। যেহেতু React জানে না কখন `ref.current` বদলায়, রেন্ডারিং এর সময়ে একে এমনকি read করতে গেলেও আপনার কম্পোনেন্টের আচার আচরণ বোঝা কঠিন হয়ে যাবে। ( এর একমাত্র ব্যতিক্রম হবে তখন যখন আপনি `if (!ref.current) ref.current = new Thing()` এভাবে কোড করছেন, যা একদম প্রথম রেন্ডারের সময়ে ref সেট করে। )

React state এর যে সীমাবদ্ধতা তা ref এর নেই। উদাহরণস্বরূপ, state [প্রতিটি রেন্ডারের একটি স্ন্যাপশটের](/learn/state-as-a-snapshot) মত কাজ করে এবং [synchronously আপডেট করে না।](/learn/queueing-a-series-of-state-updates) কিন্তু আপনি যখন একটি ref এর বর্তমান মান পরিবর্তন করেন, তখন তা সাথে সাথে পরিবর্তিত হয়।

```js
ref.current = 5;
console.log(ref.current); // 5
```

This is because **the ref itself is a regular JavaScript object,** and so it behaves like one.

You also don't need to worry about [avoiding mutation](/learn/updating-objects-in-state) when you work with a ref. As long as the object you're mutating isn't used for rendering, React doesn't care what you do with the ref or its contents.

## Refs and the DOM {/*refs-and-the-dom*/}

You can point a ref to any value. However, the most common use case for a ref is to access a DOM element. For example, this is handy if you want to focus an input programmatically. When you pass a ref to a `ref` attribute in JSX, like `<div ref={myRef}>`, React will put the corresponding DOM element into `myRef.current`. You can read more about this in [Manipulating the DOM with Refs.](/learn/manipulating-the-dom-with-refs)

<Recap>

- Refs are an escape hatch to hold onto values that aren't used for rendering. You won't need them often.
- A ref is a plain JavaScript object with a single property called `current`, which you can read or set.
- You can ask React to give you a ref by calling the `useRef` Hook.
- Like state, refs let you retain information between re-renders of a component.
- Unlike state, setting the ref's `current` value does not trigger a re-render.
- Don't read or write `ref.current` during rendering. This makes your component hard to predict.

</Recap>



<Challenges>

#### Fix a broken chat input {/*fix-a-broken-chat-input*/}

Type a message and click "Send". You will notice there is a three second delay before you see the "Sent!" alert. During this delay, you can see an "Undo" button. Click it. This "Undo" button is supposed to stop the "Sent!" message from appearing. It does this by calling [`clearTimeout`](https://developer.mozilla.org/en-US/docs/Web/API/clearTimeout) for the timeout ID saved during `handleSend`. However, even after "Undo" is clicked, the "Sent!" message still appears. Find why it doesn't work, and fix it.

<Hint>

Regular variables like `let timeoutID` don't "survive" between re-renders because every render runs your component (and initializes its variables) from scratch. Should you keep the timeout ID somewhere else?

</Hint>

<Sandpack>

```js
import { useState } from 'react';

export default function Chat() {
  const [text, setText] = useState('');
  const [isSending, setIsSending] = useState(false);
  let timeoutID = null;

  function handleSend() {
    setIsSending(true);
    timeoutID = setTimeout(() => {
      alert('Sent!');
      setIsSending(false);
    }, 3000);
  }

  function handleUndo() {
    setIsSending(false);
    clearTimeout(timeoutID);
  }

  return (
    <>
      <input
        disabled={isSending}
        value={text}
        onChange={e => setText(e.target.value)}
      />
      <button
        disabled={isSending}
        onClick={handleSend}>
        {isSending ? 'Sending...' : 'Send'}
      </button>
      {isSending &&
        <button onClick={handleUndo}>
          Undo
        </button>
      }
    </>
  );
}
```

</Sandpack>

<Solution>

Whenever your component re-renders (such as when you set state), all local variables get initialized from scratch. This is why you can't save the timeout ID in a local variable like `timeoutID` and then expect another event handler to "see" it in the future. Instead, store it in a ref, which React will preserve between renders.

<Sandpack>

```js
import { useState, useRef } from 'react';

export default function Chat() {
  const [text, setText] = useState('');
  const [isSending, setIsSending] = useState(false);
  const timeoutRef = useRef(null);

  function handleSend() {
    setIsSending(true);
    timeoutRef.current = setTimeout(() => {
      alert('Sent!');
      setIsSending(false);
    }, 3000);
  }

  function handleUndo() {
    setIsSending(false);
    clearTimeout(timeoutRef.current);
  }

  return (
    <>
      <input
        disabled={isSending}
        value={text}
        onChange={e => setText(e.target.value)}
      />
      <button
        disabled={isSending}
        onClick={handleSend}>
        {isSending ? 'Sending...' : 'Send'}
      </button>
      {isSending &&
        <button onClick={handleUndo}>
          Undo
        </button>
      }
    </>
  );
}
```

</Sandpack>

</Solution>


#### Fix a component failing to re-render {/*fix-a-component-failing-to-re-render*/}

This button is supposed to toggle between showing "On" and "Off". However, it always shows "Off". What is wrong with this code? Fix it.

<Sandpack>

```js
import { useRef } from 'react';

export default function Toggle() {
  const isOnRef = useRef(false);

  return (
    <button onClick={() => {
      isOnRef.current = !isOnRef.current;
    }}>
      {isOnRef.current ? 'On' : 'Off'}
    </button>
  );
}
```

</Sandpack>

<Solution>

In this example, the current value of a ref is used to calculate the rendering output: `{isOnRef.current ? 'On' : 'Off'}`. This is a sign that this information should not be in a ref, and should have instead been put in state. To fix it, remove the ref and use state instead:

<Sandpack>

```js
import { useState } from 'react';

export default function Toggle() {
  const [isOn, setIsOn] = useState(false);

  return (
    <button onClick={() => {
      setIsOn(!isOn);
    }}>
      {isOn ? 'On' : 'Off'}
    </button>
  );
}
```

</Sandpack>

</Solution>

#### Fix debouncing {/*fix-debouncing*/}

In this example, all button click handlers are ["debounced".](https://redd.one/blog/debounce-vs-throttle) To see what this means, press one of the buttons. Notice how the message appears a second later. If you press the button while waiting for the message, the timer will reset. So if you keep clicking the same button fast many times, the message won't appear until a second *after* you stop clicking. Debouncing lets you delay some action until the user "stops doing things".

This example works, but not quite as intended. The buttons are not independent. To see the problem, click one of the buttons, and then immediately click another button. You'd expect that after a delay, you would see both button's messages. But only the last button's message shows up. The first button's message gets lost.

Why are the buttons interfering with each other? Find and fix the issue.

<Hint>

The last timeout ID variable is shared between all `DebouncedButton` components. This is why clicking one button resets another button's timeout. Can you store a separate timeout ID for each button?

</Hint>

<Sandpack>

```js
let timeoutID;

function DebouncedButton({ onClick, children }) {
  return (
    <button onClick={() => {
      clearTimeout(timeoutID);
      timeoutID = setTimeout(() => {
        onClick();
      }, 1000);
    }}>
      {children}
    </button>
  );
}

export default function Dashboard() {
  return (
    <>
      <DebouncedButton
        onClick={() => alert('Spaceship launched!')}
      >
        Launch the spaceship
      </DebouncedButton>
      <DebouncedButton
        onClick={() => alert('Soup boiled!')}
      >
        Boil the soup
      </DebouncedButton>
      <DebouncedButton
        onClick={() => alert('Lullaby sung!')}
      >
        Sing a lullaby
      </DebouncedButton>
    </>
  )
}
```

```css
button { display: block; margin: 10px; }
```

</Sandpack>

<Solution>

A variable like `timeoutID` is shared between all components. This is why clicking on the second button resets the first button's pending timeout. To fix this, you can keep timeout in a ref. Each button will get its own ref, so they won't conflict with each other. Notice how clicking two buttons fast will show both messages.

<Sandpack>

```js
import { useRef } from 'react';

function DebouncedButton({ onClick, children }) {
  const timeoutRef = useRef(null);
  return (
    <button onClick={() => {
      clearTimeout(timeoutRef.current);
      timeoutRef.current = setTimeout(() => {
        onClick();
      }, 1000);
    }}>
      {children}
    </button>
  );
}

export default function Dashboard() {
  return (
    <>
      <DebouncedButton
        onClick={() => alert('Spaceship launched!')}
      >
        Launch the spaceship
      </DebouncedButton>
      <DebouncedButton
        onClick={() => alert('Soup boiled!')}
      >
        Boil the soup
      </DebouncedButton>
      <DebouncedButton
        onClick={() => alert('Lullaby sung!')}
      >
        Sing a lullaby
      </DebouncedButton>
    </>
  )
}
```

```css
button { display: block; margin: 10px; }
```

</Sandpack>

</Solution>

#### Read the latest state {/*read-the-latest-state*/}

In this example, after you press "Send", there is a small delay before the message is shown. Type "hello", press Send, and then quickly edit the input again. Despite your edits, the alert would still show "hello" (which was the value of state [at the time](/learn/state-as-a-snapshot#state-over-time) the button was clicked).

Usually, this behavior is what you want in an app. However, there may be occasional cases where you want some asynchronous code to read the *latest* version of some state. Can you think of a way to make the alert show the *current* input text rather than what it was at the time of the click?

<Sandpack>

```js
import { useState, useRef } from 'react';

export default function Chat() {
  const [text, setText] = useState('');

  function handleSend() {
    setTimeout(() => {
      alert('Sending: ' + text);
    }, 3000);
  }

  return (
    <>
      <input
        value={text}
        onChange={e => setText(e.target.value)}
      />
      <button
        onClick={handleSend}>
        Send
      </button>
    </>
  );
}
```

</Sandpack>

<Solution>

State works [like a snapshot](/learn/state-as-a-snapshot), so you can't read the latest state from an asynchronous operation like a timeout. However, you can keep the latest input text in a ref. A ref is mutable, so you can read the `current` property at any time. Since the current text is also used for rendering, in this example, you will need *both* a state variable (for rendering), *and* a ref (to read it in the timeout). You will need to update the current ref value manually.

<Sandpack>

```js
import { useState, useRef } from 'react';

export default function Chat() {
  const [text, setText] = useState('');
  const textRef = useRef(text);

  function handleChange(e) {
    setText(e.target.value);
    textRef.current = e.target.value;
  }

  function handleSend() {
    setTimeout(() => {
      alert('Sending: ' + textRef.current);
    }, 3000);
  }

  return (
    <>
      <input
        value={text}
        onChange={handleChange}
      />
      <button
        onClick={handleSend}>
        Send
      </button>
    </>
  );
}
```

</Sandpack>

</Solution>

</Challenges>
