# Hoisting Javascript

- [Variable Hoisting](#variable-hoisting)
  - [Variable Hoisting : global scope](#variable-hoisting--global-scope)
  - [Variable Hoisting : function scope](#variable-hoisting--function-scope)
  - [Variable Hoisting : undeclared variable](#variable-hoisting--undeclared-variable)
  - [prevent use of undeclared variable : use strict](#prevent-use-of-undeclared-variable--use-strict)
- [Function Hoisting](#function-hoisting)
  - [Function declarations](#function-declarations)
  - [Function expression](#function-expression)

Q : What is Hoisting ?

A :

> Javascript mechanism : "variable/function **declaration move to the top of their scope** before code execution"


Q : What is the scope means ?

A :

```js
// global scope

function hoist() {
  // function scope
  
}
```

Before getting started, what need to know

```js
var a;
// default value of for declared variable is undefined
console.log(a); // undefined
console.log(typeof a); // undefined

// when trying to access undeclared variable it will give ReferenceError
console.log(b); // Uncaught ReferenceError: b is not defined
console.log(typeof b); // undefined
```

## Variable Hoisting


Example :

## Variable Hoisting : global scope

1. Global scope : When the `a`, `b` is called before the `declaration`. It's will return `undefined` value for `a` and `b`.

```js
console.log(a, b, a + b); // undefined undefined NaN
var a =10;
var b =5;
```

same with this

```js
// hoisting the declaration : move to the top of global scope
var a;
var b;

console.log(a, b, a + b); // undefined undefined NaN
a =10;
b =5;
```

## Variable Hoisting : function scope

2. Function scope : When `messsage` is called it will be hoisted to the top of function scope

```js
function hoist() {
  console.log(message); // undefined
  var message='Hoisting is all the rage!'
}

hoist();
```

same with this

```js
function hoist() {
  // hoisting the declaration : move to the top of function scope
  var message;

  console.log(message); // undefined
  message='Hoisting is all the rage!'
}

hoist();
```


Q : What happened for `undeclared` variable ? is it also hoisted ?

A :

> For `undeclared` variable it will be hoisted, when the code `assigning` that varible is executed.

> That means all `undeclared` variable is `global` variable

Example :

## Variable Hoisting : undeclared variable

3. `undeclared` variable is `assigned` inside a function, the called outside of function scope

```js
function hoist() {
  a = 20;
  var b = 100;
}

hoist();

// a hoisted become global variable
console.log(a); // 20

// access b outside of scope : hoist function
console.log(b);  // Uncaught ReferenceError: b is not defined
```

## prevent use of undeclared variable : use strict

Q : How to prevent using of `undeclared` variable, is that a good practice ?

A : Of course not, hoisting the `undeclared` variable become `global`, will make the variable so hard to trace. To avoid use of it use `'use strict';` mode. So instead of hoisting the `undeclared` varibale with value `undefined`. It will throw `ReferenceError` when the variable is called.

```js
'use strict';

console.log(hoist); // Output: ReferenceError: hoist is not defined
hoist = 'Hoisted'; 
```

## Function Hoisting

### Function declarations

```js
hoisted(); // Output: "This function has been hoisted."

function hoisted() {
  console.log('This function has been hoisted.');
};
```

same with this 


```js
function hoisted() {
  console.log('This function has been hoisted.');
};
hoisted(); // Output: "This function has been hoisted."
```

### Function expression

But it will not work when we are using function expression.

```js
expression(); //Output: "TypeError: expression is not a function

var expression = function() {
  console.log('Will this work?');
};
```

same with this 

```js
var expression; // undefined
expression(); //Output: "TypeError: expression is not a function

expression = function() {
  console.log('Will this work?');
};
```

