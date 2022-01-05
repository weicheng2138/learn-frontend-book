---
description: A solution to deal with async problem.
---

# RxJS

### Problems that you may encounter

* Race Condition (ex. Call an api many times. Then you won't know who is callback first)
* Memory Leak (ex. Often happens in SPA. We use js router to do the paging. But if you change page a to b and you forget to remove the scroll event listener)
* Complex State (Assume that we have an service which is pay to use. Then we need to get the service info and auth the user. After that the user may click start then stop. All of these states are changed rapidly)
* Exception Handling

### Different kind of APIs

* DOM Events
* XMLHttpRequest
* fetch
* Websockets
* Server Send Events
* Node Stream
* Timer

### Functional Programming and Reactive Programming

#### Reactive Programming (RP)

* Vue.js is the demo framework for this style
* Programmers focus on <mark style="color:red;">the event after the data changed</mark> instead of how to inform or update the data.

#### Functional Programming (FP)

* <mark style="color:red;">arr.slice (pure function)</mark> v.s. arr.splice
* No side effect
* Expression, no Statement: running a function and return something. It won't directly give an value to a variable.
* Pure function: the function will always return the same result whatever your parameter is.

### Observable

#### Observer Pattern

* Register an event. When the event is initiated, it will automatically handle it, Ex. DOM object.

#### Iterator Pattern

* Iterator is a pointer. It point to the element that can be generated to a sequence.
* Iterator is evantually a sequence, then we can utilize functionality, such as, map and filter.

```javascript
var arr = [1, 2, 3];

var iterator = arr[Symbol.iterator]();

iterator.next();
// { value: 1, done: false }
iterator.next();
// { value: 2, done: false }
iterator.next();
// { value: 3, done: false }
iterator.next();
// { value: undefined, done: true }
```

* **Lazy evaluation (**call-by-need**)** is a proper way of implementing it in tremendous data structure. We define a generator `getNumbers.` The generator will return a iterator. When we call the generator function  getNumbers, it didn't complete evaluating the logic in generator. It only process it while we are calling `.next()`.

```javascript
function* getNumbers(words) {
	for (let word of words) {
		if (/^[0-9]+$/.test(word)) {
			yield parseInt(word, 10);
		}
	}
}
	
const iterator = getNumbers('30 天精通 RxJS (04)');
	
iterator.next();
// { value: 3, done: false }
iterator.next();
// { value: 0, done: false }
iterator.next();
// { value: 0, done: false }
iterator.next();
// { value: 4, done: false }
iterator.next();
// { value: undefined, done: true }vvv
```

#### Observable

After Observer Pattern and Iterator Pattern, we can talk about Observable. Both of these patterns have something in common, it is **progressively processing data.** Differences are that Observer is <mark style="color:red;">pushing</mark> data as a <mark style="color:red;">Producer</mark> and Iterator is <mark style="color:red;">pulling</mark> data as a <mark style="color:red;">Consumer</mark>.

![from https://ithelp.ithome.com.tw/articles/10186832](.gitbook/assets/push\_pull.png)

### RxJS

RxJS contains one core (<mark style="color:orange;">Observable</mark>) and three critical points.

* <mark style="color:orange;">Observer</mark>
* <mark style="color:orange;">Subject</mark>
* <mark style="color:orange;">Schedulers</mark>

{% hint style="info" %}
[redux-observable](https://github.com/redux-observable/redux-observable) is implemented with the concept of Subject
{% endhint %}

#### <mark style="color:orange;">Observable</mark>

* Observable can be dealt with async and sync problem.

```javascript
var observable = Rx.Observable
	.create(function(observer) {
		observer.next('Jerry'); // RxJS 4.x 以前的版本用 onNext
		observer.next('Anna');
	})
	
console.log('start');
observable.subscribe(function(value) {
	console.log(value);
});
console.log('end');

// start
// Jerry
// Anna
// end

// NOT
// start
// end
// Jerry
// Anna
```

```javascript
var observable = Rx.Observable
	.create(function(observer) {
		observer.next('Jerry'); // RxJS 4.x 以前的版本用 onNext
		observer.next('Anna');
		
		setTimeout(() => {
			observer.next('RxJS 30 days!');
		}, 30)
	})
	
console.log('start');
observable.subscribe(function(value) {
	console.log(value);
});
console.log('end');

// start
// Jerry
// Anna
// end
// RxJS 30 days!
```

* Observer is an object with three functions.&#x20;

```javascript
var observable = Rx.Observable
	.create(function(observer) {
			observer.next('Jerry');
			observer.next('Anna');
			observer.complete();
			observer.next('not work');
	})
	
// 宣告一個觀察者，具備 next, error, complete 三個方法
var observer = {
	next: function(value) {
		console.log(value);
	},
	error: function(error) {
		console.log(error)
	},
	complete: function() {
		console.log('complete')
	}
}

// 用我們定義好的觀察者，來訂閱這個 observable	
observable.subscribe(observer)

// Jerry
// Anna
// complete
```

```javascript
var observable = Rx.Observable
  .create(function(observer) {
    try {
      observer.next('Jerry');
      observer.next('Anna');
      throw 'some exception';
    } catch(e) {
      observer.error(e)
    }
  });
	
// 宣告一個觀察者，具備 next, error, complete 三個方法
var observer = {
	next: function(value) {
		console.log(value);
	},
	error: function(error) {
		console.log('Error: ', error)
	},
	complete: function() {
		console.log('complete')
	}
}

// 用我們定義好的觀察者，來訂閱這個 observable	
observable.subscribe(observer)

// Jerry
// Anna
// Error: some exception
```

* Observer can only have `next function`. It's optional.

{% hint style="info" %}
Sometimes a observable can be an infinitie sequence, such as click event.
{% endhint %}

{% hint style="info" %}
You can also pass `next, error` and `complete` by order in `observable.subscribe`. It will compose it to be a observer object.
{% endhint %}

* Observable and addEventListener are a bit alike when they are doing subscribing and addEventListener. However, what they are actually doing is different.
* addEventListener is follow Observer Pattern. It will reserve <mark style="color:red;">a listener list</mark>. However, Observable don't have that list. Observable is more likely to <mark style="color:red;">execute a object's function</mark> and pass data into the function.

{% hint style="success" %}
Summary

* Observable can deal with **async** and **sync** simultaneously.
* Observer is an object and contains with three functions such as **next**, **error** and **complete.**
* Subscribe an Observable is **executing a function**
{% endhint %}
