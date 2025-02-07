**JavaScript & React Destructuring (জাভাস্ক্রিপ্ট ও রিয়্যাক্ট ডিস্ট্রাকচারিং)**

Destructuring হলো JavaScript-এর একটি feature যা array থেকে মান বা object-এর property আলাদা variable-এ নির্দিষ্টভাবে বের করতে সাহায্য করে। এটি কোডকে আরও সহজপাঠ্য এবং কার্যকর করে তোলে। ReactJS-এ এটি props এবং state থেকে ডাটা সহজভাবে এক্সট্রাক্ট করতে ব্যবহৃত হয়।

---

### **Array Destructuring (অ্যারে ডিস্ট্রাকচারিং)**  
Index ব্যবহার করে উপাদান access করার পরিবর্তে, destructuring সরাসরি variable-এ assign করে।

#### **Example (উদাহরণ):**
```javascript
const sandwich = ['bread', 'lettuce', 'tomato', 'cheese', 'mayo'];

// নির্দিষ্ট উপাদান বের করা
const [bread, , tomato, cheese] = sandwich;

console.log(bread);  // "bread"
console.log(tomato); // "tomato"
console.log(cheese); // "cheese"
```
(*Note: কমা `,` ব্যবহার করে "lettuce" বাদ দেওয়া হয়েছে।*)

---

### **Object Destructuring (অবজেক্ট ডিস্ট্রাকচারিং)**  
Destructuring object থেকে সরাসরি property বের করতে সাহায্য করে।

#### **Example (উদাহরণ):**
```javascript
const ingredients = {
  bread: 'whole grain',
  spread: 'mayo',
  protein: 'chicken',
  veggie: 'lettuce'
};

// শুধুমাত্র প্রয়োজনীয় মান বের করা
const { bread, protein } = ingredients;

console.log(bread);   // "whole grain"
console.log(protein); // "chicken"
```
এটি বারবার `ingredients.bread` এর মতো access এড়িয়ে যায়।

---

### **Destructuring with Default Values (ডিস্ট্রাকচারিং-এ ডিফল্ট মান)**
যদি কোনো মান `undefined` হয়, তবে একটি default value নির্ধারণ করা যেতে পারে।

#### **Example (উদাহরণ):**
```javascript
const { sauce = 'ketchup' } = {};
console.log(sauce); // "ketchup"
```

---

### **Variable Renaming (ভ্যারিয়েবল পুনঃনামকরণ)**
`:` ব্যবহার করে property-এর নতুন নাম নির্ধারণ করা যায়।

#### **Example (উদাহরণ):**
```javascript
const { protein: meat } = ingredients;
console.log(meat); // "chicken"
```

---

### **Destructuring in Function Parameters (ফাংশনের প্যারামিটারে ডিস্ট্রাকচারিং)**
Function-এর parameter-এও সরাসরি destructuring ব্যবহার করা যায়।

#### **Example (উদাহরণ):**
```javascript
function makeSandwich({ bread, protein }) {
  return `আপনার ${bread} এবং ${protein} দিয়ে তৈরি sandwich প্রস্তুত!`;
}

console.log(makeSandwich(ingredients)); // "আপনার whole grain এবং chicken দিয়ে তৈরি sandwich প্রস্তুত!"
```

---

### **Destructuring in ReactJS (ReactJS-এ ডিস্ট্রাকচারিং)**
ReactJS-এ destructuring props ও state থেকে data সহজে বের করতে ব্যবহার করা হয়।

#### **Props Destructuring (Props থেকে ডাটা বের করা)**
```javascript
const Welcome = ({ name, age }) => {
  return <h1>Welcome {name}, Age: {age}</h1>;
};

// Component ব্যবহার
<Welcome name="Nadib" age={25} />;
```

#### **State Destructuring (State থেকে ডাটা বের করা)**
```javascript
import { useState } from 'react';

const Counter = () => {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
};
```
এখানে `useState` থেকে `count` এবং `setCount` destructure করা হয়েছে।

---

