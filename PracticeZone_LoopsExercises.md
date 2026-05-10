# 🧪 Practice Zone - Loops Exercises

11 practical loop exercises with complete solutions and explanations.

---

## 1️⃣ Print 1 to 10 Using for

**Problem**: Print numbers from 1 to 10.

```javascript
// Basic solution
for (let i = 1; i <= 10; i++) {
  console.log(i);
}
// Output: 1 2 3 4 5 6 7 8 9 10

// Alternative: Store in array
let numbers = [];
for (let i = 1; i <= 10; i++) {
  numbers.push(i);
}
console.log(numbers);
// Output: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// With string concatenation
let result = "";
for (let i = 1; i <= 10; i++) {
  result += i + " ";
}
console.log(result);
// Output: "1 2 3 4 5 6 7 8 9 10 "
```

---

## 2️⃣ Print Even Numbers Between 1 to 20

**Problem**: Print only even numbers (2, 4, 6...) from 1 to 20.

```javascript
// Method 1: Using if condition
for (let i = 1; i <= 20; i++) {
  if (i % 2 === 0) {
    console.log(i);
  }
}
// Output: 2 4 6 8 10 12 14 16 18 20

// Method 2: Increment by 2
for (let i = 2; i <= 20; i += 2) {
  console.log(i);
}
// Output: 2 4 6 8 10 12 14 16 18 20

// Method 3: Using array filter
const numbers = [];
for (let i = 1; i <= 20; i++) {
  if (i % 2 === 0) numbers.push(i);
}
console.log(numbers);
// Output: [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]
```

---

## 3️⃣ Reverse a String Using Loop

**Problem**: Reverse a string without using built-in reverse() method.

```javascript
// Method 1: for loop (backwards)
const str = "Hello";
let reversed = "";

for (let i = str.length - 1; i >= 0; i--) {
  reversed += str[i];
}
console.log(reversed);
// Output: "olleH"

// Method 2: for-of with array
const str2 = "JavaScript";
let reversed2 = "";

for (let char of str2) {
  reversed2 = char + reversed2; // Add to front
}
console.log(reversed2);
// Output: "tpircSavaJ"

// Method 3: Function for reusability
function reverseString(str) {
  let result = "";
  for (let i = str.length - 1; i >= 0; i--) {
    result += str[i];
  }
  return result;
}

console.log(reverseString("Loops"));      // "spoоL"
console.log(reverseString("Hello World")); // "dlroW olleH"

// Method 4: Using array reverse
function reverseStringV2(str) {
  return str.split('').reverse().join('');
}
console.log(reverseStringV2("Hello")); // "olleH"
```

---

## 4️⃣ Object Iteration with for-in

**Problem**: Print all object keys and values.

```javascript
const user = { name: "Harsh", age: 26 };

for (let key in user) {
  console.log(key, user[key]);
}
// Output:
// name Harsh
// age 26

// Extended example
const person = {
  name: "John",
  age: 30,
  city: "New York",
  email: "john@example.com"
};

for (let key in person) {
  console.log(`${key}: ${person[key]}`);
}
// Output:
// name: John
// age: 30
// city: New York
// email: john@example.com

// Function to display object nicely
function displayObject(obj) {
  for (let key in obj) {
    console.log(`${key.toUpperCase()}: ${obj[key]}`);
  }
}

displayObject(user);
// Output:
// NAME: Harsh
// AGE: 26
```

---

## 5️⃣ Sum of All Numbers in an Array

**Problem**: Calculate the sum of all numbers in an array.

```javascript
// Method 1: for loop
const numbers = [10, 20, 30, 40, 50];
let sum = 0;

for (let i = 0; i < numbers.length; i++) {
  sum += numbers[i];
}
console.log(sum);
// Output: 150

// Method 2: for-of loop
const numbers2 = [5, 15, 25, 35];
let sum2 = 0;

for (let num of numbers2) {
  sum2 += num;
}
console.log(sum2);
// Output: 80

// Method 3: Function
function sumArray(arr) {
  let total = 0;
  for (let num of arr) {
    total += num;
  }
  return total;
}

console.log(sumArray([1, 2, 3, 4, 5]));        // 15
console.log(sumArray([100, 200, 300]));        // 600
console.log(sumArray([10, 20, 30, 40, 50]));   // 150

// Method 4: forEach
const arr = [7, 14, 21, 28];
let sum4 = 0;
arr.forEach(num => {
  sum4 += num;
});
console.log(sum4);
// Output: 70
```

---

## 6️⃣ Print All Characters of a Name Using for-of

**Problem**: Print each character of a string on a new line.

```javascript
// Method 1: Simple for-of
const name = "JavaScript";

for (let char of name) {
  console.log(char);
}
// Output:
// J
// a
// v
// a
// S
// c
// r
// i
// p
// t

// Method 2: With index (using entries)
const name2 = "Harsh";

for (let [index, char] of name2.split('').entries()) {
  console.log(`Position ${index}: ${char}`);
}
// Output:
// Position 0: H
// Position 1: a
// Position 2: r
// Position 3: s
// Position 4: h

// Method 3: Function
function printCharacters(str) {
  for (let char of str) {
    console.log(char);
  }
}

printCharacters("Code");
// Output: C o d e (each on new line)

// Method 4: With count
function printCharactersWithCount(str) {
  let count = 0;
  for (let char of str) {
    count++;
    console.log(`${count}: ${char}`);
  }
}

printCharactersWithCount("Hi");
// Output:
// 1: H
// 2: i
```

---

## 7️⃣ Print All Object Keys and Values Using for-in

**Problem**: Display all properties of an object in a formatted way.

```javascript
// Basic example
const product = {
  name: "Laptop",
  price: 50000,
  brand: "Dell",
  inStock: true
};

for (let key in product) {
  console.log(`${key}: ${product[key]}`);
}
// Output:
// name: Laptop
// price: 50000
// brand: Dell
// inStock: true

// Formatted table style
function printObjectTable(obj) {
  console.log("--- Object Properties ---");
  for (let key in obj) {
    console.log(`| ${key.padEnd(15)} | ${obj[key]} |`);
  }
}

printObjectTable({ name: "John", age: 30, city: "NYC" });
// Output:
// --- Object Properties ---
// | name           | John |
// | age            | 30 |
// | city           | NYC |

// Nested objects
const user = {
  name: "Alice",
  contact: { email: "alice@example.com", phone: "123-456" },
  role: "Admin"
};

for (let key in user) {
  if (typeof user[key] === 'object') {
    console.log(`${key}:`);
    for (let subkey in user[key]) {
      console.log(`  - ${subkey}: ${user[key][subkey]}`);
    }
  } else {
    console.log(`${key}: ${user[key]}`);
  }
}
// Output:
// name: Alice
// contact:
//   - email: alice@example.com
//   - phone: 123-456
// role: Admin
```

---

## 8️⃣ Use continue to Skip a Specific Number

**Problem**: Print numbers but skip a specific number using continue.

```javascript
// Skip 5
for (let i = 1; i <= 10; i++) {
  if (i === 5) {
    continue; // Skip 5
  }
  console.log(i);
}
// Output: 1 2 3 4 6 7 8 9 10

// Skip odd numbers
for (let i = 1; i <= 10; i++) {
  if (i % 2 !== 0) {
    continue; // Skip odd
  }
  console.log(i);
}
// Output: 2 4 6 8 10

// Skip multiple numbers
const skipNumbers = [3, 5, 7];
for (let i = 1; i <= 10; i++) {
  if (skipNumbers.includes(i)) {
    continue; // Skip if in array
  }
  console.log(i);
}
// Output: 1 2 4 6 8 9 10

// Function: Print with exclusions
function printWithSkip(start, end, skipList) {
  for (let i = start; i <= end; i++) {
    if (skipList.includes(i)) {
      continue;
    }
    console.log(i);
  }
}

printWithSkip(1, 15, [5, 10, 13]);
// Output: 1 2 3 4 6 7 8 9 11 12 14 15
```

---

## 9️⃣ Guess Number Game – Use while

**Problem**: Computer picks a number, user guesses until correct using while loop.

```javascript
// Simple version (simulated guessing)
function guessNumberGame() {
  const secretNumber = 7;
  let guess = 0;
  let attempts = 0;

  while (guess !== secretNumber) {
    attempts++;
    guess = Math.floor(Math.random() * 10) + 1; // Random 1-10
    
    if (guess < secretNumber) {
      console.log(`Attempt ${attempts}: ${guess} is too low`);
    } else if (guess > secretNumber) {
      console.log(`Attempt ${attempts}: ${guess} is too high`);
    } else {
      console.log(`Attempt ${attempts}: ${guess} is correct! You won!`);
    }
  }

  return attempts;
}

// guessNumberGame();

// Interactive version (for browser with prompt)
function interactiveGuessGame() {
  const secretNumber = Math.floor(Math.random() * 100) + 1;
  let guess = null;
  let attempts = 0;

  while (guess !== secretNumber) {
    guess = parseInt(prompt("Guess a number (1-100):"));
    attempts++;

    if (isNaN(guess)) {
      console.log("Please enter a valid number");
      continue;
    }

    if (guess < secretNumber) {
      console.log(`Too low! Attempts: ${attempts}`);
    } else if (guess > secretNumber) {
      console.log(`Too high! Attempts: ${attempts}`);
    } else {
      console.log(`Correct! You won in ${attempts} attempts!`);
    }
  }
}

// Advanced: Limit attempts
function guessGameWithLimit() {
  const secretNumber = 5;
  let guess = null;
  let attempts = 0;
  const maxAttempts = 5;

  while (attempts < maxAttempts) {
    guess = Math.floor(Math.random() * 10) + 1;
    attempts++;
    
    console.log(`Attempt ${attempts}: Guessed ${guess}`);

    if (guess === secretNumber) {
      console.log(`Won in ${attempts} attempts!`);
      break; // Exit loop
    }
  }

  if (guess !== secretNumber) {
    console.log(`Game over! Secret was ${secretNumber}`);
  }
}

guessGameWithLimit();
```

---

## 🔟 Pattern: Print Triangle Using *

**Problem**: Print a triangle pattern using asterisks.

```javascript
// Triangle (height = 5)
//     *
//    **
//   ***
//  ****
// *****

function printTriangle(rows) {
  for (let i = 1; i <= rows; i++) {
    let spaces = " ".repeat(rows - i);
    let stars = "*".repeat(i);
    console.log(spaces + stars);
  }
}

printTriangle(5);

// Right-aligned triangle
function printRightTriangle(rows) {
  for (let i = 1; i <= rows; i++) {
    console.log("*".repeat(i));
  }
}

printRightTriangle(4);
// Output:
// *
// **
// ***
// ****

// Inverted triangle
function printInvertedTriangle(rows) {
  for (let i = rows; i >= 1; i--) {
    console.log("*".repeat(i));
  }
}

printInvertedTriangle(4);
// Output:
// ****
// ***
// **
// *

// Diamond pattern
function printDiamond(rows) {
  // Upper half
  for (let i = 1; i <= rows; i++) {
    let spaces = " ".repeat(rows - i);
    let stars = "*".repeat(2 * i - 1);
    console.log(spaces + stars);
  }
  
  // Lower half
  for (let i = rows - 1; i >= 1; i--) {
    let spaces = " ".repeat(rows - i);
    let stars = "*".repeat(2 * i - 1);
    console.log(spaces + stars);
  }
}

printDiamond(4);
// Output:
//    *
//   ***
//  *****
// *******
//  *****
//   ***
//    *
```

---

## 1️⃣1️⃣ Sum of Even Numbers in an Array Using forEach

**Problem**: Calculate sum of only even numbers using forEach.

```javascript
// Basic solution
const numbers = [10, 15, 20, 25, 30, 35, 40];
let sum = 0;

numbers.forEach(num => {
  if (num % 2 === 0) {
    sum += num;
  }
});

console.log(sum);
// Output: 100 (10 + 20 + 30 + 40)

// With index
const arr = [1, 2, 3, 4, 5, 6];
let evenSum = 0;

arr.forEach((num, index) => {
  if (num % 2 === 0) {
    console.log(`Index ${index}: ${num}`);
    evenSum += num;
  }
});

console.log("Sum of evens:", evenSum);
// Output:
// Index 1: 2
// Index 3: 4
// Index 5: 6
// Sum of evens: 12

// Function for reusability
function sumEvenNumbers(arr) {
  let total = 0;
  arr.forEach(num => {
    if (num % 2 === 0) {
      total += num;
    }
  });
  return total;
}

console.log(sumEvenNumbers([1, 2, 3, 4, 5, 6]));           // 12
console.log(sumEvenNumbers([10, 20, 30, 40, 50]));         // 150
console.log(sumEvenNumbers([11, 13, 15, 17, 19]));         // 0 (no evens)

// Advanced: Count even and sum
function analyzeArray(arr) {
  let evenSum = 0;
  let oddSum = 0;
  let evenCount = 0;
  let oddCount = 0;

  arr.forEach(num => {
    if (num % 2 === 0) {
      evenSum += num;
      evenCount++;
    } else {
      oddSum += num;
      oddCount++;
    }
  });

  return {
    evenSum: evenSum,
    oddSum: oddSum,
    evenCount: evenCount,
    oddCount: oddCount,
    average: (evenSum / evenCount).toFixed(2)
  };
}

console.log(analyzeArray([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]));
// Output:
// {
//   evenSum: 30,
//   oddSum: 25,
//   evenCount: 5,
//   oddCount: 5,
//   average: '6.00'
// }
```

---

## 🎯 Challenge Yourself

Try these variations:

1. **Prime numbers**: Print all prime numbers 1-50
2. **Fibonacci**: Print first 10 Fibonacci numbers
3. **Multiplication table**: Print table for multiple numbers
4. **Word pattern**: Print word pyramid
5. **Array operations**: Sum, average, max, min in one loop
6. **Palindrome checker**: Check if string is palindrome using loop
7. **Count occurrences**: Count how many times a number appears in array

---

## 📊 Quick Reference

| Exercise | Best Loop | Key Concept |
|----------|-----------|-------------|
| 1-10 numbers | for | Basic counting |
| Even numbers | for | Conditional check |
| Reverse string | for backwards | Decrement loop |
| Object iteration | for-in | Object keys |
| Array sum | for-of | Array values |
| String characters | for-of | Iterate string |
| Object properties | for-in | Key-value pairs |
| Continue usage | for | Skip iteration |
| Guess game | while | Unknown iterations |
| Patterns | for nested | Nested loops |
| Even sum | forEach | Array method |

---

**Keep practicing! These exercises build loop mastery. 🚀**
