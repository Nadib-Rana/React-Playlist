Here’s a note on ES6 Functions in Bengali:

---

### **ES6 ফাংশন (Functions)**
ES6-এর দুটি গুরুত্বপূর্ণ ফাংশন ফিচার হল 
-- **Arrow Functions** এবং 
-- **Default Parameters**।
#### **1. Arrow Functions (এ্যারো ফাংশন):**
এ্যারো ফাংশন একটি সংক্ষিপ্ত পদ্ধতিতে ফাংশন লেখার পদ্ধতি। এর সাহায্যে `function` কীওয়ার্ডের পরিবর্তে `=>` সিম্বল ব্যবহার করা হয়।

**সাধারণ ফাংশন:**
```javascript
function sum(a, b) {
  return a + b;
}
```

**এ্যারো ফাংশন:**
```javascript
const sum = (a, b) => a + b;
```

- এ্যারো ফাংশনে `return` কিওয়ার্ডও সহজভাবে লেখা যায় যদি ফাংশন এক লাইনেই রিটার্ন করে।

**উদাহরণ:**
```javascript
const greet = name => `Hello, ${name}!`;
console.log(greet("Nadib")); // Output: Hello, Nadib!
```

#### **2. Default Parameter :**
ES6-এ ফাংশনের প্যারামিটারগুলোর জন্য Default মান সেট করা সম্ভব। যদি কোন  Parameter প্রদান না করা হয়, তবে Default মানটি ব্যবহার হবে।

**উদাহরণ:**
```javascript
function greet(name = "Guest") {
  console.log(`Hello, ${name}!`);
}

greet("Nadib");  // Output: Hello, Nadib!
greet();         // Output: Hello, Guest!
```

#### **3. Rest Parameters (রেস্ট প্যারামিটার):**
এটি এমন একটি ফিচার যা একটি ফাংশনের মধ্যে অজস্র আর্গুমেন্ট গ্রহণ করতে সাহায্য করে এবং এগুলিকে একটি অ্যারে হিসেবে রিটার্ন করে।

**উদাহরণ:**
```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4));  // Output: 10
```

#### **4. Spread Syntax (স্প্রেড সিনট্যাক্স):**
স্প্রেড সিনট্যাক্সের মাধ্যমে একটি অ্যারে বা অবজেক্টের সব উপাদানকে আলাদাভাবে ব্যবহার করা যায়।

**উদাহরণ:**
```javascript
const numbers = [1, 2, 3];
const newNumbers = [...numbers, 4, 5];
console.log(newNumbers); // Output: [1, 2, 3, 4, 5]
```

#### **5. Function Expressions (ফাংশন এক্সপ্রেশন):**
এটি একটি ফাংশন ডিফাইন করার একটি পদ্ধতি যেখানে ফাংশনটি একটি ভ্যারিয়েবল হিসেবে সংরক্ষিত থাকে।

**উদাহরণ:**
```javascript
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(2, 3));  // Output: 6
```

#### **ফাংশন লেখার সুবিধা:**
- কোডের দৈর্ঘ্য কম হয়।
- কোড আরও সোজা ও পরিষ্কার হয়।
- ফাংশনের মধ্যে ডিফল্ট মান এবং আর্গুমেন্ট গুলি সহজে ব্যবহার করা যায়।

---
