---
title: নতুন প্রোজেক্ট শুরু করুন
---

<Intro>

আপনি যদি React দিয়ে কোন অ্যাপ বা ওয়েবসাইট বানাতে চান তাহলে, React কমিউনিটি ব্যাবহার করে এমন যেকোনো একটি জনপ্রিয় ফ্রেমওয়ার্ক ব্যাবহার করতে আমরা আপনাকে উৎসাহিত করব। এই ফ্রেমওয়ার্ক গুলো আপনাকে গুরুত্বপূর্ণ কিছু feature দিবে, যেমনঃ Routing, Data fetching এবং HTML generate করা, যা মোটামুটি সব ধরণের অ্যাপ অথবা ওয়েবসাইটের দরকার হয়।

</Intro>

<Note>

**লোকাল ডেভেলপমেন্টের জন্যে আপনার অবশ্যই [Node.js](https://nodejs.org/en/) ইন্সটল থাকতে হবে।** আপনি চাইলে আপনার production সার্ভারে Node.js ইন্সটল করতে পারেন কিন্তু এটা আবশ্যক নয় কারণ অনেক React ফ্রেমওয়ার্ক আপনার অ্যাপ বা ওয়েবসাইট এর স্ট্যাটিক HTML/CSS/JS তৈরি করে দেয়।

</Note>

## Production grade React ফ্রেমওয়ার্কের তালিকা {/*production-grade-react-frameworks*/}

### Next.js {/*nextjs*/}

**[Next.js](https://nextjs.org/) একটি full-stack React ফ্রেমওয়ার্ক।** এটি খুবই জনপ্রিয় এবং খুবই সহজে একটি ছোট ব্লগ ওয়েবসাইট অথবা অনেক বড় এবং জটিল অ্যাপ বানানোর জন্যে উপযোগী। নিচের কমান্ড টি আপনার টার্মিনাল এ রান করে আপনি একটি Next.js প্রোজেক্ট তৈরি করতে পারবেন।

<TerminalBlock>
npx create-next-app
</TerminalBlock>

আপনি যদি Next.js এ নতুন হয়ে থাকেন তাহলে তাদের অফিসিয়াল [Next.js tutorial](https://nextjs.org/learn/foundations/about-nextjs) দেখতে পারেন।

[Vercel](https://vercel.com/) Next.js এর রক্ষণাবেক্ষণের কাজ করে থাকে। যেকোনো Node.js অথবা serverless হোস্টিং, অথবা আপনার নিজস্ব সার্ভারে [একটি Next.js অ্যাপ deploy](https://nextjs.org/docs/deployment) করতে পারবেন। [সম্পূর্ণ স্ট্যাটিক Next.js অ্যাপ](https://nextjs.org/docs/advanced-features/static-html-export) যেকোনো স্ট্যাটিক হোস্টিং এ deploy করা যায়।

### Remix {/*remix*/}

**[Remix](https://remix.run/) হল nested routing সহ একটি full-stack React ফ্রেমওয়ার্ক।** এটি আপনার অ্যাপকে ছোট ছোট অংশে ভাগ করে যাতে সেগুলোকে পারালাল ভাবে ডাটা লোড করতে পারে। এটি ইউজার এর কাজের এর উপর ভিত্তি করে সেই ছোট ছোট অংশ গুলোকে রিফ্রেশ করতেও সাহায্য করে। নিচের কমান্ড টি আপনার টার্মিনাল এ রান করে আপনি একটি Remix প্রোজেক্ট তৈরি করতে পারবেন।

<TerminalBlock>
npx create-remix
</TerminalBlock>

আপনি যদি Remix এ নতুন হয়ে থাকেন তাহলে তাদের অফিসিয়াল Remix [blog tutorial](https://remix.run/docs/en/main/tutorials/blog) (short) এবং [app tutorial](https://remix.run/docs/en/main/tutorials/jokes) (long) দেখতে পারেন।

[Shopify](https://www.shopify.com/) Remix এর রক্ষণাবেক্ষণের কাজ করে থাকে। Remix প্রোজেক্ট তৈরি করার সময় আপনাকে আপনার [deployment target](https://remix.run/docs/en/main/guides/deployment) করে নিতে হবে। একটি [adapter](https://remix.run/docs/en/main/other-api/adapter) লিখে আপনি আপনার Remix অ্যাপ যেকোনো Node.js বা serverless হোস্টিং ব্যাবহার করে deploy করতে পারবেন।

### Gatsby {/*gatsby*/}

**[Gatsby](https://www.gatsbyjs.com/) একটি CMS ওয়েবসাইটগুলির জন্য React ফ্রেমওয়ার্ক।** এর সমৃদ্ধ প্লাগইন ইকোসিস্টেম এবং এর ডেটা লেয়ার কন্টেন্ট, APIs এবং সার্ভিস গুলকে একটি ওয়েবসাইটে একত্রিত করা সহজ করে। নিচের কমান্ড টি আপনার টার্মিনাল এ রান করে আপনি একটি Gatsby প্রোজেক্ট তৈরি করতে পারবেন।

<TerminalBlock>
npx create-gatsby
</TerminalBlock>

আপনি যদি Gatsby এ নতুন হয়ে থাকেন তাহলে তাদের অফিসিয়াল [Gatsby tutorial](https://www.gatsbyjs.com/docs/tutorial/) দেখতে পারেন।

[Netlify](https://www.netlify.com/) Gatsby এর রক্ষণাবেক্ষণের কাজ করে থাকে। আপনি যেকোন স্ট্যাটিক হোস্টিংয়ে একটি সম্পূর্ণ স্ট্যাটিক Gatsby সাইট deploy করতে পারবেন। আপনি যদি শুধুমাত্র সার্ভারের বৈশিষ্ট্যগুলি ব্যবহার করার বিকল্প বেছে নেন, তাহলে নিশ্চিত করুন যে আপনার হোস্টিংয়ে Gatsby এর জন্য সার্ভারের বৈশিষ্ট্যগুলি আছে।

### Expo (নেটিভ অ্যাপের জন্য) {/*expo*/}

যা আপনাকে সত্যিকারের নেটিভ UI সহ সার্বজনীন Android, iOS এবং ওয়েব অ্যাপ তৈরি করতে দেয়।

**[Expo](https://expo.dev/) হল একটি React ফ্রেমওয়ার্ক যা আপনাকে নেটিভ UI সহ অ্যান্ড্রয়েড, iOS এবং ওয়েব অ্যাপ তৈরি করতে দেয়।** এটি [React Native](https://reactnative.dev/) জন্য একটি SDK প্রদান করে যা native অংশগুলিকে ব্যবহার করা সহজ করে তোলে। নিচের কমান্ড টি আপনার টার্মিনাল এ রান করে আপনি একটি Expo প্রোজেক্ট তৈরি করতে পারবেন।

<TerminalBlock>
npx create-expo-app
</TerminalBlock>

আপনি যদি Expo এ নতুন হয়ে থাকেন তাহলে তাদের অফিসিয়াল [Expo tutorial](https://www.gatsbyjs.com/docs/tutorial/) দেখতে পারেন।

[Expo (the company)](https://expo.dev/about) Expo এর রক্ষণাবেক্ষণের কাজ করে থাকে। Expo দিয়ে বিনামূল্যে অ্যাপ তৈরি করতে পারবেন, এবং কোন সীমাবদ্ধতা ছাড়াই আপনি সেগুলিকে Google এবং Apple অ্যাপ স্টোরগুলিতে জমা দিতে পারবেন৷ Expo এছাড়াও অপ্ট-ইন ক্লাউড সার্ভিস প্রদান করে থাকে৷

<DeepDive>

#### আমি কি ফ্রেমওয়ার্ক ছাড়া React ব্যবহার করতে পারি? {/*can-i-use-react-without-a-framework*/}

আপনি অবশ্যই একটি ফ্রেমওয়ার্ক ছাড়া React ব্যবহার করতে পারেন--এইভাবে আপনি আপনার [পৃষ্ঠাটির একটি অংশের জন্য React ব্যবহার করবেন।](/learn/add-react-to-an-existing-project#using-react-for-a-part-of-your-existing-page) **পরিশেষে, আপনি যদি সম্পূর্ণভাবে React সহ একটি নতুন অ্যাপ বা সাইট তৈরি করেন, আমরা একটি ফ্রেমওয়ার্ক ব্যবহার করার পরামর্শ দিই।**

বিস্তারিত কারণ।

যদিও আপনার প্রথমে রাউটিং বা ডেটা আনার প্রয়োজন না হয়, পরবর্তীতে আপনি সম্ভবত তাদের জন্য কিছু লাইব্রেরি যোগ করতে চাইবেন। আপনার জাভাস্ক্রিপ্ট bundle প্রতিটি নতুন feature সাথে বৃদ্ধি পাওয়ার সাথে সাথে আপনাকে প্রতিটি রুটের জন্য পৃথকভাবে কোড বিভক্ত করার উপায় বের করতে হতে পারে। যেহেতু আপনার ডেটা আনার প্রয়োজনীয়তা আরও জটিল হয়ে উঠছে, আপনি সম্ভবত সার্ভার-ক্লায়েন্ট network waterfalls এর সম্মুখীন হতে পারেন যা আপনার অ্যাপকে খুব স্লো করে দিবে। যেহেতু আপনার ইউজার দের মধ্যে দুর্বল নেটওয়ার্ক সম্পন্ন এবং কম শক্তিশালী ডিভাইস ব্যবহারকারী থাকতে পারে, তাই আপনাকে জলদি কন্টেন্ট দেখানোর জন্য আপনার কম্পোনেন্টস থেকে HTML তৈরি করতে হতে পারে--সার্ভারে বা বিল্ডের এর সময়। সার্ভারে বা বিল্ডের সময় কিছু কোড চালানোর জন্য আপনার সেটআপ পরিবর্তন করা খুব কঠিন হতে পারে।

**এই সমস্যাগুলি React এর নয়। এই কারণেই Svelte এর SvelteKit আছে, Vue এর Nuxt আছে ইত্যাদি।** এই সমস্যাগুলি নিজে থেকে সমাধান করতে, আপনাকে রাউটার এবং ডেটা আনার লাইব্রেরির সাথে আপনার বান্ডলারকে সংযোগ করতে হবে। একটি প্রাথমিক কার্যকারী সেটআপ করা কঠিন নয়, তবে একটি অ্যাপ তৈরির সাথে অনেক সূক্ষ্মতা জড়িত থাকে যা সময়ের সাথে সাথে অ্যাপের সাইজ বাড়লেও দ্রুত লোড করতে পারেতে হয়। আপনি একটি পৃষ্ঠা লোড করার জন্যে নুন্নতম কোড পাঠাতে চাইবেন কিন্তু পৃষ্ঠার ডাটা প্যারালাল ভাবে লোড একটি একক ক্লায়েন্ট-সার্ভার রাউন্ডট্রিপে করতে চান। ওয়েবসাইটের Progressive enhancement এর জন্যে আপনি সম্ভবত আপনার জাভাস্ক্রিপ্ট কোডটি চালানোর আগে পৃষ্ঠাটি ইন্টারেক্টিভ করতে চাইবেন। আপনি আপনার মার্কেটিং পেইজ গুলির জন্য সম্পূর্ণরূপে স্ট্যাটিক HTML ফাইলগুলির একটি ফোল্ডার তৈরি করতে চাইতে পারেন যা যে কোনও জায়গায় হোস্ট করা যেতে পারে এবং জাভাস্ক্রিপ্ট বন্ধ থাকেলও কাজ করতে পারে। এই ক্ষমতাগুলি অ্যাপের মধ্যে তৈরি করতে আসল কাজ লাগে। 

**কোন অতিরিক্ত কাজ ছাড়াই এই পৃষ্ঠার React ফ্রেমওয়ার্ক গুলো ডিফল্টভাবে এই ধরনের সমস্যাগুলি সমাধান করে।** তারা আপনাকে খুব সহজে শুরু করতে সাহায্য করে এবং তারপরে আপনার প্রয়োজনের সাথে আপনার অ্যাপটি স্কেল করতে সাহায্য করে। প্রতিটি React ফ্রেমওয়ার্কের একটি কমিউনিটি রয়েছে, তাই প্রশ্নের উত্তর খুঁজে পাওয়া এবং টুলিং আপগ্রেড করা সহজ। ফ্রেমওয়ার্কগুলি আপনার কোডের কাঠামোও দেয়, আপনাকে এবং অন্যদেরকে বিভিন্ন প্রকল্পের মধ্যে প্রসঙ্গ এবং দক্ষতা বজায় রাখতে সাহায্য করে। বিপরীতভাবে, একটি কাস্টম সেটআপের মধ্যে খুব সহজেই unsupported dependency version গুলিতে আটকে যাওয়া সহজ, এবং আপনি মূলত আপনার নিজস্ব কাঠামো তৈরি করতে পারবেন—যদিও কোনো framework আপগ্রেড পথ নেই (এবং যদি এটি আরও এলোমেলোভাবে ডিজাইন করা আমাদের অতীতে তৈরি করা framework গুলির মতো কিছু হয়)।

আপনি যদি এখনও নিশ্চিত না হন, বা আপনার অ্যাপে অস্বাভাবিক সীমাবদ্ধতা থাকে যা এই framework গুলো দ্বারা ভালভাবে পরিবেশিত না হয় এবং আপনি আপনার নিজস্ব কাস্টম সেটআপ রোল করতে চান, আমরা আপনাকে থামাব না--এটির জন্য npm থেকে `react` এবং `react-dom` ইন্সটল করুন, [Vite](https://vitejs.dev/) or [Parcel](https://parceljs.org/) এর মতো একটি বান্ডলার দিয়ে আপনার কাস্টম বিল্ড প্রক্রিয়া সেট আপ করুন এবং রাউটিং, স্ট্যাটিক জেনারেশন বা সার্ভার-সাইড রেন্ডারিং এবং আরও অনেক কিছুর জন্য আপনার প্রয়োজন অনুযায়ী অন্যান্য টুল যোগ করুন।
</DeepDive>

## জনপ্রিয় React ফ্রেমওয়ার্ক গুলো {/*bleeding-edge-react-frameworks*/}

আমরা কীভাবে React এর উন্নতি চালিয়ে যেতে পারি তার খোঁজ করেছি , আমরা বুঝতে পেরেছি যে ফ্রেমওয়ার্কগুলির সাথে React কে আরও ঘনিষ্ঠভাবে একীভূত করা (বিশেষত, রাউটিং, বান্ডলিং এবং সার্ভার প্রযুক্তির সাথে) React ব্যবহারকারীদের আরও ভাল অ্যাপ তৈরি করতে সহায়তা করার সবচেয়ে বড় সুযোগ। Next.js টিম [React সার্ভার কম্পোনেন্টের](/blog/2023/03/22/react-labs-what-we-have-been-working-on-march-2023#react-server-components) মতো ফিচারের গবেষণা, বিকাশ, একীভূতকরণ এবং পরীক্ষা করতে আমাদের সাথে সহযোগিতা করতে সম্মত হয়েছে।

এই বৈশিষ্ট্যগুলি প্রতিদিন প্রস্তুত হওয়ার কাছাকাছি আসছে, এবং আমরা সেগুলিকে একীভূত করার বিষয়ে অন্যান্য বান্ডলার এবং ফ্রেমওয়ার্ক বিকাশকারীদের সাথে কথা বলেছি। আমাদের আশা যে এক বা দুই বছরের মধ্যে, এই পৃষ্ঠায় তালিকাভুক্ত সমস্ত কাঠামো এই বৈশিষ্ট্যগুলির জন্য সম্পূর্ণ সমর্থন পাবে৷ (আপনি যদি এই বৈশিষ্ট্যগুলির সাথে পরীক্ষা করার জন্য আমাদের সাথে অংশীদারি করতে আগ্রহী একজন ফ্রেমওয়ার্ক লেখক হন তবে দয়া করে আমাদের জানান!)

### Next.js (অ্যাপ রাউটার) {/*nextjs-app-router*/}

**[Next.js's অ্যাপ রাউটার](https://beta.nextjs.org/docs/getting-started) এটি Next.js API-এর একটি পুনঃডিজাইন যা React টিমের ফুল-স্ট্যাক আর্কিটেকচার ভিশন পূরণ করার লক্ষ্যে।** এটি আপনাকে asynchronous কম্পোনেন্ট গুলিতে ডেটা আনতে দেয় যা সার্ভারে বা এমনকি বিল্ড চলাকালীনও চলে।

[Vercel](https://vercel.com/) Next.js এর রক্ষণাবেক্ষণের কাজ করে থাকে। যেকোনো Node.js অথবা serverless হোস্টিং, অথবা আপনার নিজস্ব সার্ভারে [একটি Next.js অ্যাপ deploy](https://nextjs.org/docs/deployment) করতে পারবেন। Next.js [স্ট্যাটিক এক্সপোর্ট](https://beta.nextjs.org/docs/configuring/static-export) সমর্থন করে যার জন্য সার্ভারের প্রয়োজন হয় না।
<Pitfall>

Next.js-এর অ্যাপ রাউটার **বর্তমানে beta তে রয়েছে এবং এটি এখনও প্রোডাকশনের জন্য সাজেস্ট করা হয়নি** (মার্চ 2023 অনুযায়ী). একটি Next.js প্রোজেক্টে এটি নিয়ে পরীক্ষা করতে, [এই ক্রমবর্ধমান মাইগ্রেশন গাইড অনুসরণ করুন](https://beta.nextjs.org/docs/upgrade-guide#migrating-from-pages-to-app)।

</Pitfall>

<DeepDive>

#### কোন বৈশিষ্ট্যগুলি React টিমের ফুল-স্ট্যাক আর্কিটেকচার ভিশন তৈরি করে? {/*which-features-make-up-the-react-teams-full-stack-architecture-vision*/}

Next.js অ্যাপ রাউটার বান্ডলার অফিসিয়াল [React সার্ভার কম্পোনেন্ট](https://github.com/reactjs/rfcs/blob/main/text/0188-server-components.md) স্পেসিফিকেশন সম্পূর্ণরূপে প্রয়োগ করে। এটি আপনাকে একটি একক React বিল্ড-টাইম, শুধুমাত্র সার্ভার এবং ইন্টারেক্টিভ কম্পোনেন্ট গুলকে মিশ্রিত করতে দেয়।

উদাহরণস্বরূপ, আপনি একটি সার্ভার-অনলি React কম্পোনেন্টকে একটি `async` ফাংশন হিসেবে লিখতে পারেন যা কোনো ডাটাবেস বা কোনো ফাইল থেকে পড়ে। তারপরে আপনি এটি থেকে আপনার ইন্টারেক্টিভ উপাদানগুলিতে ডেটা প্রেরণ করতে পারেন:

```js
// This component runs *only* on the server (or during the build).
async function Talks({ confId }) {
  // 1. You're on the server, so you can talk to your data layer. API endpoint not required.
  const talks = await db.Talks.findAll({ confId });

  // 2. Add any amount of rendering logic. It won't make your JavaScript bundle larger.
  const videos = talks.map(talk => talk.video);

  // 3. Pass the data down to the components that will run in the browser.
  return <SearchableVideoList videos={videos} />;
}
```

Next.js's App Router also integrates [data fetching with Suspense](/blog/2022/03/29/react-v18#suspense-in-data-frameworks). This lets you specify a loading state (like a skeleton placeholder) for different parts of your user interface directly in your React tree:

```js
<Suspense fallback={<TalksLoading />}>
  <Talks confId={conf.id} />
</Suspense>
```

Server Components and Suspense are React features rather than Next.js features. However, adopting them at the framework level requires buy-in and non-trivial implementation work. At the moment, the Next.js App Router is the most complete implementation. The React team is working with bundler developers to make these features easier to implement in the next generation of frameworks.

</DeepDive>
