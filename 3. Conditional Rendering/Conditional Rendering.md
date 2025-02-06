### **React Conditional Rendering (বাংলা)**  

React-এ কন্ডিশনাল রেন্ডারিং করতে আমরা আলাদা আলাদা কম্পোনেন্ট তৈরি করতে পারি এবং অ্যাপ্লিকেশনের স্টেট অনুযায়ী নির্দিষ্ট কম্পোনেন্ট রেন্ডার করতে পারি। এটি মূলত JavaScript এর শর্তানুযায়ী কাজ করে।  

---

## **🔹 শর্তানুযায়ী রেন্ডারিং করার উপায়**  

### **1️⃣ `if` শর্ত ব্যবহার করে রেন্ডারিং**  
আমরা `if` শর্ত ব্যবহার করে আলাদা কম্পোনেন্ট রেন্ডার করতে পারি।  

```jsx
function UserGreeting() {
  return <h1>আপনাকে স্বাগতম!</h1>;
}

function GuestGreeting() {
  return <h1>অনুগ্রহ করে লগইন করুন।</h1>;
}

function Greeting(props) {
  if (props.isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Greeting isLoggedIn={false} />);
```
✅ এখানে `isLoggedIn` প্রপসের মান যদি `true` হয়, তাহলে `UserGreeting` রেন্ডার হবে, নাহলে `GuestGreeting` রেন্ডার হবে।  

---

### **2️⃣ এলিমেন্ট ভেরিয়েবল ব্যবহার করা**  
এলিমেন্ট ভেরিয়েবল ব্যবহার করে আমরা শর্তানুযায়ী নির্দিষ্ট অংশ পরিবর্তন করতে পারি।  

```jsx
function LoginButton(props) {
  return <button onClick={props.onClick}> Login </button>;
}

function LogoutButton(props) {
  return <button onClick={props.onClick}>LogOut</button>;
}

class LoginControl extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isLoggedIn: false };
  }

  handleLoginClick = () => {
    this.setState({ isLoggedIn: true });
  };

  handleLogoutClick = () => {
    this.setState({ isLoggedIn: false });
  };

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button = isLoggedIn ? (
      <LogoutButton onClick={this.handleLogoutClick} />
    ) : (
      <LoginButton onClick={this.handleLoginClick} />
    );

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<LoginControl />);
```
✅ এখানে ব্যবহারকারী লগইন বা লগআউট বাটন ক্লিক করলে তার স্টেট পরিবর্তিত হবে এবং ভিন্ন UI উপস্থাপন করবে।  

---

### **3️⃣ `&&` লজিকাল অপারেটর দিয়ে ইনলাইন রেন্ডারিং**  
আমরা `&&` অপারেটর ব্যবহার করে কিছু কন্ডিশন পূরণ হলে কেবলমাত্র নির্দিষ্ট অংশ রেন্ডার করতে পারি।  

```jsx
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>হ্যালো!</h1>
      {unreadMessages.length > 0 && <h2>আপনার {unreadMessages.length} টি নতুন বার্তা আছে।</h2>}
    </div>
  );
}

const messages = ["React", "Re: React", "Re:Re: React"];
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Mailbox unreadMessages={messages} />);
```
✅ এখানে `unreadMessages` যদি খালি না হয়, তাহলে বার্তা দেখাবে, নাহলে কিছুই দেখাবে না।  

---

### **4️⃣ `? :` টার্নারি অপারেটর ব্যবহার করা**  
আমরা `? :` অপারেটর ব্যবহার করে সহজেই শর্তানুযায়ী ইনলাইন রেন্ডারিং করতে পারি।  

```jsx
class UserStatus extends React.Component {
  constructor(props) {
    super(props);
    this.state = { isLoggedIn: false };
  }

  render() {
    return (
      <div>
        <p>ব্যবহারকারী {this.state.isLoggedIn ? "প্রবেশ করেছেন" : "প্রবেশ করেননি"}।</p>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<UserStatus />);
```
✅ এখানে `isLoggedIn` স্টেট পরিবর্তন হলে টেক্সট আপডেট হবে।  

---

### **5️⃣ কম্পোনেন্ট হাইড করা (null ফেরত দেওয়া)**  
কখনও কখনও আমরা চাই, কোনো কম্পোনেন্ট কোনো শর্ত পূরণ না হলে একদমই রেন্ডার না হোক। এজন্য `null` ফেরত দিতে পারি।  

```jsx
function WarningBanner(props) {
  if (!props.warn) {
    return null;
  }
  return <div className="warning">সতর্কতা!</div>;
}

class Page extends React.Component {
  constructor(props) {
    super(props);
    this.state = { showWarning: true };
  }

  toggleWarning = () => {
    this.setState((state) => ({ showWarning: !state.showWarning }));
  };

  render() {
    return (
      <div>
        <WarningBanner warn={this.state.showWarning} />
        <button onClick={this.toggleWarning}>
          {this.state.showWarning ? "লুকান" : "দেখান"}
        </button>
      </div>
    );
  }
}

const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(<Page />);
```
✅ এখানে `showWarning` স্টেট `false` হলে `<WarningBanner />` একদমই রেন্ডার হবে না।  

---

## **✨ উপসংহার**  
✅ **React-এ কন্ডিশনাল রেন্ডারিং করার জন্য বিভিন্ন পদ্ধতি রয়েছে:**  
✔️ `if` শর্ত ব্যবহার  
✔️ এলিমেন্ট ভেরিয়েবল  
✔️ `&&` লজিকাল অপারেটর  
✔️ `? :` টার্নারি অপারেটর  
✔️ `null` ফেরত দিয়ে কম্পোনেন্ট হাইড করা  

