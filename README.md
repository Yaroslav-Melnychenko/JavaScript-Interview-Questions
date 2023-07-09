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
12. [High Order Functions](#high-order-functions)
13. [Memoization](#memoization)
14. [Recurcion](#recurcion)
15. [Generator Functions](#generator-functions)
16. ["this" keyword](#this-keyword)
17. [bind(), call(), apply()](#bind-call-pply)
18. [Object Prototype](#object-prototype)
19. [Prototyping Inheritance](#prototyping-nheritance)
20. [Promises](#Promises)
21. [Async Await](#async-await)
22. [Set and WeakSet](#set-and-weakset)
23. [Map and WeakMap](#map-and-weakmap)
24. [JavaScript Design Patterns](#javaScript-design-patterns)
25. [OOP](#oop)
26. [SOLID](#solid)
27. [React. What is it JSX?](#react-what-is-it-JSX)
28. [React. What is it virtual DOM](react-what-is-it-virtual-DOM)
29. [Redux. Reducer](redux-reducer)


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


## **High Order Functions**
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


## **Memoization**
Memoization is reate cache object to store the results of function calls
```javascript
function fibonacci(n, memo = {}) {
  if (n in memo) {
    return memo[n]; // If the result is already cached, return it
  }

  if (n <= 2) {
    return 1; // Base case for fibonacci sequence
  }

  const result = fibonacci(n - 1, memo) + fibonacci(n - 2, memo);
  memo[n] = result; // Cache the result for future use
  return result;
}

console.log(fibonacci(10)); // 55
console.log(fibonacci(15)); // 610
```


## **Recurcion**
```javascript
const factorial = (n) => {
	if (n === 1) return 1;
  	if (n === 2) return 2;
  
  	return factorial(n - 1) * n;
}

console.log('factorial', factorial(5))
```


## **Generator Functions**
Generator Functions that can be used to create iterators
```javascript
 function* numberGenerator() {
    yield 1;
    yield 2;
    yield 3;
  }

  const iterator = numberGenerator();

  console.log(iterator.next().value); // Output: 1
  console.log(iterator.next().value); // Output: 2
  console.log(iterator.next().value); // Output: 3
  console.log(iterator.next().value); // Output: undefined
```


## **"this" keyword**
"this" allows you to access and manipulate properties and methods within the context of the current object.
The value of "this" is determined dynamically based on how a function is called. It can have different values depending on the way the function is invoked.
- Global scope: If this is used outside of any function or object, it refers to the global object, which is typically the window object in web browsers or the global object in Node.js.
- Object method: When this is used inside a method of an object, it refers to the object itself. You can use this to access other properties or methods of the object.
```javascript
const myObject = {
  property: 'value',
  method: function() {
    console.log(this.property); // Accessing property of the object
  }
};
myObject.method(); // Outputs: "value"
```
- Constructor function: When a function is used as a constructor with the new keyword, this refers to the newly created instance of the object.
```javascript
function MyClass() {
  this.property = 'value';
}
const myInstance = new MyClass();
console.log(myInstance.property); // Outputs: "value"
```
- Event handler: In event-driven programming, when an event occurs and an event handler function is invoked, this typically refers to the element that triggered the event.
```javascript
const button = document.querySelector('button');
button.addEventListener('click', function() {
  console.log(this); // Refers to the button element
});
```
### "this" vs lexical envitonment
The differences between the lexical environment and the this keyword in JavaScript:

1. Definition:
- Lexical Environment: The lexical environment is a data structure that holds variable and function declarations in a particular scope. It determines the accessibility and visibility of identifiers (variables and functions) based on the physical placement of code in the source file. Each function has its own lexical environment.
- "this" Keyword: this is a special keyword in JavaScript that refers to the current execution context or the object that a function is being executed on. It is determined dynamically at runtime based on how the function is invoked.

2. Scope Determination:
- Lexical Environment: The lexical environment is determined statically based on the lexical (or static) structure of the code. It is created during the creation phase of a function and does not change during runtime.
- "this" Keyword: The value of this is determined dynamically at runtime based on the way a function is called. It can have different values depending on the invocation context.

3. Accessibility:
- Lexical Environment: The lexical environment determines the accessibility of variables and functions based on their scope and the scope chain. Variables and functions defined in an outer scope are accessible in an inner scope, but not vice versa.
- "this" Keyword: The this keyword provides access to the properties and methods of the current object or execution context. It allows you to refer to the object itself and access its members.

4. Usage:
- Lexical Environment: The lexical environment is primarily used for scoping and resolving identifiers within a function. It helps determine which variables and functions are accessible within a specific scope.
- "this" Keyword: The this keyword is used to access and manipulate properties and methods within the context of the current object. It is often used in object-oriented programming to refer to the object on which a method is called.

In summary, the lexical environment deals with scoping and the visibility of variables and functions based on the physical structure of the code, while the this keyword relates to the dynamic execution context of a function and provides access to the current object or execution context.


## **bind(), call(), apply()**
call() and apply() are used to invoke a function with a specific "this" value and arguments.
bind() creates a new function with a bound this value and optional arguments, which can be invoked later.
```javascript
function Hello(a, b, c) {
  console.log(`Hello ${this.name}`);
  console.log('Params', a, b, c);
}

Hello.call({ name: 'John' }, 1, 2, 3);
Hello.apply({ name: 'Kate' }, [4, 5, 6]);

const HelloNew = Hello.bind({ name: 'Sara' }, 11, 22, 33);
HelloNew();
```


## Object Prototype
Object prototypes are a way to define a blueprint or template for creating objects.

There are multiple ways to work with object prototypes in JavaScript:

1. Constructor Functions and the prototype Property:
```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function() {
  console.log("Hello, my name is " + this.name);
};

const john = new Person("John");
john.sayHello(); // Output: Hello, my name is John
```

2. The Object.create() method:
```javascript
const personPrototype = {
  sayHello: function() {
    console.log("Hello, my name is " + this.name);
  }
};

const lili = Object.create(personPrototype);
lili.name = "Lili";
lili.sayHello(); // Output: Hello, my name is Lili
```

3. The class Syntax (ES6): ES6 introduced the class syntax. Under the hood, class still uses prototypes.
```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log("Hello, my name is " + this.name);
  }
}

const andy = new Person("Andy");
andy.sayHello(); // Output: Hello, my name is Andy
```


## **Prototyping Inheritance**
```javascript
  function Animal(name) {
    this.name = name;
  }

  Animal.prototype.running = function() {
    console.log(this.name, 'is running');
  }

  function Dog(name) {
    this.name = name;
  }

  Dog.prototype = Object.create(Animal.prototype);

  const dog1 = new Dog('🐩 ');
  dog1.running();
```

## **Promises**
Promises are used to handle asynchronous operations in javascript.

Pending - Initial state of promise.
Fulfilled - The async operation is completed.
Rejected - The async operation has failed.
Settled - Promise has been or rejected or fulfilled.

```javascript
const getValue = new Promise((resolve, reject) => {
	setTimeout(() => {
  	resolve('hello');
  }, 1000);
});

getValue.then(res => console.log('res', res)) // "res", "hello" after 1 sec
```


## **Async Await**
Async/await provides a more intuitive way to write asynchronous code and helps avoid the complexities of nested callbacks or promise chains. However, it's still important to understand the underlying concepts of promises and how they work with async/await to handle errors and control the flow of your asynchronous code effectively.

```javascript
const response = await fetch('https://api.example.com/data');
const data = await response.json();
```


## **Set and WeakSet**
###Set:
- Adding and Removing Elements: add(), delete()
- Checking the Size and Presence of Elements: size, has()
- Iteration: for...of and forEach() loops
- Unique Values: If you try to add a duplicate value, it will be ignored
```javascript
let obj = { name: 'John' };
const set = new Set();
set.add(obj);
obj = null;
console.log('set', set); // Set(1) {name: "John"}
```

### WeakSet
No Iteration
Limited Methods: It does not have methods like size or forEach
Weakly Held References: do not prevent the referenced objects from being removed
```javascript
let obj = { name: 'John' };
const set = new Set();
set.add(obj);
obj = null;
console.log('set', set); // WeakSet {}
```


## **Map and WeakMap**
Map and WeakMap - built-in data structures that allow you to store key-value pairs
### Map
Map is a collection of key-value pairs where the keys can be of any type.
It has own methods: get(), has(), delete(), set(), for (const [key, value] of map) - iterate
```javascript
const map = new Map();
map.set('key1', 1);
map.set('key2', 2);
console.log(map); // Map(2) {key1: 1, key2: 2}
```

### WeakMap
- The keys in a WeakMap must be objects
- WeakMap does not have a iterator methods, size property
- They are held weakly (Garbage Collection)
```javascript
var k1 = {a: 1};
var k2 = {b: 2};

var map = new Map();
var wm = new WeakMap();

map.set(k1, 'k1');
wm.set(k2, 'k2');

k1 = null;
map.forEach(function (val, key) {
console.log(key, val); // k1 {a: 1}
});

k2 = null;
console.log(wm.get(k2)); // undefined
```


## **JavaScript Design Patterns**
- Singleton Pattern:
    The Singleton pattern ensures that a class has only one instance, and provides a global point of access to it.
    This can be useful in scenarios where only a single instance of a class is required,
    such as managing a shared resource or configuration.

- Factory Pattern:
    The Factory pattern is used to create objects without exposing the object creation logic directly to the client.
    It provides a factory method that returns an instance of the object based on specific parameters or configurations.

- Observer Pattern:
    The Observer pattern establishes a one-to-many relationship between objects,
    where when one object changes its state, all its dependents (observers) are notified and updated automatically. 
    It is commonly used in event-driven systems or for implementing pub-sub architectures.

- Module Pattern:
    The Module pattern encapsulates a set of related variables and functions into a single object. 
    It provides a way to create private variables and methods that are accessible only within the module, 
    allowing for better organization and encapsulation of code.

- Prototype Pattern:
    The Prototype pattern creates objects by cloning an existing object (prototype) rather than creating new instances from scratch. 
    It is useful when creating multiple objects with similar properties and behaviors, as it reduces the need for class 
    instantiation and improves performance.

- MVC (Model-View-Controller) Pattern:
    The MVC pattern is a software architectural pattern that separates an application into 
    three interconnected components: the Model (data and business logic), the View (presentation layer), 
    and the Controller (handles user input and updates the model and view). It helps to achieve separation 
    of concerns and promotes code organization and maintainability.

- Decorator Pattern:
    The Decorator pattern allows dynamically adding new behavior or modifying existing 
    behavior of an object without affecting other instances of the same class. 
    It involves wrapping an object with another object that provides additional functionality 
    or alters the behavior of the original object.


## **OOP**
OOP, Object-Oriented Programming, is a programming paradigm that told us how the code should be organized.
There are main 3 concepts:
- Inheritance: allows classes to inherit properties and methods from other classes, promoting code reuse.
- Polymorphism: used to create the functions with the same name and different execution
- Encapsulation: hides internal details of an object and provides public interfaces for interaction

## **SOLID**
### Single Responsibility Principle (SRP):
The class should do only one job. For example it it is User class ther should be logic related only for users. There should not be presend something else, for example logger data, erc.

### Open-Closed Principle (OCP):
Software entities (classes, modules, functions) should be open for extension but closed for modification. It means that you should be able to extend the behavior of a software entity without modifying its existing code.

### Liskov Substitution Principle (LSP):
The behavior of the base class should be preserved in its subclasses. In other words the extended class should not substitute the base class methods.

### Interface Segregation Principle (ISP):
Program entities should not depend on methods they do not use.

### Dependency Inversion Principle (DIP):
High-level modules should not depend on low-level modules; both should depend on abstractions. This principle promotes loose coupling between modules. It allows modules to be more independent, flexible, and easier to test and maintain.


## **React. What is it JSX**
JavaScript XML. It is a syntax extension used in React. JSX allows developers to write HTML-like code within JavaScript, enabling them to define the structure and content of their components in a declarative and intuitive manner. JSX looks similar to HTML, but it's not actually HTML. It's a syntax extension that gets transformed into regular JavaScript using a transpiler like Babel before it can be executed by the browser.

## **React. What is it virtual DOM**
It is a lightweight copy of the actual DOM, which is a representation of the HTML structure of a web page. The virtual DOM exists in memory and is used to track and manage changes to the user interface.
Here's how the virtual DOM works in React:
- When you create a React component, you define its structure and behavior using JSX or JavaScript.
- React uses the virtual DOM to create a virtual representation of the component's structure.
- When changes occur in the component's state or props, React updates the virtual DOM with the new values.
- React then performs a process called "reconciliation" to compare the previous virtual DOM with the updated one, determining the minimal set of changes needed to be made to the actual DOM.
- Finally, React efficiently updates the real DOM by applying only the necessary changes, resulting in an optimized and performant rendering of the updated component.

## **Redux. Reducer**
Reducers are functions that take the current state and an action as arguments, and return a new state result.
In other words, (state, action) => newState.

## **Redux. Dispatch**
Dispatch is a function provided by Redux that allows you to trigger an action.

## **Redux. Action**
In Redux, actions are plain JavaScript objects that contain type and payload value
```javascript
const incrementAction = {
  type: 'INCREMENT',
  payload: {
    amount: 1
  }
};
```
