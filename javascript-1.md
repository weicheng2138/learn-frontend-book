# Javascript ES6

### Destructuring Assignment

```javascript
// 陣列的解構賦值
let [a, b] = [1, 2];

console.log(a); // 1
console.log(b); // 2

// 物件的解構賦值
const { attr1: x, attr2: y } = { attr1: 10, attr2: 20 };

console.log(x); // 10
console.log(y); // 20

// 物件的屬性也能解構賦值
const { admin, user } = { admin: 'a', user: 'b' };

console.log(admin); // 'a'
console.log(user);  // 'b'

// 字串的解構賦值
let [x, y] = 'Hi';
console.log(x, y); // 'H', 'i'

// Set 資料結構
let [x, y, z] = new Set([10, 20, 30]);
console.log(x, y, z); // 10, 20, 30

// 交換變數的值 
let a = 1, b = 10;

[a, b] = [b, a];
console.log(a); // 10
console.log(b); // 1

```

### for…of

```javascript
let arr = ['a', 'b', 'c', 'd'];

// for...in 取得 "鍵名/屬性名"
for (let key in arr) {
    console.log(key); // '0' '1' '2' '3'
}

// for...of 取得 "鍵值/屬性值"
for (let value of arr) {
    console.log(value); // 'a' 'b' 'c' 'd'
}

// 使用在字串上
let string = 'Hello';

for (let i of string) {
    console.log(i); // 'H' 'e' 'l' 'l' 'o'
}

// Get key and value simultaneously
for (let [key, value] of arr.entries()) {
    console.log(key, value);
}

// 內層為陣列類型時
let arr = [
    [1, 2, 3],
    [4, 5, 6],
    ['Hello', 'world']
];

for (let [x, y, z] of arr) {
    console.log(x, y, z);
}
// 1, 2, 3
// 4, 5, 6
// 'Hello', 'world', undefined

// 內層為物件類型時
let family = [
    {name: 'ES6', type: 'JavaScript'},
    {name: 'for', type: 'Iterator'}
];

for (let {name, type} of family) {
    console.log(name + ': ' + type);
}
```

### Spread Operator

```javascript
// copy an array
let a1 = [1, 2];
let a2 = [...a1];

// merge two arrays
let a1 = ['Hello', 'world'];
let a2 = [1, 2, 3];
a2 = [...a2, ...a1];

// string split into array, equals to str.split('')
let text = [...'Hello'];

// copy and merge object
let obj1 = { name: 'foo', x: 10 };
let obj2 = { name: 'test', y: 20 };
let clonedObj = { ...obj1 };

// if obj1 and obj2 have same property, the last one will be considered
const mergedObj = { ...obj1, ...obj2 };

// push 
let list = [1, 2];
list.push(...[3, 4]);
list.push.apply(list, [3, 4]); // same as below
console.log(list); // [1, 2, 3, 4]

```

### Default Parameter

```javascript
// 函數中的預設參數
function multiply(a, b = 1) {
    return console.log(a * b);
}
// 等同於
function multiply(a, b) {
    b = (typeof b !== 'undefined') ?  b : 1;
    return console.log(a * b);
}
multiply(10, 2); // 20
multiply(10); // 10

// 放入 undefined 與 null 的差別
function foo(x = 5, y = 10) {
    console.log(x, y);
}
foo(undefined, null); // 5 null
```

### Rest Parameter

When you use `...` as parameter, that is an opposite meaning to Spread Operator.

```javascript
// 函數中的 Rest 參數
function foo(...rest) {
    return console.log(rest);
}
// 等同於
function foo() {
    return console.log(Array.prototype.slice.call(arguments));
}
foo(); // []
foo(10, 20, 30); // [10, 20, 30]

function foo(a, ...b, c) {}
// SyntaxError: Rest parameter must be last formal parameter

// 使用在解構賦值上
// 將兩個陣列合併後再做排序大小，最後取出第一個值
let spread1 = [5, 2, 8];
let spread2 = [6, 1, 3];

let [first, ...rest] = [...spread1, ...spread2].sort();

console.log(first); // 1 
console.log(rest); // [2, 3, 5, 6, 8]
```

### Arrow Function

```javascript
// 使用 addEventListener 監聽事件
var button = document.querySelector('button');
var fn_arrow = () => {
  // 建立 function 時 this 指向 Window
    console.log(this.constructor.name);  // 執行 function 時 this 指向 Window
};
var fn = function(){
  // 建立 function 時 this 指向 Window
    console.log(this.constructor.name);  // 執行 function 時 this 指向 HTMLButtonElement
};

button.addEventListener('click', fn_arrow);
button.addEventListener('click', fn);
```

### Syntactic sugar

```javascript
// 對物件直接寫入變數和函數，省略了許多關鍵詞
let birth = '2018/01/01';
let person = {
    name: '老王',

    // 等同於 birth: birth
    birth,

    // 等同於 sayHello: function() {...}
    sayHello() { 
        console.log('My name is '+ this.name + ' ' + this.birth);
    }
};
```

### Symbol

This function always returns a **unique** symbol value. Even the value key is the same. Normally use it as constant value for the function.

```javascript
let s1 = Symbol('s1');
let s2 = Symbol('s2');
let s3 = Symbol('s2');

console.log(s3 === s2) // false

const obj = {
    [s1]: 'Hello',
    [s2]: 'World'
};

for (let key in obj) {
    console.log(key); // 無輸出
}

let propertyNames = Object.getOwnPropertyNames(obj);
console.log(propertyNames); // []


let propertySymbols = Object.getOwnPropertySymbols(obj);
console.log(propertySymbols); // [ Symbol(s1), Symbol(s2) ]
```

### Map (HashMap)

Key of map can not be duplicated.

{% hint style="warning" %}
**Ordering** of array is better than map.
{% endhint %}

```javascript
let myMap = new Map([
  [1, 'one'],
  [2, 'two'],
]);

myMap.set(keyFunc, 'value associated with function');

// 方法
myMap.has(keyString); // true，透過 .has 判斷該 Map 中是否有某一屬性
myMap.size; //  3，透過 .size 來取得 Map 內的屬性數目
myMap.get(keyString); // 使用 .get(key) 可取得屬性的內容
myMap.delete(keyString); // 刪除 Map 中的某個屬性，成功刪除回傳 true，否則 false
myMap.clear(); // 清空整個 Map


/** Clone map */
let students = {
  Aaron: { age: '29', country: 'Taiwan' },
  Jack: { age: '26', country: 'USA' },
  Johnson: { age: '32', country: 'Korea' },
};

const studentMap = new Map(Object.entries(students));
const cloneMap = new Map(studentMap);

cloneMap.get('Aaron'); // { age: '29', country: 'Taiwan' }
studentMap === cloneMap; // false. Useful for shallow comparison

/** Making hashtable */
const arr = ['apple', 'apple', 'banana', 'banana', 'cat', 'dog', 'fat', 'fat', 'fat', 'fat'];

const hashTable = new Map();

arr.forEach((item) => {
  if (hashTable.has(item)) {
    hashTable.set(item, hashTable.get(item) + 1);
  } else {
    hashTable.set(item, 1);
  }
});

// Map { 'apple' => 2, 'banana' => 2, 'cat' => 1, 'dog' => 1, 'fat' => 4 }
console.log(hashTable);
```

### Module System

```javascript
export const obj = {a: 1};
export function foo() {
    console.log('function test');
}

// 使用大括號 "{}" 做統一輸出
let str = 'Hello';

let foo = function() {
    console.log('function test');
}

// 也能使用 as 重新命名
export {str, foo as fooTest};
import {str, fooTest} from './myModule.js';

import * as module from './myModule.js';

console.log(module.str); 
console.log(module.obj);


// Export default
function circleArea(r) {
    return console.log('area: ', r * r * 3.14);
}
export default circleArea;
// --------------------------------------------
// 檔名: import.js
import getArea from './export.js';

getArea(10); // area: 100
```

### Set

```javascript
let set = new Set();

// 可以使用 add() 方法設置資料內容
set.add(10);
set.add(10);
set.add('text');
set.add({sayHi: 'Hi'});

console.log(set);
// Set(4) {10, "text", {sayHi: "Hi"}}
```

### Proxy

{% hint style="info" %}
**Vue3** is using `Proxy` object with getter and setter to fulfill reactive data. Vue3 didn't change the object value but proxy.\
\
Also using **Reflect** object to get and set proxy data.
{% endhint %}

{% hint style="info" %}
**Vue2** fulfill the same thing by directly manipulating object data in terms of `Object.defineProperty` with getter and setter.
{% endhint %}

```javascript
// 這是基本語法
var proxy = new Proxy(target, handler);

// 此用來攔截變數的 "物件內容"，改變它的原始行為 
var proxy = new Proxy({}, {
    get: function(target, propKey, receiver) {
        return 'getting';
    },
    set: function(target, propKey, value, receiver) {
        console.log('setting');
    }
});

console.log(proxy.test);  // 'getting' 
console.log(proxy.other); // 'getting' 

// 以下都會執行 console.log('setting');
proxy.abc = 10; 
proxy[10] = 'test'; 

// won't make set happen
proxy.test.abc = 0
```

### Promise

```javascript
// 宣告 promise 建構式
let newPromise = new Promise((resolve, reject) => {
  // 傳入 resolve 與 reject，表示資料成功與失敗
  let ran = parseInt(Math.random() * 2); // 隨機成功或失敗
  console.log('Promise 開始')
  if (ran) {
    setTimeout(function(){
      // 3 秒時間後，透過 resolve 來表示完成
      resolve('3 秒時間(fulfilled)');
    }, 3000);
  } else {
    // 回傳失敗
    reject('失敗中的失敗(rejected)')
  }

});

newPromise.then((data)=> {
  // 成功訊息 (需要 3 秒)
  console.log(data);
}).catch((err)=> {
  // 失敗訊息 (立即)
  console.log(err)
});
```
