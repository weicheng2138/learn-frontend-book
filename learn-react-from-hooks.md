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

## React Hooks!!!

### useState

{% hint style="info" %}
Demo is here

[https://codepen.io/weicheng2138/pen/MWoYdNg?editors=1011](https://codepen.io/weicheng2138/pen/MWoYdNg?editors=1011)
{% endhint %}

* At the beginning we adjust the variable **count** in the Counter component. It didn't render when you change the value.
* If you something like **useState**, it should be a **Hook**. Because the prefix _**use**_ of the term.
* Every Component with JSX can have only **one root** **node**.
* Normally when you heard about state in React, it should be considered as **data**.

```bash
// dig out useState from React
const { useState } = React;

// state it in React Component
const [count, setCount] = useState('initial data');

// change the state by using setCount in React Component
return (
    <div onClick={() => {setCount(count + 1)}}/>
)
```

```bash
// dig out useState in two ways
React.useState(); 
const { useState } = React;
```

### inline-style in JSX

* `display: none` **occupation** will disappear and mess up
* `visibility: hidden` occupation still alive

```bash
// two types of inline-style
// when count is true return 'hidden'
style={{
    visibility: count >= 10 && 'hidden',
}}

// when count is true return true (css get true and do nothing)
style={{
    visibility: count >= 10 || 'hidden',
}}

// ternary operator
style={
    (count <= 0) ? {visibility: 'hidden'}:{}
}
```

```bash
className="chevron chevron-up"
className={`chevron chevron-up ${count >= 10 && 'visibility-hidden'}`}
```

```bash
// If you want the element cannot be seen in 
// devtool you can use the way below
{count < 10 && (
  <div
    className="chevron chevron-up"
    onClick={() => {
      setCount(count + 1);
    }}
  />
)}
```

### Handle Event

* `onClick={function}`the function position should be a function not calling the function. We expect to call it when we click it, but it turn to be called while it's rendering. An infinite loop of **rendering -&gt; handleClick called -&gt; setCount called**.

{% hint style="danger" %}
`onClick={handleClick('increment')}`
{% endhint %}

{% hint style="success" %}
`onClick={() => handleClick('increment')}`
{% endhint %}

{% hint style="success" %}
`onClick={handleClick} // without parameter`
{% endhint %}

* Advanced approach makes you to make error example to work.

```bash
// Original
const handleClick = (type) => {
  return function() {
    if (type === 'increment') {
      setCount(count + 1);
    }
    if (type === 'decrement') {
      setCount(count - 1);
    }
  };
};

// Simplified
const handleClick = type => () =>
    setCount(type === 'increment' ? count + 1 : count - 1);
```

{% hint style="success" %}
`onClick={handleClick('increment')}`
{% endhint %}

### Map for Looping Components

```bash
// [undefined, undefined, ..., undefined]
Array.from({ length: 10 });

// [0, 1, 2, ..., 8, 9]
Array.from({ length: 10 }, (_, index) => index)
```

```bash
const counters = Array.from({ length: 14 }, (_, index) => index);

// In JSX
{
    counters.map((item) => (<Counter />))
}
```

### Speed Converter

{% hint style="info" %}
[https://codepen.io/weicheng2138/pen/xxrGxGR?editors=0011](https://codepen.io/weicheng2138/pen/xxrGxGR?editors=0011)
{% endhint %}

```bash
// in React Component
const handleInputChange = (e) => {
  const {value} = e.target;
  setInputValue(value);
};

// in JSX
<input type="number" className="input-number" min="0"                
onChange={handleInputChange} value={inputValue}/>
```

### Props for CardFooter

```bash
const CardFooter = (props) => {
  const { inputValue } = props;

  // ...
  return (
    {/* ... */ }
  );
};

// in SpeedConverter
<CardFooter inputValue={inputValue} />
```

{% hint style="danger" %}
**Never** use Hook method \(useState useEffect...\) in condition, loop and nested functions. But you can use the data and function from useState. Normally, the render process call those React Components, React Hooks record the calling order of those hooks. If you put it in condition, the order will be in echos.
{% endhint %}

### CSS-in-JS \(styled-components/_**emotion**_\)

{% hint style="info" %}
[https://codesandbox.io/s/jovial-firefly-twwr8?file=/src/WeatherApp.js](https://codesandbox.io/s/jovial-firefly-twwr8?file=/src/WeatherApp.js)
{% endhint %}

```bash
import React from "react";
import styled from '@emotion/styled';

const Container = styled.div`
  background-color: #ededed;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
`;

const WeatherCard = styled.div`
  position: relative;
  min-width: 360px;
  box-shadow: 0 1px 3px 0 #999999;
  background-color: #f9f9f9;
  box-sizing: border-box;
  padding: 30px 15px;
`;

const WeatherApp = () => {
  return(
    <Container>
      <WeatherCard>
        <h1>Weather</h1>
      </WeatherCard>
    </Container>
  );
};

export default WeatherApp;
```

* class name of each component will come with a unique name. `css-ncsjdcn`

```bash
// great for manipulate svg animation and directly use Cloudy in JSX
import { ReactComponent as Cloudy } from './images/cloudy.svg';

// great for normal image with static using
import cloudyIcon from './images/cloudy.svg';
// in JSX
<img src={cloudyIcon} alt="cloudy icon" />
```

```bash
// You can make component by style-component
// You can also create Comp then add style
const Cloudy = styled(CloudyIcon)`
  flex-basis: 30%;
`;
```

```bash
// bring props in styled-components
// in JSX
<Location theme="dark">台北市</Location>

// in styled-components
const Location = styled.div`
  ${props => console.log(props)}
  font-size: 28px;
  color: ${props => props.theme === 'dark' ? '#dadada' : '#212121'};
  margin-bottom: 20px;
`;
```

{% hint style="warning" %}
You can not comment `${props => console.log(props)}` in Location component. It works for css element.
{% endhint %}

```bash
// pre-define some template style-component and reuse it
// props also can be used
import { css } from '@emotion/core';

const buttonDefault = (props) => css`
  display: block;
  width: 120px;
  height: 30px;
  font-size: 14px;
  background-color: transparent;
  color: ${props.theme === 'dark' ? '#dadada' : '#212121'};
`;

const rejectButton = styled.button`
  ${buttonDefault}
  background-color: red;
`

const acceptButton = styled.button`
  ${buttonDefault}
  background-color: green;
`
```

* Get the weather data from [https://opendata.cwb.gov.tw/user/authkey](https://opendata.cwb.gov.tw/user/authkey) and api url from [https://opendata.cwb.gov.tw/dist/opendata-swagger.html](https://opendata.cwb.gov.tw/dist/opendata-swagger.html). And use fetch to get the data from those apis.
* When you try to modify an attribute or some attributes in state object, follow below... 

{% hint style="danger" %}
`setCurrentWeather({ temperature: 31, });`

`console.log(currentWeather); // object left only temp attr`
{% endhint %}

{% hint style="success" %}
`setCurrentWeather({ ...currentWeather, temperature: 31, })`

`console.log(currentWeather); // reserve all attr of an object`
{% endhint %}

### useEffect \(**side-effect**\)

| invoke function component -&gt; | render -&gt; | execute function in useEffect |
| :--- | :--- | :--- |
| beginning of the component | JSX | `useEffect()` |

* Will be called either `setSomething()` is called or the first load. Or you can say that it will be called after **rendering**.
* Mutations, subscriptions, timers, logging, and other **side effects** are not allowed inside the main body of a function component.

```bash
 // [dependencies] is put to avoid infinite loop of calling
 // setSomething and setEffect. Only call setEffect when
 // dependencies is mutated. [] -> only the first time
 useEffect(() => {
    console.log('execute function in useEffect');
    fetchCurrentWeather();
 }, [dependencies]);
```

{% hint style="danger" %}
After rendering, useEffect will be called as long as dependencies are mutated
{% endhint %}

```bash
// setSomething can preserve the preState
useEffect(() => {
    console.log('execute function in useEffect');
    fetchCurrentWeather();
    fetchWeatherForecast();
}, []);

const fetchCurrentWeather = () =>
    
    setWeatherElement((preState) => ({
        ...preState,
        observationTime: locationData.time.obsTime,
        ...
    }));
}

const fetchWeatherForecast= () =>
    
    setWeatherElement((preState) => ({
        ...preState,
        description: weatherElements.Wx.parameterName,
        ...
    }));
}

// in JSX
<Redo onClick={() => {
    fetchCurrentWeather();
    fetchWeatherForecast();
}} />
```

```bash
// make fetchData to be public use in useEffect and JSX
const fetchData = async () => {
  const [currentWeather, weatherForecast] = await Promise.all([
    fetchCurrentWeather(),
    fetchWeatherForecast(),
  ]);
  
  setWeatherElement({
    ...currentWeather,
    ...weatherForecast,
  });
};

// in useEffect
useEffect(() => {
  console.log('execute function in useEffect');
  fetchData();
}, []);

// in JSX
<Redo onClick={fetchData} />
```

{% hint style="warning" %}
After do things above... Eslint output error...

_React Hook useEffect has a missing dependency: 'fetchData'. Either include it or remove the dependency array. \(react-hooks/exhaustive-deps\)_
{% endhint %}

* Before that eslint problem, fetchData is defined and only used in useEffect. However, we take it out and make it public, problem pops out.

