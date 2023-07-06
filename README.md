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
