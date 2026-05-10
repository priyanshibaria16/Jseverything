# 🔄 Loops - Complete Guide

Master loops to repeat code efficiently. The backbone of data processing.

---

## 📚 Quick Contents

1. [Why Loops?](#why-loops)
2. [for Loop](#for-loop)
3. [while & do-while](#while--do-while)
4. [break & continue](#break--continue)
5. [for-of Loop](#for-of-loop)
6. [forEach Method](#foreach-method)
7. [for-in Loop](#for-in-loop)
8. [Common Confusions](#common-confusions)
9. [Practical Examples](#practical-examples)

---

## ❓ Why Loops?

Loops help repeat code without rewriting it. Perfect for:
- **Printing numbers**: 1 to 100
- **Processing arrays**: Go through each element
- **Checking strings**: Examine each character
- **Counting**: Until a condition is met

```javascript
// WITHOUT loop - repetitive and error-prone
console.log(1);
console.log(2);
console.log(3);
// ... repeat 97 more times!

// WITH loop - clean and scalable
for (let i = 1; i <= 100; i++) {
  console.log(i);
}
```

---

## 🔁 for Loop

**Best for**: Known number of iterations (arrays, counting).

**Syntax**: `for (initialization; condition; increment)`

```javascript
// Count from 0 to 4
for (let i = 0; i < 5; i++) {
  console.log(i);
}
// Output: 0, 1, 2, 3, 4

// Count from 1 to 10
for (let i = 1; i <= 10; i++) {
  console.log(i);
}

// Count backwards
for (let i = 5; i >= 1; i--) {
  console.log(i);
}
// Output: 5, 4, 3, 2, 1

// Skip by 2
for (let i = 0; i < 10; i += 2) {
  console.log(i);
}
// Output: 0, 2, 4, 6, 8
```

**Loop through array**:
```javascript
const fruits = ["apple", "banana", "orange"];

for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
// Output: apple, banana, orange
```

**Nested loops** (loop within loop):
```javascript
// Multiplication table
for (let i = 1; i <= 3; i++) {
  for (let j = 1; j <= 3; j++) {
    console.log(`${i} × ${j} = ${i * j}`);
  }
}

// Print 3×3 grid
for (let row = 1; row <= 3; row++) {
  for (let col = 1; col <= 3; col++) {
    process.stdout.write(col + " ");
  }
  console.log(); // New line
}
// Output:
// 1 2 3
// 1 2 3
// 1 2 3
```

---

## 🔁 while & do-while

### while Loop

**Condition is checked BEFORE running**.

```javascript
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
// Output: 0, 1, 2, 3, 4

// Real example: Count down
let countdown = 5;
while (countdown > 0) {
  console.log("Launching in " + countdown);
  countdown--;
}
console.log("Blastoff!");

// Process until condition is met
let sum = 0;
let num = 1;
while (sum < 100) {
  sum += num;
  num++;
}
console.log("Reached sum:", sum); // 105
```

### do-while Loop

**Runs AT LEAST ONCE, even if condition is false**.

```javascript
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
// Output: 0, 1, 2, 3, 4

// Difference: Condition false from start
let x = 10;

// while - never runs
while (x < 5) {
  console.log("This never prints");
}

// do-while - runs once
do {
  console.log("This prints once"); // Prints!
} while (x < 5);
```

**Real example: User input validation**:
```javascript
// In actual browser with prompt():
let password = "";
do {
  password = prompt("Enter password (min 5 chars):");
} while (password.length < 5);
console.log("Password accepted!");
```

### When to Use
- **for**: Known iterations (arrays, counters)
- **while**: Unknown iterations (check until condition)
- **do-while**: Run at least once, then check

```javascript
// while vs do-while
let attempts = 0;

// while - might never run
while (attempts > 5) {
  console.log("Over limit");
}

// do-while - always runs at least once
do {
  attempts++;
  console.log("Attempt " + attempts); // Prints once
} while (attempts > 5);
```

---

## ⛔ break & continue

### break
**Exit loop completely**.

```javascript
for (let i = 0; i < 10; i++) {
  if (i === 5) break; // Exit loop
  console.log(i);
}
// Output: 0, 1, 2, 3, 4

// Find first even number
for (let i = 1; i <= 100; i++) {
  if (i % 2 === 0) {
    console.log("First even: " + i);
    break;
  }
}
// Output: First even: 2
```

### continue
**Skip current iteration, move to next**.

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) continue; // Skip this iteration
  console.log(i);
}
// Output: 0, 1, 3, 4

// Skip even numbers
for (let i = 1; i <= 10; i++) {
  if (i % 2 === 0) continue;
  console.log(i);
}
// Output: 1, 3, 5, 7, 9
```

### Practical Examples
```javascript
// Find sum of numbers until we hit negative
let sum = 0;
const numbers = [1, 2, 3, -1, 4, 5];

for (let num of numbers) {
  if (num < 0) break; // Stop at negative
  sum += num;
}
console.log(sum); // 6

// Skip empty strings in array
const items = ["apple", "", "banana", "", "orange"];

for (let item of items) {
  if (item === "") continue; // Skip empty
  console.log(item);
}
// Output: apple, banana, orange
```

---

## 🌀 for-of Loop

**Best for**: Array values and strings. Can use break/continue.

```javascript
// Loop through array values
const fruits = ["apple", "banana", "orange"];

for (let fruit of fruits) {
  console.log(fruit);
}
// Output: apple, banana, orange

// Loop through string characters
for (let char of "Hello") {
  console.log(char);
}
// Output: H, e, l, l, o

// With break/continue (unlike forEach)
const numbers = [1, 2, 3, 4, 5];
for (let num of numbers) {
  if (num === 3) break; // Works!
  console.log(num);
}
// Output: 1, 2
```

**With index** (if needed):
```javascript
const arr = ["a", "b", "c"];

for (let [index, value] of arr.entries()) {
  console.log(index, value);
}
// Output:
// 0 a
// 1 b
// 2 c
```

---

## 🧱 forEach Method

**Best for**: Simple array iteration (cleaner syntax).

⚠️ **Limitation**: Can't use break or continue, can't stop early.

```javascript
const nums = [10, 20, 30];

nums.forEach((num) => {
  console.log(num);
});
// Output: 10, 20, 30

// With index
nums.forEach((num, index) => {
  console.log(`[${index}] = ${num}`);
});
// Output:
// [0] = 10
// [1] = 20
// [2] = 30

// With array parameter
nums.forEach((num, index, array) => {
  console.log(array);
});
```

**forEach vs for-of**:
```javascript
const arr = [1, 2, 3];

// forEach - can't break/continue
arr.forEach((num) => {
  // if (num === 2) break; // ERROR!
  // if (num === 2) continue; // ERROR!
  console.log(num);
});

// for-of - can break/continue
for (let num of arr) {
  if (num === 2) continue; // Works!
  console.log(num);
}
```

---

## 🧱 for-in Loop

**Best for**: Object keys. Also works on arrays (but not recommended).

```javascript
// Loop through object keys
const person = { name: "John", age: 30, city: "NYC" };

for (let key in person) {
  console.log(key + ": " + person[key]);
}
// Output:
// name: John
// age: 30
// city: NYC

// Array iteration (not recommended)
const arr = ["a", "b", "c"];

for (let index in arr) {
  console.log(index, arr[index]);
}
// Output:
// 0 a
// 1 b
// 2 c
```

⚠️ **Problem with for-in on arrays**:
```javascript
const arr = [10, 20, 30];
arr.newProperty = "unexpected";

for (let index in arr) {
  console.log(index); // 0, 1, 2, newProperty
  // Includes unexpected properties!
}
```

**Use for-of for arrays, for-in for objects**:
```javascript
// ✅ CORRECT
for (let key in { a: 1, b: 2 }) console.log(key); // for objects
for (let value of [1, 2, 3]) console.log(value); // for arrays

// ❌ WRONG
for (let value in [1, 2, 3]) console.log(value); // Gets indexes, not values
for (let key of { a: 1, b: 2 }) console.log(key); // Error!
```

---

## ⚠️ Common Confusions

### ❌ Forgetting increment (Infinite loop)
```javascript
// WRONG - i++ is missing
for (let i = 0; i < 5; ) {
  console.log(i); // Runs forever!
}

// CORRECT
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### ❌ for-in on arrays
```javascript
// WRONG - gets indexes and unexpected properties
for (let item in [10, 20, 30]) {
  console.log(item); // 0, 1, 2 (indexes, not values)
}

// CORRECT - use for-of
for (let item of [10, 20, 30]) {
  console.log(item); // 10, 20, 30 (values)
}
```

### ❌ Using break/continue in forEach
```javascript
// WRONG - causes error
[1, 2, 3].forEach((num) => {
  if (num === 2) break; // SyntaxError!
});

// CORRECT - use for-of
for (let num of [1, 2, 3]) {
  if (num === 2) break; // Works!
}
```

### ❌ Infinite while loops
```javascript
// WRONG - will run forever
while (true) {
  console.log("Infinite!");
}

// CORRECT - add exit condition
let count = 0;
while (count < 5) {
  console.log(count);
  count++;
}
```

### ❌ Array length in loop
```javascript
// If you modify array inside loop, be careful
const arr = [1, 2, 3];

for (let i = 0; i < arr.length; i++) {
  arr.push(4); // Adds element
  // Loop might run longer than expected!
}
```

---

## 🎯 Practical Examples

### Example 1: Sum of numbers
```javascript
// Using for
let sum = 0;
for (let i = 1; i <= 100; i++) {
  sum += i;
}
console.log(sum); // 5050

// Using while
let sum2 = 0, num = 1;
while (num <= 100) {
  sum2 += num;
  num++;
}
console.log(sum2); // 5050
```

### Example 2: Count vowels
```javascript
function countVowels(str) {
  let count = 0;
  for (let char of str.toLowerCase()) {
    if ("aeiou".includes(char)) count++;
  }
  return count;
}

console.log(countVowels("Hello World")); // 3
```

### Example 3: Find item in array
```javascript
const items = ["apple", "banana", "orange"];
const searchFor = "banana";

for (let item of items) {
  if (item === searchFor) {
    console.log("Found: " + item);
    break;
  }
}
```

### Example 4: Reverse array
```javascript
const arr = [1, 2, 3, 4, 5];

for (let i = arr.length - 1; i >= 0; i--) {
  console.log(arr[i]);
}
// Output: 5, 4, 3, 2, 1
```

### Example 5: Object properties
```javascript
const user = {
  name: "John",
  age: 30,
  email: "john@example.com"
};

for (let key in user) {
  console.log(key + ": " + user[key]);
}
// Output:
// name: John
// age: 30
// email: john@example.com
```

---

## 📊 Loop Comparison Table

| Loop | Use For | Break/Continue | Example |
|------|---------|---|---------|
| **for** | Known iterations | ✅ Yes | `for (let i = 0; i < 10; i++)` |
| **while** | Unknown iterations | ✅ Yes | Check until condition |
| **do-while** | Run at least once | ✅ Yes | User input validation |
| **for-of** | Array values | ✅ Yes | `for (let val of arr)` |
| **forEach** | Array processing | ❌ No | Clean array iteration |
| **for-in** | Object keys | ✅ Yes | `for (let key in obj)` |

---

## 🧠 Mindset

**Loops = Data Processor**

Choose the right loop for the job:
- **for** → Array index, counting (1, 2, 3...)
- **for-of** → Array values directly
- **for-in** → Object keys
- **while** → Unknown end condition
- **do-while** → Must run at least once
- **forEach** → Simple, clean array processing

```javascript
// Same result, different approaches

// 1. for (classic)
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// 2. for-of (modern, clean)
for (let item of arr) {
  console.log(item);
}

// 3. forEach (functional)
arr.forEach(item => console.log(item));
```

---

**Practice These: Print multiples of 3 up to 30, count characters in a string, find max number in array, reverse a string, print pattern (pyramid). 🚀**
