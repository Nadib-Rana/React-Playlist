Here’s a simplified note on **Ternary Operator in ReactJS** in Bengali:

---

### **ReactJS-এ Ternary Operator (Ternary Operator in ReactJS)**

Ternary Operator হল একটি শর্তাধীন এক্সপ্রেশন যা **if-else** স্টেটমেন্টের বিকল্প। এটি এক লাইনে শর্ত যাচাই করে দুটি ভিন্ন মান রিটার্ন করতে ব্যবহৃত হয়।

**সিনট্যাক্স:**
```javascript
condition ? expressionIfTrue : expressionIfFalse;
```

#### **1. Ternary Operator ব্যবহার:**

ReactJS-এ `ternary operator` UI এর মধ্যে শর্ত যাচাই করার জন্য ব্যবহার করা হয়।

**উদাহরণ:**
```javascript
function Greeting(props) {
  return (
    <h1>{props.isLoggedIn ? "Welcome Back!" : "Please Sign Up"}</h1>
  );
}
```

এখানে, যদি `props.isLoggedIn` সঠিক হয়, তবে "Welcome Back!" দেখানো হবে। অন্যথায়, "Please Sign Up" দেখানো হবে।

#### **2. Multiple Conditions:**

একাধিক শর্ত যাচাই করতে `ternary operator` চেইন করা যেতে পারে।

**উদাহরণ:**
```javascript
function UserStatus(props) {
  return (
    <h1>
      {props.isLoggedIn ? "Welcome Back!" : props.isAdmin ? "Admin" : "Guest"}
    </h1>
  );
}
```

এখানে, প্রথম শর্ত চেক করা হয়, যদি সেটি না মেলে তবে দ্বিতীয় শর্ত চেক করা হয়, তারপর তৃতীয় শর্ত।

#### **3. JSX-এ Ternary Operator:**

React JSX-এ `ternary operator` ব্যবহার করে শর্ত অনুযায়ী UI পরিবর্তন করা যায়।

**উদাহরণ:**
```javascript
function App(props) {
  return (
    <div>
      {props.isOnline ? <p>User is online</p> : <p>User is offline</p>}
    </div>
  );
}
```

#### **4. Shorthand for Conditional Rendering:**

Ternary operator অনেক সময় **conditional rendering** বা **inline if** হিসেবে ব্যবহৃত হয়।

**উদাহরণ:**
```javascript
function DisplayMessage(props) {
  return <h1>{props.isLoggedIn ? "Hello, User!" : "Please Log In"}</h1>;
}
```

---

