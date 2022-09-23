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

