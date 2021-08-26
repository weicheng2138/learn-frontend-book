# Learn React from Hooks

## Basics

### Template literals／Template strings

```bash
console.log(`The ${favoritePhone} is ${currentPrice} now.`);
```

### Arrow Functions

```bash
const showIphonePrice = (currentPrice) => {
  return `The iPhone is ${currentPrice} now.`;
};
```

### Shorthand Property Names

{% tabs %}
{% tab title="Original" %}
```bash
const deviceName = 'Galaxy Note';
const currentPrice = 30900;
const storage = '256G';

const galaxyNote = {
  deviceName: deviceName,
  currentPrice: currentPrice,
  storage: storage,
};

console.log(galaxyNote.deviceName); // Galaxy Note
```
{% endtab %}

{% tab title="Shorthand" %}
```bash
const deviceName = 'Galaxy Note';
const currentPrice = 30900;
const storage = '256G';

const galaxyNote = {
  deviceName,
  currentPrice,
  storage,
};

console.log(galaxyNote.deviceName);   // Galaxy Note
```
{% endtab %}
{% endtabs %}

### Destructuring Assignment

{% tabs %}
{% tab title="Object" %}
```bash
const product = {
  name: 'iPhone',
  image: 'https://i.imgur.com/b3qRKiI.jpg',
  aggregateRating: {
    ratingValue: '4.6',
    reviewCount: '120',
  },
  offers: {
    priceCurrency: 'TWD',
    price: '26,900',
  },
};

const { name, image } = product;
```
{% endtab %}

{% tab title="Array" %}
```bash
const mobileBrands = [
  'Samsung', 'Apple', 'Huawei', 'Oppo',
  'Vivo', 'Xiaomi', 'LG', 'Lenovo', 'ZTE'
];

const [best, second, third] = mobileBrands;
```
{% endtab %}
{% endtabs %}

### Spread Syntax/Rest Syntax

{% tabs %}
{% tab title="Spread" %}
```bash
const mobilePhone = {
  name: 'mobile phone',
  publishedYear: '2019',
};

const iPhone = {
  ...mobilePhone,
  name: 'iPhone',
  os: 'iOS',
};
```
{% endtab %}

{% tab title="Rest" %}
```bash
const product = {
  name: 'iPhone',
  image: 'https://i.imgur.com/b3qRKiI.jpg',
  brand: {
    name: 'Apple',
  },
  aggregateRating: {
    ratingValue: '4.6',
    reviewCount: '120',
  },
  offers: {
    priceCurrency: 'TWD',
    price: '26,900',
  },
};

const { name, image, ...other } = product;
console.log(other); // { brand, aggregateRating...}
```
{% endtab %}
{% endtabs %}

## Why JSX?

{% hint style="info" %}
Do the practice first to feel the reason why

[https://codepen.io/weicheng2138/pen/LYLEoxp?editors=1011](https://codepen.io/weicheng2138/pen/LYLEoxp?editors=1011)
{% endhint %}

When we are manipulating the DOM in pure JS, we need to do the query select from the DOM and do what you want in JS. But JSX offers a way to deal with the DOM selecting in JS. **Babel**, **React** and **ReactDOM** are required.

* `class` for DOM class List should be `className` in JSX.
* inline-style in JSX should be `<div style={someStyle}`

{% tabs %}
{% tab title="Variable" %}
```bash
const Counter = (
  <div className="container" style={shadow}>
    <div className="chevron chevron-up"></div>
    <div className="number">256</div>
    <div className="chevron chevron-down"></div>
  </div>
);

ReactDOM.render(Counter,document.getElementById('root'));
```
{% endtab %}

{% tab title="React Component" %}
```bash
// you may have variable in Component
const Counter = () => {
  const variable = [];
  return (
    <div className="container">
      <div className="chevron chevron-up" />
      <div className="number">256</div>
      <div className="chevron chevron-down" />
    </div>
  );
};

ReactDOM.render(<Counter />,document.getElementById('root'));
```
{% endtab %}

{% tab title="React Component \(pure jsx\)" %}
```
// Simplified with () and no return
const Counter = () => (
  <div className="container">
    <div className="chevron chevron-up" />
    <div className="number">256</div>
    <div className="chevron chevron-down" />
  </div>
);

ReactDOM.render(<Counter />,document.getElementById('root'));
```
{% endtab %}
{% endtabs %}

* React Component should be in **capital form** in JSX. If it's not, it will be treated as a normal html tag.
* Attributes should be in **Pascal Case**.

## React Hooks!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

{% hint style="info" %}
Demo is here

[https://codepen.io/weicheng2138/pen/MWoYdNg?editors=1011](https://codepen.io/weicheng2138/pen/MWoYdNg?editors=1011)
{% endhint %}

* At the beginning we adjust the variable **count** in the Counter component. It didn't render when you change the value.
* If you something like **useState**, it should be a **Hook**. Because the prefix _**use**_ of the term.
* Every Component with JSX can have only **one root** **node**.
* Normally when you heard about state in React, it should be considered as **data**.

