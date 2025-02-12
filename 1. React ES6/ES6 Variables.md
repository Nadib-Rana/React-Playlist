Here’s a simplified note on **Variables in ReactJS** in Bengali:

---

### **ReactJS-এ ভেরিয়েবলস (Variables in ReactJS)**

 **JavaScript** এর মত React-এও ভেরিয়েবল তৈরি করা হয়।

#### **1. let, const, var:**
ReactJS-এ ভেরিয়েবল ডিক্লেয়ার করার জন্য তিনটি কিওয়ার্ড আছে:
- **let**: মান পরিবর্তন করা যাবে।
- **const**: একবার মান নির্ধারণের পর পরিবর্তন করা যাবে না।
- **var**: পুরানো পদ্ধতি, এখন এটির ব্যবহার কম।

**উদাহরণ:**
```javascript
let name = "Nadib";  // পরিবর্তনযোগ্য
const age = 25;      // পরিবর্তনযোগ্য নয়
```

#### **2. State as a Variable:**
React-এ `useState` হুক ব্যবহার করে স্টেট (State) ভেরিয়েবল তৈরি করা হয়। স্টেট ভেরিয়েবল UI পরিবর্তন করতে সহায়ক।

**উদাহরণ:**
```javascript
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0); // count হলো ভেরিয়েবল
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

#### **3. Props as a Variable:**
React কম্পোনেন্টে ডাটা পাঠানোর জন্য **props** ব্যবহার করা হয়। `props` একটি ভেরিয়েবল হিসেবে কাজ করে, যা এক কম্পোনেন্ট থেকে অন্য কম্পোনেন্টে ডাটা পাঠায়।

**উদাহরণ:**
```javascript
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>; // props.name একটি ভেরিয়েবল
}

function App() {
  return <Greeting name="Nadib" />;
}
```

#### **4. Variables in JSX:**
React-এ JSX এর মধ্যে JavaScript ভেরিয়েবল ব্যবহার করতে `{}` ব্যবহার করতে হয়।

**উদাহরণ:**
```javascript
const name = "Nadib";
const element = <h1>Hello, {name}!</h1>;
```

#### **5. Destructuring:**
React-এ object বা array থেকে ভেরিয়েবল বের করার জন্য **destructuring** ব্যবহার করা হয়। এটি কোড আরও পরিষ্কার এবং সহজ করে তোলে।

**উদাহরণ:**
```javascript
const person = { name: "Nadib", age: 25 };
const { name, age } = person; // name এবং age ভেরিয়েবল বের করা
```

---

