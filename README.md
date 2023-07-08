# JavaScript-Interview-Questions

## Questions

1. [Data Types](#data-types)
2. [Hoisting. Scope and Scope Chain](#hoisting-scope-and-scope-chain)
3. [Debugger](#debugger)
4. [Strict Mode](#strict-mode)
5. [Pass by type or reference. Deep cloning](#pass-by-type-or-reference-deep-cloning)
6. [var, let, const](#var-let-const)
7. [Error types](#error-types)
8. [DOM and BOM](#dom-and-bom)
9. [Function declarations and differences](#function-declarations-and-differences)
10. [Currying](#currying)
11. [Closures](#closures)
12. [Hign Order Functions](#high-order-functions)
13. [Memoization](#memoization)
14. [Recurcion](#recurcion)
15. [Generator Functions](#generator-functions)
16. ["this" keyword](#this-keyword)
17. [bind(), call(), apply()](#bind-call-pply)
18. [Object Prototype](#object-prototype)
19. [Prototyping Inheritance](#prototyping-nheritance)
20. [Prototype Design Pattern](#prototype-design-pattern)
21. [Promises](#Promises)
22. [Async/Await](#async-await)
23. [Set and WeakSet](#set-weakset)
24. [Map and WeakMap](#map-weakmap)
25. [JavaScript Design Patterns](#javaScript-design-patterns)
26. [OOP](#oop)
27. [SODID](#solid)


## **Data Types**

```javascript
// Numbers:
let length = 16;

// Strings:
let color = "Yellow";

// Booleans
let x = true;

// BigInt
const bigNumber = 1234567890123456789012345678901234567890n;
const bigNumberFromConstructor = BigInt("1234567890123456789012345678901234567890");

// undefined
let x;
console.log(x); // Output: undefined

function doSomething() {
  // No return statement
}
console.log(doSomething()); // Output: undefined

// null
const car = null;

// Symbol
const key1 = Symbol();
const key2 = Symbol("description");
const obj = {
  [key1]: "value 1",
  [key2]: "value 2"
};
console.log(obj[key1]); // Output: value 1
```

## **Hoisting. Scope and Scope Chain**

### Hoisting
Hoisting is a JavaScript behavior where variable and function declarations are moved to the top of their scopes during the compilation phase. This means that you can use variables and call functions before they are declared in your code.
However, only the declarations are hoisted, not the initializations or assignments. For example:
```javascript
console.log(x); // Output: undefined
var x = 5;
```

### Scope
Scope refers to the accessibility or visibility of variables, functions, and objects. In JavaScript, there are global scope and local scope (function scope and block scope). Variables defined within a scope are accessible only within that scope, unless they are explicitly shared with outer scopes. For example:
```javascript
function myFunction() {
  var x = 10; // Local scope variable
  console.log(x); // Output: 10
}
console.log(x); // Error: x is not defined (not accessible outside the function scope)
```

### Scope Chain
The scope chain is a hierarchical structure that determines the accessibility of variables in nested functions. Each function has its own scope, and when a variable is referenced, JavaScript searches for that variable in the current scope and then follows the chain of nested scopes until it finds the variable or reaches the global scope
```javascript
var x = 10; // Global variable

function outerFunction() {
  var y = 20; // Outer function scope variable

  function innerFunction() {
    var z = 30; // Inner function scope variable
    console.log(x + y + z); // Output: 60 (accessible through the scope chain)
  }

  innerFunction();
}
outerFunction();
```

## **Debugger**
Debugger can do following:
- Setting Breakpoints
- Inspecting Variables
- Stepping through Code
- Watching Expressions
- Conditional Breakpoints
- Handling Exceptions


## **Strict Mode**
Strict mode is a feature in JavaScript that enables a stricter set of rules and behaviors in the execution of code.
- Strict mode throw errors if you assigning values to undeclared variables, using reserved keywords as variable names
- It prevents the use of the with statement, which can cause scope-related issues, and restricts the usage of the eval() function, which can introduce security vulnerabilities.
- In strict mode, the value of this is different in certain scenarios compared to non-strict mode. In functions that are not methods, this is set to undefined, rather than the global object (window in browsers).
```javascript
'use strict';

function myFunction() {
  console.log(this);
}
myFunction(); // Output: undefined
```
- Strict mode improves error handling by making it stricter and more informative. It throws errors for common mistakes like assigning values to read-only properties, duplicating function parameter names, or using delete on variables, functions, or function arguments.


## **Pass by type or reference. Deep cloning**
- "pass by value" for primitive types such as numbers, strings, booleans, null, and undefined
```javascript
let x = 2;
let y = x;
y++;

console.log(x); // 2
console.log(y); // 3
```

- "pass by reference" for non-primitive types such as objects
```javascript
let x = { name: 'John' };
let y = x;

x.name = 'Kate';

console.log(x); // { name: 'Kate' }
console.log(y); // { name: 'Kate' }
```


## **var, let, const**
### var
- Function-scoped
- Hoisting
- Reassignable
- No block scope
```javascript
for (var i = 0; i < 10; i++) {
	console.log('i', i); // "i", "from 1 to 9"
} 
console.log('out of block', i); // "out of block", 10
```

### let
- Block-scoped
- No hoisting
- Reassignable
- Temporal Dead Zone - accessed the variable earlier than its declaration would throw a ReferenceError
```javascript
for (let i = 0; i < 10; i++) {
	console.log('i', i); // "i", "from 1 to 9"
} 
console.log('out of block', i); // Uncaught ReferenceError: i is not defined
```

### const
- Block-scoped
- No hoisting
- Cannot be reassigned
- Temporal Dead Zone (same as let)


## **Error types**
- Syntax Error:
```javascript
// Missing closing parenthesis
if (x > 5 {
	console.log("x is greater than 5");
}
```

- Reference Error:
```javascript
// Trying to access an undefined variable
console.log(myVariable);
```

- Type Error - An error occurs when a value is used outside the scope of its data type.
```javascript
let num = 15;
console.log(num.split("")); // converts a number to an array
```

- Evaluation Error - Current JavaScript engines and EcmaScript specifications do not throw this error. However, it is still available for backward compatibility. The error is called when the eval() backward function is used, as shown in the following code block:
```javascript
try{
    throw new EvalError("'Throws an error'")
} catch(error){
    console.log(error.name, error.message)
}
```

- RangeError - There is an error when a range of expected values is required, as shown below:
```javascript
const checkRange = (num)=>{
    if (num < 30) throw new RangeError("Wrong number");
    return true
}
checkRange(20);
```

- URI Error - When the wrong character(s) are used in a URI function
```javascript
console.log(decodeURI("https://www.educative.io/shoteditor"))
console.log(decodeURI("%sdfk"));
```

-Internal Error - In the JS engine, this error occurs most often when there is too much data and the stack exceeds its critical size. When there are too many recursion patterns, switch cases, etc., the JS engine gets overwhelmed.

## **DOM and BOM**

### DOM - Document Object Model
It represents the structure of an HTML or XML document as a tree-like model JavaScript can access and manipulate the DOM using the provided APIs

### BOM - Browser Object Model
The BOM provides objects such as window, document, navigator, history, and location, among others, which allow developers to interact with the browser and the webpage's content

## **Function declarations and differences**

### Function Declaration
```javascript
function functionName(parameters) {
  // Function body
}
```
Function declarations are hoisted, which means they can be called before they are declared in the code.

### Function Expression
```javascript
const functionName = function(parameters) {
  // Function body
};
```
Function expressions are not hoisted, so they can only be called after they are defined in the code.

### Arrow Function Expression
```javascript
const functionName = (parameters) => {
  // Function body
};
```
Arrow functions have lexical scoping of this, which means the value of this inside the function is determined by the surrounding context.

### Function Constructor
```javascript
var functionName = new Function('parameters', 'Function body');
```


## **Currying**
Currying is a concept in functional programming that transform a function with multiple arguments into a series of functions with single argument
```javascript
function add(x) {
  return function(y) {
    return x + y;
  };
}

const addCurried = add(5);
console.log(addCurried(3)); // Output: 8

console.log(add(5)(3)); // Output: 8
```


## **Closures**
Closures it is the ability of a function to remember and access its lexical scope, even when it is executed outside that scope
```javascript
const counter = () => {
  let count = 0;

  const increase = () => {
    count++;
    console.log('increase, count = ', count);
  }

  const decrease = () => {
    count--;
    console.log('decrease, count = ', count);
  }

  return {
    increase,
    decrease
  }
}

const count = counter();
count.increase(); // "increase", 1
count.increase(); // "increase", 2
```


## **Hign Order Functions**
Higher-order function is a function that does at least one of the following:
- takes one or more functions as arguments (i.e. a procedural parameter, which is a parameter of a procedure that is itself a procedure),
- returns a function as its result.
In js array methods like map(), filter(), reduce(),... is a high-order-functions
```javascript
function multiplyBy(factor) {
  return function (number) {
    return number * factor;
  };
}
const multiplyByTwo = multiplyBy(2);
console.log(multiplyByTwo(5)); // Output: 10

```
