# **Keyword Differences Between HTML & JSX**  

| **বৈশিষ্ট্য**  | **HTML** 🟢 | **JSX (React)** 🔵 |
|--------------|------------|----------------|
| **Class Attribute** | `class="container"` | `className="container"` |
| **Inline Styles** | `style="color: red;"` | `style={{ color: "red" }}` (Double Curly Braces) |
| **Self-Closing Tags** | `<img src="image.jpg">` | `<img src="image.jpg" />` (Self-closing Required) |
| **Event Handling** | `onclick="handleClick()"` | `onClick={handleClick}` (CamelCase, Function Reference) |
| **For Attribute** | `<label for="name">Name</label>` | `<label htmlFor="name">Name</label>` |
| **JavaScript Code Injection** | সরাসরি লেখা যায় না | `{}` এর মধ্যে JavaScript ব্যবহার করা যায় |

---

### **HTML উদাহরণ:**  
```html
<div class="box" onclick="handleClick()" style="color: red;">
  Hello, World!
</div>
```

### **JSX উদাহরণ:**  
```jsx
<div className="box" onClick={handleClick} style={{ color: "red" }}>
  Hello, World!
</div>
```
