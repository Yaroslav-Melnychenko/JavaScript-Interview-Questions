# JavaScript-Interview-Questions

## Questions

1. [Data Types](#data-types)
2. [Hoisting. Scope and Scope Chain](#hoisting-scope-chain)
3. [Debugger](#debugger)
4. [Pass by type/reference. Deep cloning](#pass-by-type-reference-deep-cloning)
5. [Strict Mode](#strict-mode)
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
