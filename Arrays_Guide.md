# 📦 Arrays - Complete Guide

Master arrays: the backbone of storing and manipulating multiple values.

---

## 📚 Quick Contents

1. [What are Arrays?](#what-are-arrays)
2. [Creating & Accessing](#creating--accessing)
3. [Modifier Methods](#modifier-methods)
4. [Extractor Methods](#extractor-methods)
5. [Iteration Methods](#iteration-methods)
6. [Destructuring & Spread](#destructuring--spread)
7. [Common Confusions](#common-confusions)
8. [Practical Examples](#practical-examples)

---

## ❓ What are Arrays?

An array is like a row of boxes where each box holds a value and has an index (0, 1, 2...).

Arrays store multiple values in a single variable: numbers, strings, objects, or even functions.

**Analogy**: Library shelves
- Each shelf = array
- Each book = element
- Book position = index (starts at 0)

```javascript
// Array of numbers
let marks = [90, 85, 78, 92];

// Array of strings
let fruits = ["apple", "banana", "mango"];

// Array of objects
let users = [
  { name: "John", age: 30 },
  { name: "Sarah", age: 25 }
];

// Mixed array
let mixed = [1, "hello", true, null, { id: 1 }];

// Empty array
let empty = [];
```

**Why use arrays?**
- ✅ Store related data together
- ✅ Access by index (fast)
- ✅ Easy iteration
- ✅ Rich methods for transformation

---

## 🏗️ Creating & Accessing

### Creating Arrays

```javascript
// Literal syntax (preferred)
let fruits = ["apple", "banana", "mango"];

// Array constructor
let numbers = new Array(1, 2, 3, 4, 5);

// Array with size
let empty = new Array(5); // [empty × 5]

// From string
let chars = "hello".split(''); // ['h', 'e', 'l', 'l', 'o']

// Array.of()
let arr = Array.of(1, 2, 3); // [1, 2, 3]

// Array.from()
let range = Array.from({ length: 5 }, (_, i) => i + 1); // [1, 2, 3, 4, 5]
```

### Accessing Elements

```javascript
let fruits = ["apple", "banana", "mango"];

// Index access (0-based)
console.log(fruits[0]); // "apple"
console.log(fruits[1]); // "banana"
console.log(fruits[2]); // "mango"

// Negative indexing (from end)
console.log(fruits.at(-1)); // "mango" (last)
console.log(fruits.at(-2)); // "banana" (second last)

// Array length
console.log(fruits.length); // 3

// Last element
console.log(fruits[fruits.length - 1]); // "mango"
```

### Updating Elements

```javascript
let marks = [90, 85, 78];

// Update by index
marks[1] = 88;
console.log(marks); // [90, 88, 78]

// Add to new index
marks[5] = 95;
console.log(marks); // [90, 88, 78, empty, empty, 95]

// Check if index exists
if (marks[2] !== undefined) {
  console.log("Index 2 exists");
}
```

---

## ⚙️ Modifier Methods

These methods change the original array.

### push() - Add to end

```javascript
let arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1, 2, 3, 4]

arr.push(5, 6);
console.log(arr); // [1, 2, 3, 4, 5, 6]

// Returns new length
let newLength = arr.push(7);
console.log(newLength); // 7
```

### pop() - Remove from end

```javascript
let arr = [1, 2, 3, 4];
let popped = arr.pop();
console.log(popped); // 4
console.log(arr);    // [1, 2, 3]

// Popping until condition
while (arr.length > 2) {
  arr.pop();
}
console.log(arr); // [1, 2]
```

### shift() - Remove from start

```javascript
let arr = [1, 2, 3];
let shifted = arr.shift();
console.log(shifted); // 1
console.log(arr);     // [2, 3]
```

### unshift() - Add to start

```javascript
let arr = [2, 3];
arr.unshift(1);
console.log(arr); // [1, 2, 3]

arr.unshift(0, -1);
console.log(arr); // [0, -1, 1, 2, 3]
```

### splice() - Add/Remove anywhere

```javascript
let arr = [1, 2, 3, 4, 5];

// Remove 2 items starting at index 1
arr.splice(1, 2);
console.log(arr); // [1, 4, 5]

// Add items at index 1
arr.splice(1, 0, 2, 3);
console.log(arr); // [1, 2, 3, 4, 5]

// Replace items
arr.splice(1, 2, 20, 30);
console.log(arr); // [1, 20, 30, 4, 5]
```

### reverse() - Reverse order

```javascript
let arr = [1, 2, 3, 4];
arr.reverse();
console.log(arr); // [4, 3, 2, 1]

// Works on strings too (after split)
let word = "hello".split('').reverse().join('');
console.log(word); // "olleh"
```

### sort() - Sort array

```javascript
let arr = [3, 1, 4, 1, 5];
arr.sort();
console.log(arr); // [1, 1, 3, 4, 5] - lexical sort

// Lexical sort issues
let nums = [10, 2, 30, 5];
nums.sort();
console.log(nums); // [10, 2, 30, 5] - WRONG! Treats as strings

// Correct numeric sort
nums.sort((a, b) => a - b);
console.log(nums); // [2, 5, 10, 30]

// Descending sort
nums.sort((a, b) => b - a);
console.log(nums); // [30, 10, 5, 2]

// Sort objects by property
let users = [
  { name: "John", age: 30 },
  { name: "Sarah", age: 25 },
  { name: "Mike", age: 35 }
];

users.sort((a, b) => a.age - b.age);
console.log(users);
// Sarah (25), John (30), Mike (35)
```

---

## 🔍 Extractor Methods

These methods don't modify the original array.

### slice() - Copy portion

```javascript
let arr = [1, 2, 3, 4, 5];

// From index 1 to 3 (excludes 3)
let sliced = arr.slice(1, 3);
console.log(sliced); // [2, 3]
console.log(arr);    // [1, 2, 3, 4, 5] - unchanged

// From index 2 to end
console.log(arr.slice(2)); // [3, 4, 5]

// Last 2 elements
console.log(arr.slice(-2)); // [4, 5]

// Copy entire array
let copy = arr.slice();
console.log(copy); // [1, 2, 3, 4, 5]
```

### join() - Convert to string

```javascript
let arr = ["a", "b", "c"];
let str = arr.join();
console.log(str); // "a,b,c"

// With custom separator
console.log(arr.join("-")); // "a-b-c"
console.log(arr.join(" ")); // "a b c"
console.log(arr.join(""));  // "abc"

// Reverse usage: split
let csv = "apple,banana,mango";
let fruits = csv.split(",");
console.log(fruits); // ["apple", "banana", "mango"]
```

### indexOf() & lastIndexOf()

```javascript
let arr = [1, 2, 3, 2, 4];

console.log(arr.indexOf(2));      // 1 (first occurrence)
console.log(arr.lastIndexOf(2));  // 3 (last occurrence)
console.log(arr.indexOf(5));      // -1 (not found)

// Check if exists
if (arr.indexOf(3) !== -1) {
  console.log("3 exists in array");
}

// Remove element
arr = arr.filter(x => x !== 2);
console.log(arr); // [1, 3, 4]
```

### includes() - Check existence

```javascript
let fruits = ["apple", "banana", "mango"];

console.log(fruits.includes("banana")); // true
console.log(fruits.includes("grape"));  // false

// Works with numbers
let nums = [1, 2, 3];
console.log(nums.includes(2)); // true

// Case sensitive
let words = ["Hello", "World"];
console.log(words.includes("hello")); // false
```

---

## 🔄 Iteration Methods

### map() - Transform each element

```javascript
let nums = [1, 2, 3, 4];

// Double each number
let doubled = nums.map(n => n * 2);
console.log(doubled); // [2, 4, 6, 8]
console.log(nums);    // [1, 2, 3, 4] - unchanged

// Extract property from objects
let users = [
  { name: "John", age: 30 },
  { name: "Sarah", age: 25 }
];

let names = users.map(user => user.name);
console.log(names); // ["John", "Sarah"]

// Convert to strings
let prices = [100, 200, 300];
let formatted = prices.map(p => `$${p}`);
console.log(formatted); // ["$100", "$200", "$300"]
```

### filter() - Keep matching elements

```javascript
let nums = [1, 2, 3, 4, 5, 6];

// Get even numbers
let evens = nums.filter(n => n % 2 === 0);
console.log(evens); // [2, 4, 6]

// Get numbers > 3
let greater = nums.filter(n => n > 3);
console.log(greater); // [4, 5, 6]

// Filter objects
let users = [
  { name: "John", age: 30, active: true },
  { name: "Sarah", age: 25, active: false },
  { name: "Mike", age: 35, active: true }
];

let activeUsers = users.filter(u => u.active);
console.log(activeUsers);
// [John, Mike]

// Chaining filters
let result = nums
  .filter(n => n > 2)
  .filter(n => n % 2 === 0);
console.log(result); // [4, 6]
```

### reduce() - Reduce to single value

```javascript
let nums = [1, 2, 3, 4, 5];

// Sum all
let sum = nums.reduce((acc, val) => acc + val, 0);
console.log(sum); // 15

// Product of all
let product = nums.reduce((acc, val) => acc * val, 1);
console.log(product); // 120

// Count occurrences
let arr = [1, 2, 2, 3, 3, 3, 4];
let counts = arr.reduce((acc, val) => {
  acc[val] = (acc[val] || 0) + 1;
  return acc;
}, {});
console.log(counts); // { '1': 1, '2': 2, '3': 3, '4': 1 }

// Group by property
let users = [
  { dept: "IT", name: "John" },
  { dept: "HR", name: "Sarah" },
  { dept: "IT", name: "Mike" }
];

let byDept = users.reduce((acc, user) => {
  acc[user.dept] = acc[user.dept] || [];
  acc[user.dept].push(user.name);
  return acc;
}, {});
console.log(byDept);
// { IT: ["John", "Mike"], HR: ["Sarah"] }
```

### forEach() - Execute for each element

```javascript
let nums = [1, 2, 3];

nums.forEach(n => {
  console.log(n * 2);
});
// Output: 2, 4, 6

// With index
["a", "b", "c"].forEach((letter, index) => {
  console.log(`${index}: ${letter}`);
});
// Output:
// 0: a
// 1: b
// 2: c

// ⚠️ forEach can't break/continue
// Use for-of instead if you need to
```

### find() - Find first match

```javascript
let nums = [1, 2, 3, 4, 5];

let firstEven = nums.find(n => n % 2 === 0);
console.log(firstEven); // 2

let user = [
  { id: 1, name: "John" },
  { id: 2, name: "Sarah" },
  { id: 3, name: "Mike" }
].find(u => u.id === 2);

console.log(user); // { id: 2, name: "Sarah" }

// Not found returns undefined
let notFound = nums.find(n => n > 10);
console.log(notFound); // undefined
```

### some() & every()

```javascript
let nums = [1, 2, 3, 4, 5];

// some() - at least one true
console.log(nums.some(n => n > 3));  // true (4, 5 exist)
console.log(nums.some(n => n > 10)); // false

// every() - all true
console.log(nums.every(n => n > 0));  // true (all > 0)
console.log(nums.every(n => n > 3));  // false (1, 2, 3 aren't)

// Real example: validation
let prices = [100, 200, 300];
console.log(prices.every(p => p > 0)); // true
console.log(prices.some(p => p > 250)); // true
```

---

## ✂️ Destructuring & Spread

### Destructuring

```javascript
// Basic
let [first, second] = ["a", "b", "c"];
console.log(first, second); // a, b

// Skip elements
let [first, , third] = ["a", "b", "c"];
console.log(first, third); // a, c

// Rest
let [head, ...tail] = [1, 2, 3, 4];
console.log(head); // 1
console.log(tail); // [2, 3, 4]

// Swap
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a, b); // 2, 1
```

### Spread Operator

```javascript
let arr = [1, 2, 3];

// Copy array
let copy = [...arr];
console.log(copy); // [1, 2, 3]

// Combine arrays
let arr2 = [4, 5];
let combined = [...arr, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5]

// Add elements
let newArr = [0, ...arr, 4, 5];
console.log(newArr); // [0, 1, 2, 3, 4, 5]

// As function arguments
let nums = [1, 2, 3];
console.log(Math.max(...nums)); // 3
```

---

## ⚠️ Common Confusions

### ❌ splice vs slice

```javascript
let arr = [1, 2, 3, 4, 5];

// splice MODIFIES original
arr.splice(1, 2);
console.log(arr); // [1, 4, 5] - CHANGED

// slice DOESN'T modify
let arr2 = [1, 2, 3, 4, 5];
arr2.slice(1, 3);
console.log(arr2); // [1, 2, 3, 4, 5] - unchanged
```

### ❌ forEach vs map

```javascript
let nums = [1, 2, 3];

// forEach - no return
let result1 = nums.forEach(n => n * 2);
console.log(result1); // undefined

// map - returns new array
let result2 = nums.map(n => n * 2);
console.log(result2); // [2, 4, 6]
```

### ❌ sort() with strings vs numbers

```javascript
// String sort (lexical)
let letters = ["c", "a", "b"];
letters.sort();
console.log(letters); // ["a", "b", "c"]

// Number sort (WRONG without compareFn)
let nums = [10, 2, 30, 5];
nums.sort();
console.log(nums); // [10, 2, 30, 5] - Wrong!

// Correct numeric sort
nums.sort((a, b) => a - b);
console.log(nums); // [2, 5, 10, 30]
```

---

## 🎯 Practical Examples

### Example 1: Student Grades

```javascript
let students = [
  { name: "John", marks: 85 },
  { name: "Sarah", marks: 92 },
  { name: "Mike", marks: 78 }
];

// Get top performer
let top = students.reduce((best, s) => 
  s.marks > best.marks ? s : best
);
console.log(top.name); // Sarah

// Average marks
let avg = students.reduce((sum, s) => sum + s.marks, 0) / students.length;
console.log(avg); // 85

// Pass/Fail (marks >= 80)
let passed = students.filter(s => s.marks >= 80);
console.log(passed.length); // 2
```

### Example 2: E-commerce Cart

```javascript
let cart = [
  { id: 1, name: "Laptop", price: 1000, qty: 1 },
  { id: 2, name: "Mouse", price: 25, qty: 2 },
  { id: 3, name: "Keyboard", price: 75, qty: 1 }
];

// Total price
let total = cart.reduce((sum, item) => 
  sum + (item.price * item.qty), 0
);
console.log(total); // 1225

// Remove item
cart = cart.filter(item => item.id !== 2);

// Update quantity
let laptopIndex = cart.findIndex(item => item.id === 1);
cart[laptopIndex].qty = 2;
```

### Example 3: Data Transformation

```javascript
let data = [
  { id: 1, temp: 30 },
  { id: 2, temp: 25 },
  { id: 3, temp: 35 }
];

// Convert to Fahrenheit
let fahrenheit = data.map(d => ({
  id: d.id,
  temp: (d.temp * 9/5) + 32
}));

// Filter high temps
let highTemps = fahrenheit.filter(d => d.temp > 80);
console.log(highTemps); // [30°C→86°F, 35°C→95°F]
```

---

## 📊 Array Methods Cheat Sheet

| Method | Modifies | Returns | Use When |
|--------|----------|---------|----------|
| push() | ✅ Yes | Number | Add to end |
| pop() | ✅ Yes | Element | Remove last |
| shift() | ✅ Yes | Element | Remove first |
| unshift() | ✅ Yes | Number | Add to start |
| splice() | ✅ Yes | Array | Add/remove anywhere |
| reverse() | ✅ Yes | Array | Reverse order |
| sort() | ✅ Yes | Array | Sort items |
| slice() | ❌ No | Array | Copy portion |
| map() | ❌ No | Array | Transform each |
| filter() | ❌ No | Array | Keep matching |
| reduce() | ❌ No | Value | Combine to single |
| forEach() | ❌ No | undefined | Execute for each |
| find() | ❌ No | Element | Find first |
| some() | ❌ No | Boolean | At least one? |
| every() | ❌ No | Boolean | All match? |

---

## 🧠 Mindset

**Arrays = Structured, Transformable Data**

Think of arrays as pipelines:
1. **Collect** data into array
2. **Transform** with map/filter
3. **Extract** with find/reduce
4. **Output** result to UI/logic

```javascript
// Pipeline example
let result = data
  .filter(item => item.active)     // Keep active items
  .map(item => item.value * 1.1)   // Apply 10% increase
  .reduce((sum, val) => sum + val) // Get total
```

Arrays are powerful when you chain methods. Master them to control data flow in your applications! 🚀

---

**Practice array methods daily to become a JavaScript master! 💪**
