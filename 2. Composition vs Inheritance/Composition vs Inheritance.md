### **React-এ Composition vs Inheritance**

React-এ কোড পুনঃব্যবহারের জন্য **composition** ব্যবহার করা হয়, **inheritance** না। চলুন দুটো ধারণা দেখিঃ

---

### **1. Containment:**

কিছু কম্পোনেন্ট তাদের চিলড্রেন (children) আগে থেকে জানে না। যেমন **Sidebar** বা **Dialog** কম্পোনেন্টগুলি সাধারণত generic “বক্স” হিসেবে ব্যবহৃত হয়। এই ধরনের ক্ষেত্রে, React একটি বিশেষ `children` prop প্রদান করে, যা অন্য কম্পোনেন্টগুলিকে তাদের চিলড্রেন সরাসরি কম্পোনেন্টে পাঠাতে দেয়।

#### উদাহরণ: `FancyBorder` কম্পোনেন্ট
```javascript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

#### `WelcomeDialog` কম্পোনেন্টে ব্যবহার:
```javascript
function WelcomeDialog() {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">Welcome</h1>
      <p className="Dialog-message">Thank you for visiting our spacecraft!</p>
    </FancyBorder>
  );
}
```
এখানে, `<FancyBorder>` ট্যাগের ভিতরের যে কিছু থাকবে, তা `children` prop হিসেবে পাঠানো হবে এবং `FancyBorder` কম্পোনেন্টে `{props.children}` রেন্ডার করার মাধ্যমে প্রদর্শিত হবে।

### **2. একাধিক "Hole" (স্থান) থাকতে পারে:**

কখনও কখনও আপনাকে এমন কম্পোনেন্ট তৈরি করতে হতে পারে যেগুলির একাধিক স্থান (holes) থাকে, যেখানে আপনি কনটেন্ট বসাতে পারেন। এখানে আপনি নিজেই custom props ব্যবহার করতে পারেন।

#### উদাহরণ: `SplitPane` কম্পোনেন্ট:
```javascript
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={<Contacts />}
      right={<Chat />} />
  );
}
```
এখানে, `left` এবং `right` হচ্ছে custom props, যার মাধ্যমে আপনি বিভিন্ন কম্পোনেন্ট বা কনটেন্ট `SplitPane` কম্পোনেন্টে পাঠাতে পারেন।

---

### **3. Specialization:**

কখনও কখনও আমরা একটি কম্পোনেন্টকে আরেকটি কম্পোনেন্টের বিশেষ সংস্করণ হিসেবে চিন্তা করি। React-এ এটি **composition** এর মাধ্যমে করা হয়। যেখানে একটি বিশেষ কম্পোনেন্ট একটি সাধারণ কম্পোনেন্টকে রেন্ডার করে এবং তাকে props দিয়ে কাস্টমাইজ করে।

#### উদাহরণ: `Dialog` কম্পোনেন্ট
```javascript
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">{props.title}</h1>
      <p className="Dialog-message">{props.message}</p>
    </FancyBorder>
  );
}

function WelcomeDialog() {
  return (
    <Dialog title="Welcome" message="Thank you for visiting our spacecraft!" />
  );
}
```

এখানে, `WelcomeDialog` একটি বিশেষ সংস্করণ, যা `Dialog` কম্পোনেন্টে নতুন `title` এবং `message` prop পাঠাচ্ছে।

#### ক্লাস কম্পোনেন্টের উদাহরণ:
```javascript
class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.state = { login: '' };
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
  }

  render() {
    return (
      <Dialog title="Mars Exploration Program" message="How should we refer to you?">
        <input value={this.state.login} onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>Sign Me Up!</button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({ login: e.target.value });
  }

  handleSignUp() {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
}
```
এখানে, `SignUpDialog` কম্পোনেন্ট `Dialog` এর একটি বিশেষ সংস্করণ, যা কিছু অতিরিক্ত ফর্ম ফিল্ড এবং বাটন যোগ করেছে।

---

### **তাহলে Inheritance কী?**

Facebook-এ React এর মাধ্যমে হাজার হাজার কম্পোনেন্ট ব্যবহৃত হয়, এবং এখানে **component inheritance hierarchies** তৈরি করার কোনো প্রয়োজন হয়নি। **composition** এবং **props** দিয়ে React কম্পোনেন্টের মধ্যে ফ্লেক্সিবিলিটি এবং কাস্টমাইজেশন করা যায়, যা অনেক বেশি সেফ এবং মানানসই।

আপনি যদি **non-UI functionality** পুনঃব্যবহার করতে চান, তাহলে সেটি একটি আলাদা JavaScript module এ নিয়ে যান। কম্পোনেন্টগুলো সেই module কে import করে ব্যবহার করতে পারে, কিন্তু inheritance দিয়ে নয়।

---

### **মুল টিপস:**
- React-এ কোড পুনঃব্যবহারের জন্য **composition** বেশি সুবিধাজনক।
- **Containment** এর মাধ্যমে কম্পোনেন্ট অন্য কম্পোনেন্টে চিলড্রেন পাঠাতে পারে।
- **Specialization** এর মাধ্যমে একটি কম্পোনেন্ট অন্য কম্পোনেন্টের বিশেষ সংস্করণ হতে পারে।
- React-এ **inheritance** ব্যবহারের প্রয়োজন নেই, **composition** অনেক বেশি ফ্লেক্সিবল এবং মেইনটেইনেবল।
