# 🧠 Functions - Complete Guide

Master functions: the building blocks of reusable logic in JavaScript.

---

## 📚 Quick Contents

1. [What are Functions?](#what-are-functions)
2. [Function Declarations](#function-declarations)
3. [Parameters vs Arguments](#parameters-vs-arguments)
4. [Return Values](#return-values)
5. [Function Expressions](#function-expressions)
6. [Arrow Functions](#arrow-functions)
7. [Default, Rest & Spread](#default-rest--spread)
8. [First-Class Functions](#first-class-functions)
9. [Higher-Order Functions](#higher-order-functions)
10. [Closures & Scope](#closures--scope)
11. [IIFE](#iife)
12. [Hoisting](#hoisting)
13. [Common Confusions](#common-confusions)

---

## ❓ What are Functions?

Functions are reusable blocks of code that perform a specific task. Instead of repeating the same logic, wrap it in a function and reuse it with different inputs.

**Analogy**: Function = Vending Machine
- **Input**: You give money + item code
- **Output**: Machine gives you the item
- **Logic**: Hidden inside the machine

```javascript
// Without function (repetitive)
console.log("Hello John");
console.log("Hello Sarah");
console.log("Hello Mike");

// With function (reusable)
function greet(name) {
  console.log("Hello " + name);
}

greet("John");   // Reuse with different input
greet("Sarah");
greet("Mike");
```

**Benefits**:
- ✅ Write once, use many times
- ✅ Easier to maintain
- ✅ Better code organization
- ✅ Reduce errors

---

## 🏗️ Function Declarations

The traditional way to define functions.

```javascript
// Basic syntax
function greet() {
  console.log("Welcome to JavaScript!");
}

greet(); // Call the function

// With parameter
function sayHello(name) {
  console.log("Hello " + name);
}

sayHello("Harsh");  // "Hello Harsh"
sayHello("Alice");  // "Hello Alice"

// Multiple parameters
function add(a, b) {
  console.log(a + b);
}

add(5, 10);  // 15
add(20, 30); // 50

// With return
function multiply(x, y) {
  return x * y;
}

let result = multiply(4, 5);
console.log(result); // 20
```

**Key Points**:
- Define once with `function` keyword
- Call multiple times with different inputs
- Parameters are placeholders
- Can have 0 or more parameters

---

## 📋 Parameters vs Arguments

- **Parameter**: Placeholder in function definition
- **Argument**: Actual value passed when calling function

```javascript
function greet(name) {
  //   ^^^^ This is a PARAMETER
  console.log("Hello " + name);
}

greet("Harsh");
//     ^^^^^^^ This is an ARGUMENT

// Real example
function calculateArea(length, width) {
  // length, width = PARAMETERS
  return length * width;
}

calculateArea(5, 10);
// 5, 10 = ARGUMENTS
// Returns 50
```

**Multiple Parameters**:
```javascript
function displayInfo(name, age, city) {
  console.log(`${name} is ${age} and lives in ${city}`);
}

displayInfo("John", 30, "NYC");
// Parameters: name, age, city
// Arguments: "John", 30, "NYC"
```

---

## 🔄 Return Values

The `return` statement sends a value back from the function. After `return`, the function exits.

```javascript
// Without return (undefined)
function greet(name) {
  console.log("Hello " + name);
  // No return, so undefined
}

let result = greet("John");
console.log(result); // undefined

// With return
function sum(a, b) {
  return a + b;
}

let total = sum(5, 10);
console.log(total); // 15

// Early return (exit function early)
function checkAge(age) {
  if (age < 18) {
    return "Not eligible";
  }
  // This only runs if age >= 18
  return "Eligible";
}

console.log(checkAge(15)); // "Not eligible"
console.log(checkAge(25)); // "Eligible"
```

**⚠️ Important Difference**:
```javascript
// ❌ WRONG - console.log is NOT return
function getNumber() {
  console.log(42); // Prints, but doesn't return!
}
let num = getNumber(); // num is undefined

// ✅ CORRECT - use return
function getNumber2() {
  return 42; // Returns the value
}
let num2 = getNumber2(); // num2 is 42
```

---

## 🎁 Function Expressions

Functions stored in variables. Cannot be hoisted (can't call before defining).

```javascript
// Function expression
const greet = function() {
  console.log("Hello!");
};

greet(); // "Hello!"

// With parameter
const greet2 = function(name) {
  console.log("Hello " + name);
};

greet2("John"); // "Hello John"

// Named function expression (rare)
const add = function sum(a, b) {
  return a + b;
};

console.log(add(5, 10)); // 15
// console.log(sum(5, 10)); // ERROR - sum is not accessible

// Comparison: Declaration vs Expression
// DECLARATION - can call before defining (hoisted)
hello(); // Works!
function hello() {
  console.log("Hi");
}

// EXPRESSION - must define before calling
// greet(); // ERROR - greet is not defined yet
const greet3 = function() {
  console.log("Hi");
};
greet3(); // Works
```

---

## 🏹 Arrow Functions

Modern syntax for function expressions. Cleaner and more concise.

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add2 = (a, b) => {
  return a + b;
};

// Concise arrow (single line)
const add3 = (a, b) => a + b; // Implicit return

console.log(add(5, 10));   // 15
console.log(add2(5, 10));  // 15
console.log(add3(5, 10));  // 15

// Single parameter (optional parentheses)
const square = x => x * x; // Works
const square2 = (x) => x * x; // Also works

console.log(square(4));  // 16

// No parameter
const greet = () => "Hello!";
console.log(greet()); // "Hello!"
```

**Arrow vs Regular Functions**:
```javascript
// ❌ Arrow functions DON'T have their own 'this'
const person = {
  name: "John",
  greet: () => {
    console.log(this.name); // undefined - 'this' is global
  }
};

// ✅ Regular functions have their own 'this'
const person2 = {
  name: "John",
  greet: function() {
    console.log(this.name); // "John"
  }
};

person2.greet(); // "John"
```

---

## 🎛️ Default, Rest & Spread

### Default Parameters

```javascript
function multiply(a = 1, b = 1) {
  return a * b;
}

console.log(multiply(5, 10)); // 50
console.log(multiply(5));     // 5 (b defaults to 1)
console.log(multiply());      // 1 (both default to 1)

// Real example
function greet(name = "Guest") {
  console.log("Hello " + name);
}

greet("John");  // "Hello John"
greet();        // "Hello Guest"
```

### Rest Parameter (...nums)

Collects remaining arguments into an array.

```javascript
function sum(...nums) {
  let total = 0;
  for (let num of nums) {
    total += num;
  }
  return total;
}

console.log(sum(1, 2, 3));       // 6
console.log(sum(1, 2, 3, 4, 5)); // 15
console.log(sum(10));            // 10

// Multiple parameters with rest
function printInfo(name, age, ...hobbies) {
  console.log(name, age);        // name, age
  console.log(hobbies);          // remaining as array
}

printInfo("John", 30, "coding", "gaming", "reading");
// John 30
// ["coding", "gaming", "reading"]
```

### Spread Operator (...array)

Spreads array elements as individual arguments.

```javascript
const nums = [1, 2, 3];

function sum(a, b, c) {
  return a + b + c;
}

console.log(sum(...nums)); // Spreads [1, 2, 3] to 1, 2, 3
// Result: 1 + 2 + 3 = 6

// Spread with array
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Spread with object
const obj1 = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
const merged = { ...obj1, ...obj2 };
console.log(merged); // { a: 1, b: 2, c: 3, d: 4 }
```

---

## 🎯 First-Class Functions

JavaScript treats functions as values: assign to variables, pass as arguments, return from functions.

```javascript
// 1. Assign function to variable
const greet = function() {
  return "Hello!";
};

// 2. Pass function as argument
function runFunction(fn) {
  return fn();
}

console.log(runFunction(greet)); // "Hello!"

// 3. Return function from function
function createGreeter(greeting) {
  return function(name) {
    return greeting + " " + name;
  };
}

const sayHello = createGreeter("Hello");
console.log(sayHello("John")); // "Hello John"
```

---

## 🧬 Higher-Order Functions

Functions that take other functions as arguments or return functions.

```javascript
// HOF that takes a function
function applyTwice(fn, value) {
  return fn(fn(value));
}

function double(x) {
  return x * 2;
}

console.log(applyTwice(double, 5)); // double(double(5)) = 20

// HOF that returns a function
function createMultiplier(x) {
  return function(y) {
    return x * y;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5)); // 10
console.log(triple(5)); // 15

// Real example: Array methods (forEach, map, filter)
const nums = [1, 2, 3, 4, 5];

nums.forEach((num) => {
  console.log(num * 2);
}); // forEach takes a function!

const doubled = nums.map((num) => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

const evens = nums.filter((num) => num % 2 === 0);
console.log(evens); // [2, 4]
```

---

## 🔐 Closures & Scope

A closure is when a function remembers its parent scope, even after the parent has finished.

```javascript
// Simple closure
function outer() {
  let count = 0; // Parent scope variable
  
  return function() {
    count++;
    console.log(count);
  };
}

const counter = outer();
counter(); // 1
counter(); // 2
counter(); // 3
// Even after outer() is done, counter remembers count!

// Real example: Bank account
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Private variable
  
  return {
    deposit: function(amount) {
      balance += amount;
      return balance;
    },
    withdraw: function(amount) {
      balance -= amount;
      return balance;
    },
    getBalance: function() {
      return balance;
    }
  };
}

const myAccount = createBankAccount(1000);
console.log(myAccount.deposit(500));    // 1500
console.log(myAccount.withdraw(200));   // 1300
console.log(myAccount.getBalance());    // 1300

// ⚠️ Can't access balance directly
console.log(myAccount.balance); // undefined (private)
```

**Lexical Scope**:
```javascript
const global = "global";

function outer() {
  const outer_var = "outer";
  
  function inner() {
    const inner_var = "inner";
    console.log(inner_var);  // "inner" (own scope)
    console.log(outer_var);  // "outer" (parent scope)
    console.log(global);     // "global" (global scope)
  }
  
  inner();
}

outer();
```

---

## ⚡ IIFE

Immediately Invoked Function Expression - runs instantly and creates private scope.

```javascript
// Basic IIFE
(function() {
  console.log("Runs immediately!");
})();
// Output: "Runs immediately!"

// IIFE with parameters
(function(name) {
  console.log("Hello " + name);
})("John");
// Output: "Hello John"

// Arrow IIFE
(() => {
  console.log("Arrow IIFE");
})();

// Used to create private scope
(function() {
  const secret = "This is private";
  console.log(secret);
})();

// console.log(secret); // ERROR - secret is not defined
```

---

## 🚀 Hoisting

Function declarations are hoisted (moved to top). Expressions are not.

```javascript
// ✅ HOISTING WORKS - Declaration
hello(); // Works! Function is hoisted
function hello() {
  console.log("Hi");
}

// ❌ HOISTING DOESN'T WORK - Expression
// greet(); // ERROR - greet is not defined
const greet = function() {
  console.log("Hello");
};
greet(); // Now it works

// Arrow functions also NOT hoisted
// sayHi(); // ERROR
const sayHi = () => {
  console.log("Hi!");
};
sayHi(); // Works

// How hoisting works (conceptually)
console.log(x); // undefined (hoisted but not assigned)
var x = 5;

// Equivalent to:
var x; // Hoisted declaration
console.log(x); // undefined
x = 5; // Assignment stays in place
```

---

## ⚠️ Common Confusions

### ❌ Arrow functions don't have their own 'this'

```javascript
// Wrong for object methods
const person = {
  name: "John",
  greet: () => {
    console.log(this); // global object, NOT person
  }
};

// Correct for object methods
const person2 = {
  name: "John",
  greet: function() {
    console.log(this.name); // "John"
  }
};
```

### ❌ Return vs console.log

```javascript
function getValue1() {
  console.log(42); // Prints, doesn't return
}
const val1 = getValue1(); // val1 is undefined

function getValue2() {
  return 42; // Returns value
}
const val2 = getValue2(); // val2 is 42
```

### ❌ Closures trap variable values

```javascript
// Problem: Closure traps the final value
for (var i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // All print 3
  }, 100);
}

// Solution 1: Use let (block scope)
for (let i = 0; i < 3; i++) {
  setTimeout(function() {
    console.log(i); // Prints 0, 1, 2
  }, 100);
}

// Solution 2: IIFE
for (var i = 0; i < 3; i++) {
  (function(j) {
    setTimeout(function() {
      console.log(j); // Prints 0, 1, 2
    }, 100);
  })(i);
}
```

### ❌ forEach doesn't work with break

```javascript
// forEach can't break
[1, 2, 3, 4, 5].forEach(num => {
  if (num === 3) break; // ERROR!
});

// Use for-of instead
for (let num of [1, 2, 3, 4, 5]) {
  if (num === 3) break; // Works!
}
```

---

## 📊 Function Types Comparison

| Type | Syntax | Hoisted | Use Case |
|------|--------|---------|----------|
| Declaration | `function foo() {}` | ✅ Yes | Reusable, called many times |
| Expression | `const foo = function() {}` | ❌ No | Variables, callbacks |
| Arrow | `const foo = () => {}` | ❌ No | Modern, concise callbacks |
| IIFE | `(function() {})()` | N/A | Private scope |

---

## 🧠 Mindset

**Functions = Logic Blocks + Memory Holders**

- Functions make code reusable and clean
- Avoid repeating code (DRY principle)
- Use functions for organization
- Closures let functions remember values
- Higher-order functions unlock powerful patterns
- Always choose the right function type for the job

```javascript
// Poor: Repeated logic
let area1 = 5 * 10;
let area2 = 7 * 12;
let area3 = 3 * 8;

// Better: Reusable function
function area(length, width) {
  return length * width;
}

const area1 = area(5, 10);
const area2 = area(7, 12);
const area3 = area(3, 8);
```

---

**Master functions to master JavaScript! 🚀**
