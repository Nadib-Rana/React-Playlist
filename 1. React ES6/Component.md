# **React Components**  

React-এর প্রধান দুটি কম্পোনেন্ট হল:  

### **1. Stateless Functional Component**  
- এটি একটি সাধারণ **ফাংশন**, যা **JSX রিটার্ন** করে।  
- **স্টেট নেই** (React Hooks আসার আগে)।  
- শুধুমাত্র **UI রেন্ডারিং** এর জন্য ব্যবহৃত হয়।  

🔹 **উদাহরণ:**  
```jsx
function Greeting(props) {
  return <h1>Hello, {props.name}!</h1>;
}
```

---

### **2. Stateful Class Component**  
- এটি একটি **ES6 ক্লাস**, যা `React.Component` এক্সটেন্ড করে।  
- **স্টেট ম্যানেজ** করতে `this.state` ব্যবহার করে।  
- **লাইফসাইকেল মেথড** (`componentDidMount`, ইত্যাদি) ব্যবহার করে।  

🔹 **উদাহরণ:**  
```jsx
class Counter extends React.Component {
  constructor() {
    super();
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + ১ });
  };

  render() {
    return (
      <div>
        <h1>Count: {this.state.count}</h1>
        <button onClick={this.increment}>Increase</button>
      </div>
    );
  }
}
```

👉 **আধুনিক React-এ ফাংশনাল কম্পোনেন্ট** + **Hooks (`useState`, `useEffect`)** বেশি ব্যবহৃত হয়। 
