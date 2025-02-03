### React-এ ফর্ম এবং কন্ট্রোলড কম্পোনেন্টস

React-এ ফর্মের ইনপুট এলিমেন্ট যেমন `<input>`, `<textarea>`, এবং `<select>` কিছুটা আলাদা ভাবে কাজ করে। HTML-এ, ফর্ম এলিমেন্টগুলো নিজেই স্টেট (যেমন ইনপুট ভ্যালু) ম্যানেজ করে, কিন্তু React-এ, আমাদের কম্পোনেন্টের স্টেটে এই ভ্যালু ম্যানেজ করা হয়। React-এ এই ধরনের ইনপুট এলিমেন্টগুলোকে **কন্ট্রোলড কম্পোনেন্ট** বলা হয়। এখানে React স্টেটই ইনপুট ফিল্ডের একমাত্র "সোর্স অব ট্রুথ"।

### কন্ট্রোলড কম্পোনেন্টস:
React-এ **কন্ট্রোলড কম্পোনেন্ট** বলতে এমন একটি ফর্ম এলিমেন্ট বুঝানো হয়, যার মান React স্টেট দ্বারা নিয়ন্ত্রিত হয়। অর্থাৎ, আপনি ইনপুটের মান React স্টেটে রাখতে পারবেন, এবং যখনই ইনপুটে কিছু পরিবর্তন হবে, সেটি স্টেটে আপডেট হবে।

### উদাহরণ:

1. **Text Input (Name Form)**:
   ```jsx
   class NameForm extends React.Component {
     constructor(props) {
       super(props);
       this.state = { value: '' };
     }

     handleChange = (event) => {
       this.setState({ value: event.target.value });
     };

     handleSubmit = (event) => {
       alert('Name Submitted: ' + this.state.value);
       event.preventDefault();
     };

     render() {
       return (
         <form onSubmit={this.handleSubmit}>
           <label>
             Name:
             <input type="text" value={this.state.value} onChange={this.handleChange} />
           </label>
           <input type="submit" value="Submit" />
         </form>
       );
     }
   }
   ```

2. **Textarea**:
   ```jsx
   class EssayForm extends React.Component {
     constructor(props) {
       super(props);
       this.state = { value: 'Write about your favorite DOM element.' };
     }

     handleChange = (event) => {
       this.setState({ value: event.target.value });
     };

     handleSubmit = (event) => {
       alert('Essay Submitted: ' + this.state.value);
       event.preventDefault();
     };

     render() {
       return (
         <form onSubmit={this.handleSubmit}>
           <label>
             Essay:
             <textarea value={this.state.value} onChange={this.handleChange} />
           </label>
           <input type="submit" value="Submit" />
         </form>
       );
     }
   }
   ```

3. **Select Dropdown**:
   ```jsx
   class FlavorForm extends React.Component {
     constructor(props) {
       super(props);
       this.state = { value: 'coconut' };
     }

     handleChange = (event) => {
       this.setState({ value: event.target.value });
     };

     handleSubmit = (event) => {
       alert('Selected Flavor: ' + this.state.value);
       event.preventDefault();
     };

     render() {
       return (
         <form onSubmit={this.handleSubmit}>
           <label>
             Choose your favorite flavor:
             <select value={this.state.value} onChange={this.handleChange}>
               <option value="grapefruit">Grapefruit</option>
               <option value="lime">Lime</option>
               <option value="coconut">Coconut</option>
               <option value="mango">Mango</option>
             </select>
           </label>
           <input type="submit" value="Submit" />
         </form>
       );
     }
   }
   ```

### একাধিক ইনপুট হ্যান্ডলিং:
যদি একাধিক ইনপুট থাকে, তাহলে আমরা প্রতিটি ইনপুটে `name` অ্যাট্রিবিউট ব্যবহার করে একটি সাধারণ হ্যান্ডলার ফাংশন তৈরি করতে পারি।

```jsx
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2,
    };
  }

  handleInputChange = (event) => {
    const { name, type, value, checked } = event.target;
    this.setState({
      [name]: type === 'checkbox' ? checked : value,
    });
  };

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange}
          />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange}
          />
        </label>
      </form>
    );
  }
}
```

### কন্ট্রোলড ইনপুটে `null` ভ্যালু:
যদি `value` প্রপসে `null` বা `undefined` দেয়া হয়, তাহলে ইনপুটটি সম্পাদনাযোগ্য হবে না। 

### কন্ট্রোলড কম্পোনেন্টস-এর বিকল্প:
যদি অনেক ইনপুট হ্যান্ডল করা কঠিন মনে হয়, তাহলে **আনকন্ট্রোলড কম্পোনেন্টস** ব্যবহার করতে পারেন। এছাড়া, **Formik** বা অন্য লাইব্রেরি ব্যবহার করে ফর্মের ভ্যালিডেশন ও হ্যান্ডলিং আরও সহজ করতে পারেন।