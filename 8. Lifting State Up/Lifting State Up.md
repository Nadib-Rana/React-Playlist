React-এর "Lifting State Up" কনসেপ্টের উপর একটি পূর্ণাঙ্গ নোট:

### লিফটিং স্টেট আপ (Lifting State Up):
যখন একাধিক কম্পোনেন্টে একই ডেটার পরিবর্তন হওয়া দরকার, তখন সেই শেয়ারড স্টেটটি তাদের সবচেয়ে কাছের সাধারণ অ্যানসেস্টর কম্পোনেন্টে উঠিয়ে নেওয়া উচিত।

#### উদাহরণ:
একটি তাপমাত্রা ক্যালকুলেটর তৈরি করা হবে, যা তাপমাত্রা নির্ধারণ করবে এবং দেখাবে যে দেওয়া তাপমাত্রায় পানি ফুটবে কি না।

### 1. **BoilingVerdict কম্পোনেন্ট**:
এটি সেলসিয়াস তাপমাত্রা গ্রহণ করে এবং একটি প্যারাগ্রাফে দেখায় যে পানি ফুটবে কি না।
```javascript
function BoilingVerdict(props) {
  if (props.celsius >= 100) {
    return <p>The water would boil.</p>;
  }
  return <p>The water would not boil.</p>;
}
```

### 2. **Calculator কম্পোনেন্ট**:
এটি একটি ইনপুট ফিল্ড তৈরি করে যেখানে ব্যবহারকারী তাপমাত্রা প্রবেশ করবে এবং তার মান স্টেটে রাখবে। এই কম্পোনেন্টটি BoilingVerdict কম্পোনেন্ট রেন্ডার করবে বর্তমান ইনপুট তাপমাত্রা অনুযায়ী।
```javascript
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    return (
      <fieldset>
        <legend>Enter temperature in Celsius:</legend>
        <input
          value={temperature}
          onChange={this.handleChange} />
        <BoilingVerdict
          celsius={parseFloat(temperature)} />
      </fieldset>
    );
  }
}
```

### 3. **TemperatureInput কম্পোনেন্ট**:
এখন আমাদের নতুন প্রয়োজন হলো সেলসিয়াস ইনপুটের পাশাপাশি একটি ফারেনহাইট ইনপুটও রাখা, এবং এই দুটি ইনপুট সিঙ্ক্রোনাইজ রাখা।

আমরা Calculator কম্পোনেন্ট থেকে একটি নতুন `TemperatureInput` কম্পোনেন্ট তৈরি করব:
```javascript
class TemperatureInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.state = {temperature: ''};
  }

  handleChange(e) {
    this.setState({temperature: e.target.value});
  }

  render() {
    const temperature = this.state.temperature;
    const scale = this.props.scale;
    return (
      <fieldset>
        <legend>Enter temperature in {scaleNames[scale]}:</legend>
        <input value={temperature}
               onChange={this.handleChange} />
      </fieldset>
    );
  }
}
```

### 4. **তাপমাত্রার রূপান্তর ফাংশন**:
আমরা সেলসিয়াস থেকে ফারেনহাইট এবং ফারেনহাইট থেকে সেলসিয়াসে রূপান্তরের জন্য দুটি ফাংশন তৈরি করব:
```javascript
function toCelsius(fahrenheit) {
  return (fahrenheit - 32) * 5 / 9;
}

function toFahrenheit(celsius) {
  return (celsius * 9 / 5) + 32;
}
```

এছাড়াও একটি `tryConvert` ফাংশন থাকবে যা তাপমাত্রা রূপান্তর করবে:
```javascript
function tryConvert(temperature, convert) {
  const input = parseFloat(temperature);
  if (Number.isNaN(input)) {
    return '';
  }
  const output = convert(input);
  const rounded = Math.round(output * 1000) / 1000;
  return rounded.toString();
}
```

### 5. **State Lifting**:
এখন আমাদের `TemperatureInput` কম্পোনেন্টে স্থানীয় স্টেট রাখা যাবে না, কারণ আমরা তাদের একে অপরের সাথে সিঙ্ক্রোনাইজ করতে চাই। আমরা এই স্টেটটি `Calculator` কম্পোনেন্টে স্থানান্তর করব। এটি হবে "source of truth" (সত্যের উৎস)।
- `Calculator` কম্পোনেন্টের মধ্যে তাপমাত্রা এবং স্কেল স্টেট রাখা হবে।
- `TemperatureInput` কম্পোনেন্টগুলি এই স্টেট থেকে তাপমাত্রা গ্রহণ করবে এবং `onTemperatureChange` প্রপের মাধ্যমে স্টেট আপডেট করবে।

### 6. **Calculator কম্পোনেন্ট**:
```javascript
class Calculator extends React.Component {
  constructor(props) {
    super(props);
    this.handleCelsiusChange = this.handleCelsiusChange.bind(this);
    this.handleFahrenheitChange = this.handleFahrenheitChange.bind(this);
    this.state = {temperature: '', scale: 'c'};
  }

  handleCelsiusChange(temperature) {
    this.setState({scale: 'c', temperature});
  }

  handleFahrenheitChange(temperature) {
    this.setState({scale: 'f', temperature});
  }

  render() {
    const scale = this.state.scale;
    const temperature = this.state.temperature;
    const celsius = scale === 'f' ? tryConvert(temperature, toCelsius) : temperature;
    const fahrenheit = scale === 'c' ? tryConvert(temperature, toFahrenheit) : temperature;

    return (
      <div>
        <TemperatureInput
          scale="c"
          temperature={celsius}
          onTemperatureChange={this.handleCelsiusChange} />
        <TemperatureInput
          scale="f"
          temperature={fahrenheit}
          onTemperatureChange={this.handleFahrenheitChange} />
        <BoilingVerdict
          celsius={parseFloat(celsius)} />
      </div>
    );
  }
}
```

### 7. **শেষ কথা**:
React-এ স্টেট শেয়ারিংয়ের ক্ষেত্রে সর্বদা একটি "সূত্রের সত্য" থাকতে হবে। যখন একটি স্টেট অন্য কম্পোনেন্টে ব্যবহার করা প্রয়োজন, তখন আমরা সেটি উপরের কম্পোনেন্টে লিফট করি। এর মাধ্যমে একটি পরিষ্কার এবং কার্যকরী ডেটা প্রবাহ নিশ্চিত হয়, যেখানে সবকিছু এককভাবে পরিচালিত হয়।

### 8. **লেসনস লার্নড**:
- স্টেটের জন্য একটি একক উৎস (single source of truth) থাকা উচিত।
- React-এ ডেটা প্রবাহ থাকে উপরের দিক থেকে নিচে (top-down), তাই স্টেটটি কম্পোনেন্টের কাছে থেকে তার অ্যানসেস্টরে পাঠাতে হবে।
- একাধিক ইনপুট সিঙ্ক্রোনাইজ করার জন্য লিফটিং স্টেট পদ্ধতি ব্যবহার করতে হবে।

এভাবে React-এ স্টেট ব্যবস্থাপনা করা যায় এবং যে কোনো সমস্যা বা বাগ খুঁজে বের করা সহজ হয়।