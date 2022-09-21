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
