- [Function as first class object](#function-as-first-class-object)
  - Characteristics :
    - [1. function can be stored in variable, object, array](#1-function-can-be-stored-in-variable-object-array)
    - [2. function can be used as an input/argument for another function](#2-function-can-be-used-as-an-inputargument-for-another-function)
    - [3. function can be returned from another function](#3-function-can-be-returned-from-another-function)
  - Usage of : Function as first class object
    - [Higher order functions](#higher-order-functions)
    - [Use Closure for private state/static variable](#use-closure-for-private-statestatic-variable)

# Function as first class object

Q : What does it means "Function as first class object"

A :

### 1. function can be stored in `variable`, `object`, `array`
```js
function foo() {
}

// stored in variable
const myVarFoo = foo;

// stored in object
const myObjFoo = {
  foo: foo
}

// stored in array
const myArrFoo = [foo];
```

### 2. function can be used as an input/argument for another function

```js
function foo() {
  console.log('foo');
}

function bar(foo) {
  foo();
  console.log('bar');
}

bar(); // output: foo bar
```

### 3. function can be returned from another function

```js
function createGenerator(){  
  return function generateNewID(){
    return 1;
  }
}

console.log(createGenerator()()); // 1
```


## Higher order functions

By using the characteristic of "first class object", we can create  `Higher order functions`

Q : What is "Higher order functions"

A : 

A function that 
- takes another functions as an input/argument : 2nd characteristic of "first class object"
- and/or return a function : 3rd characteristic of "first class object"


Example :
- [Array​.prototype​.filter()
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
- [Array​.prototype​.map()
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
- [Array​.prototype​.reduce()
](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
- etc...

## Use Closure for private state/static variable

When we want to have to keep track how many times that a function is called. Is required to store the `n call` on `state` variable.

```js
function getFooCounter() {
  let calledCount = 0;
  return function foo() {
    return ++calledCount;
  }
}

let fooCounter = getFooCounter();

fooCounter(); // 1
fooCounter(); // 2
fooCounter(); // 3
```




## Links :
- https://www.freecodecamp.org/news/here-are-a-few-function-decorators-you-can-write-from-scratch-488549fe8f86/
