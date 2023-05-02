---
title: এডিটর সেটাপ
---

<Intro>

সঠিকভাবে কনফিগার করা এডিটর আপনার কোড পড়ায় এবং লেখায় সাহায্য করতে পারে। এমনকি আপনাকে লিখার সাথে সাথে ভুলত্রুটি ধরায়ও সাহায্য করতে পারে! আপনি যদি প্রথমবারের মত এডিটর সেটাপ করেন অথবা আপনার বর্তমান এডিটরকে আরও সমৃদ্ধ করে তুলতে চান, তাহলে আমাদের কিছু পরামর্শ রয়েছে।

</Intro>

<YouWillLearn>

* সবচেয়ে জনপ্রিয় এডিটরগুলো কি কি
* কিভাবে আপনার কোড স্বয়ংক্রিয়ভাবেই ফরম্যাট করবেন

</YouWillLearn>

## আপনার এডিটর {/*your-editor*/}

[VS Code](https://code.visualstudio.com/) বর্তমানে ব্যবহৃত সবচেয়ে জনপ্রিয় এডিটরগুলোর মধ্যে একটি। এর মধ্যে বিশাল এক্সটেনশন মার্কেটপ্লেস রয়েছে এবং এটি সহজেই GitHub এর মত জনপ্রিয় সার্ভিসগুলোর সাথে সংযুক্ত হতে পারে। নিম্নোক্ত অধিকাংশ জিনিসই VS Code এ এক্সটেনশন হিসেবে যুক্ত করা যায়, যা একে আরও বেশি কনফিগার করতে সহায়তা করে।

React কমিউনিটিতে ব্যবহৃত অন্য জনপ্রিয় এডিটরগুলোঃ

* [WebStorm](https://www.jetbrains.com/webstorm/) জাভাস্ক্রিপ্টের জন্য তৈরি একটি integrated development environment।
* [Sublime Text](https://www.sublimetext.com/) - এ JSX এবং TypeScript সাপোর্টের পাশাপাশি, [সিনট্যাক্স হাইলাইটিং](https://stackoverflow.com/a/70960574/458193) এবং অটোকমপ্লিট সাপোর্ট রয়েছে।
* [Vim](https://www.vim.org/) একটি অধিক কনফিগারযোগ্য টেক্সট এডিটর যা সহজে যেকোন ধরণের টেক্সট ফাইল তৈরি এবং পরিবর্তন করতে বানানো হয়েছে। অধিকাংশ UNIX সিস্টেম এবং Apple OS X এর সাথে এটি "vi" হিসেবে দেয়া থাকে।

## প্রস্তাবিত টেক্সট এডিটরের বৈশিষ্ট্যসমূহ {/*recommended-text-editor-features*/}

কিছু এডিটরে এই বৈশিষ্ট্যগুলো ইতিমধ্যে সংযুক্ত করা থাকে, কিন্তু অন্যগুলোতে এক্সটেনশন যুক্ত করার প্রয়োজন পড়তে পারে। নিশ্চিত হওয়ার জন্য আপনার পছন্দের এডিটর কি সাপোর্ট সরবরাহ করে তা দেখে নিন!

### লিন্টিং {/*linting*/}

কোড লিন্টার আপনি কোড লিখার সাথে সাথে আপনাকে বিভিন্ন সমস্যা ধরতে এবং তা তাড়াতাড়ি সমাধান করতে সাহায্য করে। [ESLint](https://eslint.org/) জাভাস্ক্রিপ্টের একটি জনপ্রিয়, ওপেন-সোর্স লিন্টার। 

* [React এর জন্য প্রস্তাবিত কনফিগারেশন সহ ESLint ইন্সটল করুন](https://www.npmjs.com/package/eslint-config-react-app) (নিশ্চিত করুন আপনার [Node ইন্সটল করা রয়েছে!](https://nodejs.org/en/download/current/))
* [অফিশিয়াল এক্সটেনশনের সাহায্যে VSCode এ ESLint সংযুক্ত করুন](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

**নিশ্চিত করুন আপনি [`eslint-plugin-react-hooks`](https://www.npmjs.com/package/eslint-plugin-react-hooks) এর সকল রুলগুলো আপনার প্রজেক্টের জন্য enable করেছেন।** এগুলো অপরিহার্য এবং গুরুতর বাগ গুলো তাড়াতাড়ি ধরতে পারে। প্রস্তাবিত [`eslint-config-react-app`](https://www.npmjs.com/package/eslint-config-react-app) প্রিসেট এ এগুলো ইতিমধ্যে সংযুক্ত থাকে।

### ফরম্যাটিং {/*formatting*/}

অন্য কন্ট্রিবিউটরদের সাথে আপনার কোড শেয়ার করার সময় আপনি নিশ্চয়ই চাননা [tabs বনাম spaces](https://www.google.com/search?q=tabs+vs+spaces) নিয়ে কোন বিতর্কে জড়াতে! সৌভাগ্যক্রমে, [Prettier](https://prettier.io/) আপনার কোডকে নির্দিষ্ট প্রিসেট এবং রুল অনুযায়ী রি-ফরম্যাট করতে পারে। Prettier রান করুন, এবং আপনার সকল tab space এ পরিবর্তন হয়ে যাবে—এবং আপনার indentation, quotes, ইত্যাদি ও কনফিগারেশন অনুযায়ী পরিবর্তন হয়ে যাবে। আদর্শ সেটাপে, আপনি যখনই আপনার ফাইল সেইভ করবেন Prettier রান হবে, যাতে এই পরিমার্জনা গুলো দ্রুতগতিতে সম্পন্ন হয়।

আপনি নিচের ধাপগুলো অনুসরণ করে [VSCode -এ Prettier এক্সটেনশন](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) ইন্সটল করতে পারেনঃ

1. VS Code ওপেন করুন
2. Quick Open ব্যবহার করুন (Ctrl/Cmd+P চাপুন)
3. `ext install esbenp.prettier-vscode` - পেস্ট করুন
4. Enter চাপুন

#### সেইভে ফরম্যাট করা {/*formatting-on-save*/}

আদর্শভাবে, প্রতি সেইভেই আপনার কোডকে ফরম্যাট করা উচিত। VS Code এ এর সেটিং রয়েছে!

1. VS Code এ, `CTRL/CMD + SHIFT + P` প্রেস করুন।
2. "settings" টাইপ করুন
3. Enter চাপুন
4. সার্চ বারে, "format on save" টাইপ করুন
5. "format on save" অপশনটি টিক দেয়া আছে কিনা নিশ্চিত হয়ে নিন!

> আপনার ESLint প্রিসেটে যদি ফরম্যাটিং রুল থেকে থাকে, তাহলে তা Prettier এর সাথে conflict করতে পারে। আমরা পরামর্শ দেব আপনি যাতে আপনার ESLint প্রিসেটের সকল ফরম্যাটিং রুল [`eslint-config-prettier`](https://github.com/prettier/eslint-config-prettier) এর মাধ্যমে নিষ্ক্রিয় করে দেন যাতে ESLint *শুধুমাত্র* যৌক্তিক ভুল ধরার কাজে ব্যবহৃত হয়। আপনি যদি কোন pull request মার্জ করার আগে নিশ্চিত করতে চান আপনার ফাইলগুলো সঠিকভাবে ফরম্যাট করা হয়ে, তাহলে আপনার continuous integration এ [`prettier --check`](https://prettier.io/docs/en/cli.html#--check) ব্যবহার করুন।
