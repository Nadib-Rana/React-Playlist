
---

### **ES6 ক্লাস (Classes)**
ES6 (ECMAScript 2015) থেকে JavaScript-এ Classes এর সুবিধা যুক্ত করা হয়েছে। এটি OOP স্টাইলে কোড লেখার জন্য একটি নতুন এবং সহজ পদ্ধতি প্রদান করে। ক্লাসের মাধ্যমে আমরা নতুন অবজেক্ট তৈরি করতে পারি এবং তাদের মধ্যে ফাংশন (methods) যুক্ত করতে পারি।

#### **Basic Syntax:**
```javascript
class ClassName {
  constructor(parameters) {
    // constructor function (object creation time)
  }

  methodName() {
    // method (function inside class)
  }
}
```

- `class`: ক্লাস ডিফাইন করার জন্য ব্যবহার করা হয়।
- `constructor`: ক্লাসের ইনস্ট্যান্স (object) তৈরির সময় কল হওয়া বিশেষ ফাংশন।
- `method`: ক্লাসের মধ্যে থাকা সাধারণ ফাংশন।

#### **উদাহরণ (Example):**
```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old.`);
  }
}

const person1 = new Person("Nadib", 25);
person1.greet();  // Output: Hello, my name is Nadib and I am 25 years old.
```

#### **Class Inheritance:**
ES6 ক্লাস inheritance সমর্থন করে, যার মাধ্যমে একটি ক্লাস অন্য ক্লাসের বৈশিষ্ট্য ও মেথড নিতে পারে।

```javascript
class Student extends Person {
  constructor(name, age, course) {
    super(name, age);  // Parent class constructor
    this.course = course;
  }

  introduce() {
    console.log(`I am a student of ${this.course}.`);
  }
}

const student1 = new Student("Rana", 22, "Computer Science");
student1.greet();  // Output: Hello, my name is Rana and I am 22 years old.
student1.introduce();  // Output: I am a student of Computer Science.
```

#### **ক্লাসের বৈশিষ্ট্য:**
1. **এনক্যাপসুলেশন (Encapsulation)**: ক্লাসের মাধ্যমে ডেটা এবং মেথড একত্রে রাখা যায়।
2. **ইনহেরিট্যান্স (Inheritance)**: এক ক্লাসের বৈশিষ্ট্য অন্য ক্লাসে ব্যবহার করা যায়।
3. **পলিমরফিজম (Polymorphism)**: এক ধরনের মেথড বিভিন্নভাবে ব্যবহার করা যেতে পারে।

#### **ক্লাসের সুবিধা:**
- ক্লাসের মাধ্যমে কোড আরও সহজ ও পরিষ্কার হয়।
- অবজেক্টের পদ্ধতি (methods) এবং বৈশিষ্ট্য (properties) একসাথে রাখা যায়।

---

