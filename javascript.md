---
description: JS Basics
---

# 🤯 Javascript

## Lexical Environment

Where did you write your code?&#x20;

### Scope

We have Global Ex. Context (e.g. window) and Function Ex. Context (When we call a function).&#x20;

#### Function Scope

Variable as `var` is defined in function scope and can be notice in hello function. <mark style="color:yellow;">ES5</mark><mark style="color:green;">.</mark>

```javascript
var globalText = 'global'
function hello() {
    var localText = 'local'
}
console.log(globalText) // global
console.log(localText) // Uncaught ReferenceError: localText is not defined
```

#### Block Scope

Due to <mark style="color:yellow;">ES6</mark> of **const** and **let**, we can define our scope by <mark style="color:yellow;">{}</mark>. `if,` `while` and `for` are all have its scope.

```javascript
/** error */
try {
    var foo = 'foo'
} catch(error) {
    console.log(error)
}
console.log(foo)
console.log(error) // Uncaught ReferenceError

/** var, let and const */
let condition = true
function bar() {
    if(condition) {
        var nameOne = 'one'
        let nameTwo = 'two'
        const nameThree = 'three'
    }
    console.log(nameOne)
    console.log(nameTwo) // Uncaught ReferenceError
    console.log(nameThree) // Uncaught ReferenceError
}
bar()
```

#### Scope Chain

```javascript
const globalVariable = 'global text'
function layerOne() {
    const layerOneVar = 'one'
    console.log(globalVariable) // global text
    
    function layerThree() {
        const layerThreeVar = 'three'
        console.log(layerOneVar) // one
        console.log(globalVariable) // global text
        layerTwo()
    }
    layerThree()
}

function layerTwo() {
    console.log(globalVariable) // global text
    console.log(layerThreeVar) // Uncaught ReferenceError
}

layerOne()
```

List all external lexical enviroment for each function. **As you see that layerTwo can not reach layerThree's variable.**

* layerOne -> Global Ex. Context
* layerThree -> layerOne -> Global Ex. Context
* layerTwo -> Global Ex. Context

## Hoisting

```javascript
c3po() 
console.log(greeting) // undefined

var greeting = 'hello , master.'
function c3po () {
  console.log('c-3po has been called!')
} 
```

V8 Engine will do two things after Global Ex. Context is generated

1. Generate global object <mark style="color:yellow;">`window`</mark>
2. Generate <mark style="color:yellow;">`this`</mark> object
3. Reserve memory space for the variable you are going to use which is still assigned to be `undefined`
4. Reserve memory space for function (normal declare function) and write it into memory

Where we store in memory space is called <mark style="color:yellow;">Global Memory</mark> or <mark style="color:yellow;">Heap.</mark>

{% hint style="info" %}
Above all is call creating stage. And what we are doing in this stage for reserving memory space for variable and function is called <mark style="color:yellow;">**Hoisting**</mark>
{% endhint %}

{% hint style="warning" %}
let and const do happen hoisting but only for reserving memory space. Only when you actually assigned the value, the variable can be used.
{% endhint %}

## Statement & Expression

* Statement: it won't return any value (e.g. if, while, switch) and variable declaration.
* Expression: it returns a value (e.g. 1+1, 2===3)

### Function Statement

Normal function and fully hoisting.

```javascript
function functionStatement (){
	//doSomething 
} 
```

### Function Expression

Function won't be hoisting. Only variable is hoisting.

```javascript
var functionExpression = function(){
	//doSomeThing
}
```

## Closures

```javascript
/** numA is being conculde in closure in addB function
 *  numA is temporarily kept in memory by addB function
 */
let country = 'United Nations'
let soilder = ['Clone' , 'Clone' , 'Warship', 'Clone']; 
let jedi = ['Yoda' , 'Obi-Wan', 'Anakin']

function addA(numA){
	return function (numB){
		return numA+numB
	} 
} 
let addB = addA(jedi.length)
let fellowNum = addB(soilder.length) 

/** When we push func into array variable i is kept by the pushFuncToArray to form
 *  a closure and keep the value of i.
 *  However, when we call the func in array, the value of i is 3. Because i do keep
 *  in memory by closure but the have already increase to 3.
 */
function pushFuncToArray(){
    var funcArr = [] 
    for (var i=0; i<3; i++){
        funcArr.push(function(){
            console.log(i)
        }) 
    } 
    return funcArr
} 
var functionArr = pushFuncToArray()
functionArr[0]()
functionArr[1]()
functionArr[2]()
```

## Object Type and Primitive Type

```javascript
let hello = function(){
	console.log('hello') 
} 
console.log(typeof hello) // function
console.log( hello instanceof Object) // true
```

```javascript
const a = {};
const symbol1 = Symbol('123');
const symbol2 = Symbol('123'); // they have different memory address in JS 
console.log(typeof symbol1); // expected output: "symbol"

a.symbol1 = 'Hello!';
a[symbol1] // undefined
a['symbol1'] // "Hello!"
```

## Event Queue, Event Loop and Event Table

### JavaScript Engine

V8 Engine consist of Global Ex. Context, Execution Stack and Global Memery (heap)

### JS Runtime Environment ( JRE )

Browser is not only consist of JS engine, it contains something like event listener, timer and other third party apis. Basicly JRE is construct by below.&#x20;

#### Web Api

Web api like `setTimeout` is not part of JS Engine, they are browser offered api. Background executed and asynchronous.

* Api for DOM manipulation -> `document.getElementById`
* Api which related to AJAX -> `XMLHttpRequest`
* Api for timer -> `setTimeout, setInterval`

#### Event Queue

First in first out. After web api is finished its callback or waiting time, the function will be put into event queue and wait for to be put into stack.

```javascript
function executeAfterDelay() {
  console.log("I will be printed after 1000 milliseconds")
}

setTimeout(executeAfterDelay, 1000)
console.log("I will be executed first")
for(let i=0; i<10000; i++){ // if for loop is more than 5s, executeAfterDelay need
                            // to wait for it whenever the count down is finished 
                            // or not.
  console.log('@')
}
```

1. `setTimeout` is called
2. JS Engine keep executing the code below `setTimeout`. setTimeout is counting down.
3. When count down is over, put the function (`executeAfterDelay`) into event queue.
4. After JS Engine finish the `console.log` and for loop, event queue start to push tasks into stack and execute.

#### Event Table

A mapping table for web apis. Those apis will be put into this table before being put into event queue.

#### Event Loop

It's more like to be a watcher which is always watching at stack and event queue. And it also help the process to push event between stack and queue.

## Promise

A Promise is an object representing the eventual completion or failure of an asynchronous operation.
