# 🧪 Practice Zone - Arrays Exercises

11 practical array exercises with complete solutions and explanations.

---

## 1️⃣ Create an Array of Student Names and Print Each

**Problem**: Create array of student names and print each one.

```javascript
// Create array
let students = ["John", "Sarah", "Mike", "Emma", "David"];

// Method 1: for loop
for (let i = 0; i < students.length; i++) {
  console.log(students[i]);
}

// Method 2: for-of loop
for (let student of students) {
  console.log(student);
}

// Method 3: forEach
students.forEach(student => {
  console.log(student);
});

// Method 4: forEach with index
students.forEach((student, index) => {
  console.log(`${index + 1}. ${student}`);
});
// Output:
// 1. John
// 2. Sarah
// 3. Mike
// 4. Emma
// 5. David

// Method 5: map (transform while printing)
students.map((student, i) => {
  console.log(`Student ${i + 1}: ${student}`);
  return student;
});

// Print formatted
function printStudents(arr) {
  arr.forEach((student, idx) => {
    console.log(`${idx + 1}. ${student.toUpperCase()}`);
  });
}

printStudents(students);
// Output:
// 1. JOHN
// 2. SARAH
// 3. MIKE
// 4. EMMA
// 5. DAVID
```

---

## 2️⃣ Filter Even Numbers from an Array

**Problem**: Keep only even numbers from an array.

```javascript
// Basic filter
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evens = numbers.filter(n => n % 2 === 0);
console.log(evens); // [2, 4, 6, 8, 10]

// Original unchanged
console.log(numbers); // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

// With condition variable
const isEven = n => n % 2 === 0;
let evens2 = numbers.filter(isEven);
console.log(evens2); // [2, 4, 6, 8, 10]

// Filter and print
function printEvens(arr) {
  let evens = arr.filter(n => n % 2 === 0);
  evens.forEach(n => console.log(n));
}

printEvens([1, 2, 3, 4, 5]);
// Output: 2, 4

// Filter multiple conditions
let nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let evenAndGreater5 = nums.filter(n => n % 2 === 0 && n > 5);
console.log(evenAndGreater5); // [6, 8, 10]

// Count evens
let countEvens = numbers.filter(n => n % 2 === 0).length;
console.log(countEvens); // 5

// Separate into odds and evens
let odds = numbers.filter(n => n % 2 !== 0);
console.log(odds); // [1, 3, 5, 7, 9]
```

---

## 3️⃣ Map Prices to Include GST (18%)

**Problem**: Add 18% GST to prices and create new array.

```javascript
// Basic map
let prices = [100, 200, 300, 150];
let pricesWithGST = prices.map(p => p * 1.18);
console.log(pricesWithGST); // [118, 236, 354, 177]

// Original unchanged
console.log(prices); // [100, 200, 300, 150]

// Rounded to 2 decimals
let withGST = prices.map(p => parseFloat((p * 1.18).toFixed(2)));
console.log(withGST); // [118, 236, 354, 177]

// Return object with original and GST
let priceBreakdown = prices.map(p => ({
  original: p,
  gst: parseFloat((p * 0.18).toFixed(2)),
  total: parseFloat((p * 1.18).toFixed(2))
}));

console.log(priceBreakdown);
// [
//   { original: 100, gst: 18, total: 118 },
//   { original: 200, gst: 36, total: 236 },
//   { original: 300, gst: 54, total: 354 },
//   { original: 150, gst: 27, total: 177 }
// ]

// Function to apply GST
function applyGST(prices, gstRate = 0.18) {
  return prices.map(price => {
    const gstAmount = price * gstRate;
    const total = price + gstAmount;
    return {
      price: price,
      gst: parseFloat(gstAmount.toFixed(2)),
      total: parseFloat(total.toFixed(2))
    };
  });
}

console.log(applyGST([100, 200, 300]));

// With item names
let items = [
  { name: "Laptop", price: 50000 },
  { name: "Mouse", price: 500 },
  { name: "Keyboard", price: 1500 }
];

let itemsWithGST = items.map(item => ({
  ...item,
  gst: parseFloat((item.price * 0.18).toFixed(2)),
  totalPrice: parseFloat((item.price * 1.18).toFixed(2))
}));

console.log(itemsWithGST);
// [
//   { name: "Laptop", price: 50000, gst: 9000, totalPrice: 59000 },
//   { name: "Mouse", price: 500, gst: 90, totalPrice: 590 },
//   { name: "Keyboard", price: 1500, gst: 270, totalPrice: 1770 }
// ]
```

---

## 4️⃣ Reduce Salaries to Calculate Total Payroll

**Problem**: Sum all salaries using reduce method.

```javascript
// Basic reduce
let salaries = [50000, 60000, 75000, 55000];
let total = salaries.reduce((sum, salary) => sum + salary, 0);
console.log(total); // 240000

// With accumulator explanation
let total2 = salaries.reduce((accumulator, currentValue) => {
  console.log(`Adding ${currentValue} to ${accumulator}`);
  return accumulator + currentValue;
}, 0);

// Calculate statistics
let salaryStats = salaries.reduce((stats, salary) => {
  stats.total += salary;
  stats.count++;
  stats.average = stats.total / stats.count;
  stats.max = Math.max(stats.max, salary);
  stats.min = Math.min(stats.min, salary);
  return stats;
}, { total: 0, count: 0, average: 0, max: 0, min: Infinity });

console.log(salaryStats);
// {
//   total: 240000,
//   count: 4,
//   average: 60000,
//   max: 75000,
//   min: 50000
// }

// With department info
let employees = [
  { name: "John", dept: "IT", salary: 50000 },
  { name: "Sarah", dept: "HR", salary: 60000 },
  { name: "Mike", dept: "IT", salary: 75000 },
  { name: "Emma", dept: "HR", salary: 55000 }
];

// Total payroll
let totalPayroll = employees.reduce((sum, emp) => sum + emp.salary, 0);
console.log(totalPayroll); // 240000

// Payroll by department
let payrollByDept = employees.reduce((depts, emp) => {
  depts[emp.dept] = depts[emp.dept] || 0;
  depts[emp.dept] += emp.salary;
  return depts;
}, {});

console.log(payrollByDept);
// { IT: 125000, HR: 115000 }

// Count employees per department
let deptInfo = employees.reduce((info, emp) => {
  info[emp.dept] = info[emp.dept] || { count: 0, totalSalary: 0 };
  info[emp.dept].count++;
  info[emp.dept].totalSalary += emp.salary;
  return info;
}, {});

console.log(deptInfo);
// {
//   IT: { count: 2, totalSalary: 125000 },
//   HR: { count: 2, totalSalary: 115000 }
// }
```

---

## 5️⃣ Find the First Student with Grade A

**Problem**: Find first student with grade A using find method.

```javascript
// With grades array
let grades = [
  { name: "John", grade: "B" },
  { name: "Sarah", grade: "A" },
  { name: "Mike", grade: "A" },
  { name: "Emma", grade: "C" }
];

// Find first A
let firstA = grades.find(student => student.grade === "A");
console.log(firstA); // { name: "Sarah", grade: "A" }

// Find with string array
let studentGrades = [
  { name: "Alice", marks: 85 },
  { name: "Bob", marks: 92 },
  { name: "Charlie", marks: 78 }
];

let aGrade = studentGrades.find(s => s.marks >= 90);
console.log(aGrade); // { name: "Bob", marks: 92 }

// Multiple conditions
let result = grades.find(s => s.grade === "A" && s.name.startsWith("S"));
console.log(result); // { name: "Sarah", grade: "A" }

// Not found returns undefined
let notFound = grades.find(s => s.grade === "F");
console.log(notFound); // undefined

// Check if found
let student = grades.find(s => s.grade === "A");
if (student) {
  console.log(`${student.name} has grade A`);
} else {
  console.log("No student with grade A");
}

// Find and return specific property
let firstAName = (grades.find(s => s.grade === "A") || {}).name;
console.log(firstAName); // "Sarah"

// Function wrapper
function findFirstGrade(students, targetGrade) {
  return students.find(s => s.grade === targetGrade);
}

console.log(findFirstGrade(grades, "A")); // Sarah's object
console.log(findFirstGrade(grades, "F")); // undefined
```

---

## 6️⃣ Write a Function to Reverse an Array

**Problem**: Reverse array using different methods.

```javascript
// Method 1: Using reverse() method
let arr1 = [1, 2, 3, 4, 5];
arr1.reverse();
console.log(arr1); // [5, 4, 3, 2, 1]

// Method 2: Don't modify original
let arr2 = [1, 2, 3, 4, 5];
let reversed = [...arr2].reverse();
console.log(reversed); // [5, 4, 3, 2, 1]
console.log(arr2); // [1, 2, 3, 4, 5] - unchanged

// Method 3: Using slice and reverse
let arr3 = [1, 2, 3, 4, 5];
let reversed2 = arr3.slice().reverse();
console.log(reversed2); // [5, 4, 3, 2, 1]

// Method 4: Manual reverse function
function reverseArray(arr) {
  let result = [];
  for (let i = arr.length - 1; i >= 0; i--) {
    result.push(arr[i]);
  }
  return result;
}

console.log(reverseArray([1, 2, 3])); // [3, 2, 1]

// Method 5: Using for loop (in-place)
function reverseInPlace(arr) {
  for (let i = 0; i < arr.length / 2; i++) {
    // Swap
    let temp = arr[i];
    arr[i] = arr[arr.length - 1 - i];
    arr[arr.length - 1 - i] = temp;
  }
  return arr;
}

let arr4 = [1, 2, 3, 4, 5];
console.log(reverseInPlace(arr4)); // [5, 4, 3, 2, 1]

// Method 6: Using reduce
function reverseWithReduce(arr) {
  return arr.reduce((reversed, item) => [item, ...reversed], []);
}

console.log(reverseWithReduce([1, 2, 3])); // [3, 2, 1]

// Method 7: Reverse strings
let str = "Hello";
let reversedStr = str.split('').reverse().join('');
console.log(reversedStr); // "olleH"
```

---

## 7️⃣ Sort Array of Ages in Ascending Order

**Problem**: Properly sort numbers (avoid lexical sort).

```javascript
// ❌ WRONG - Lexical sort
let ages1 = [10, 2, 30, 5, 15];
ages1.sort();
console.log(ages1); // [10, 15, 2, 30, 5] - WRONG ORDER!

// ✅ CORRECT - Numeric sort
let ages2 = [10, 2, 30, 5, 15];
ages2.sort((a, b) => a - b);
console.log(ages2); // [2, 5, 10, 15, 30]

// Don't modify original
let ages3 = [10, 2, 30, 5, 15];
let sorted = [...ages3].sort((a, b) => a - b);
console.log(sorted); // [2, 5, 10, 15, 30]
console.log(ages3); // [10, 2, 30, 5, 15] - unchanged

// Descending order
let descending = [...ages3].sort((a, b) => b - a);
console.log(descending); // [30, 15, 10, 5, 2]

// Sort objects by age property
let people = [
  { name: "John", age: 30 },
  { name: "Sarah", age: 25 },
  { name: "Mike", age: 35 },
  { name: "Emma", age: 28 }
];

// Ascending age
people.sort((a, b) => a.age - b.age);
console.log(people);
// [Sarah (25), Emma (28), John (30), Mike (35)]

// Descending age
people.sort((a, b) => b.age - a.age);
console.log(people);
// [Mike (35), John (30), Emma (28), Sarah (25)]

// Sort and print
function sortAndPrint(ages) {
  let sorted = [...ages].sort((a, b) => a - b);
  sorted.forEach((age, i) => {
    console.log(`${i + 1}. ${age} years`);
  });
}

sortAndPrint([10, 2, 30, 5, 15]);
// Output:
// 1. 2 years
// 2. 5 years
// 3. 10 years
// 4. 15 years
// 5. 30 years
```

---

## 8️⃣ Destructure First Two Elements of an Array

**Problem**: Extract first two elements using destructuring.

```javascript
// Basic destructuring
let [first, second] = ["apple", "banana", "mango"];
console.log(first); // "apple"
console.log(second); // "banana"

// With numbers
let [a, b] = [10, 20, 30, 40];
console.log(a, b); // 10, 20

// Skip elements
let [head, , third] = ["a", "b", "c", "d"];
console.log(head, third); // "a", "c"

// Rest parameter
let [x, y, ...rest] = [1, 2, 3, 4, 5];
console.log(x, y); // 1, 2
console.log(rest); // [3, 4, 5]

// Default values
let [p, q = 0] = [5];
console.log(p, q); // 5, 0

// In function parameters
function printFirst(arr) {
  let [first, second] = arr;
  console.log(`First: ${first}, Second: ${second}`);
}

printFirst(["John", "Sarah", "Mike"]);
// "First: John, Second: Sarah"

// Destructure in function parameter
function greet([first, second]) {
  console.log(`${first} and ${second}`);
}

greet(["Alice", "Bob"]);
// "Alice and Bob"

// Swap variables using destructuring
let x1 = 10, y1 = 20;
[x1, y1] = [y1, x1];
console.log(x1, y1); // 20, 10

// Extract from returned array
function getCoordinates() {
  return [10, 20];
}

let [lat, lon] = getCoordinates();
console.log(lat, lon); // 10, 20
```

---

## 9️⃣ Use some() to Check if Any Student Failed

**Problem**: Check if any student has failing grade using some().

```javascript
// Basic some()
let students = [
  { name: "John", grade: "A" },
  { name: "Sarah", grade: "B" },
  { name: "Mike", grade: "F" },
  { name: "Emma", grade: "A" }
];

// Check if any failed
let anyFailed = students.some(s => s.grade === "F");
console.log(anyFailed); // true

// With marks
let marks = [
  { name: "Alice", marks: 85 },
  { name: "Bob", marks: 92 },
  { name: "Charlie", marks: 35 }
];

let anyFailing = marks.some(s => s.marks < 40);
console.log(anyFailing); // true

// No failures
let students2 = [
  { name: "John", grade: "A" },
  { name: "Sarah", grade: "B" },
  { name: "Mike", grade: "C" }
];

let hasFailures = students2.some(s => s.grade === "F");
console.log(hasFailures); // false

// Function wrapper
function hasAnyFailures(students, passingGrade = "D") {
  const passingGrades = ["A", "B", "C", "D"];
  return students.some(s => !passingGrades.includes(s.grade));
}

console.log(hasAnyFailures(students)); // true
console.log(hasAnyFailures(students2)); // false

// With numbers
function anyAboveThreshold(arr, threshold) {
  return arr.some(n => n > threshold);
}

console.log(anyAboveThreshold([1, 2, 3, 4], 3)); // true
console.log(anyAboveThreshold([1, 2, 3], 5)); // false

// All vs Some
let nums = [2, 4, 6, 8];
console.log(nums.some(n => n > 5)); // true (at least one)
console.log(nums.every(n => n > 5)); // false (not all)
```

---

## 🔟 Use Spread to Copy and Add New Item

**Problem**: Copy array and add new items using spread operator.

```javascript
// Copy and add single item
let arr = [1, 2, 3];
let newArr = [...arr, 4];
console.log(newArr); // [1, 2, 3, 4]
console.log(arr); // [1, 2, 3] - unchanged

// Add at beginning
let arr2 = [2, 3, 4];
let newArr2 = [1, ...arr2];
console.log(newArr2); // [1, 2, 3, 4]

// Add in middle
let arr3 = [1, 2, 4, 5];
let newArr3 = [1, 2, 3, ...arr3.slice(2)];
console.log(newArr3); // [1, 2, 3, 4, 5]

// Combine multiple arrays
let arr4 = [1, 2, 3];
let arr5 = [4, 5, 6];
let combined = [...arr4, ...arr5];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Add multiple items
let arr6 = [1, 2];
let arr7 = [...arr6, 3, 4, 5];
console.log(arr7); // [1, 2, 3, 4, 5]

// Spread with objects in array
let users = [
  { id: 1, name: "John" },
  { id: 2, name: "Sarah" }
];

let newUsers = [...users, { id: 3, name: "Mike" }];
console.log(newUsers);
// [
//   { id: 1, name: "John" },
//   { id: 2, name: "Sarah" },
//   { id: 3, name: "Mike" }
// ]

// Copy and modify
let original = [1, 2, 3];
let modified = [...original];
modified.push(4);
console.log(original); // [1, 2, 3] - unchanged
console.log(modified); // [1, 2, 3, 4]

// Deep copy (for nested arrays)
let nested = [[1, 2], [3, 4]];
let shallowCopy = [...nested]; // Only copies outer level
shallowCopy[0].push(99);
console.log(nested); // [[1, 2, 99], [3, 4]] - modified!

// Function to add items
function addItems(arr, ...items) {
  return [...arr, ...items];
}

console.log(addItems([1, 2], 3, 4, 5)); // [1, 2, 3, 4, 5]

// Spread in function calls
let numbers = [1, 2, 3];
console.log(Math.max(...numbers)); // 3
console.log(Math.min(...numbers)); // 1
```

---

## 🎯 Understanding Sort with Numbers

```javascript
// ❌ PROBLEM - Default sort is lexical (string)
let numbers = [10, 2, 3];
numbers.sort();
console.log(numbers); // [10, 2, 3] → ["10", "2", "3"] → wrong!

// ✅ SOLUTION - Use compare function
numbers = [10, 2, 3];
numbers.sort((a, b) => a - b);
console.log(numbers); // [2, 3, 10] - correct!

// Why? sort() converts to strings and compares alphabetically
// "10" comes before "2" (string comparison)
// But numerically: 2 < 3 < 10

// The compare function:
// Return negative: a comes first
// Return 0: equal
// Return positive: b comes first

// Ascending
[5, 2, 8].sort((a, b) => a - b); // [2, 5, 8]

// Descending
[5, 2, 8].sort((a, b) => b - a); // [8, 5, 2]
```

---

## 📊 Quick Reference

| Method | Purpose | Example |
|--------|---------|---------|
| forEach() | Execute for each | `arr.forEach(item => console.log(item))` |
| filter() | Keep matching | `arr.filter(n => n > 5)` |
| map() | Transform | `arr.map(n => n * 2)` |
| reduce() | Combine to single | `arr.reduce((sum, n) => sum + n, 0)` |
| find() | Find first | `arr.find(s => s.grade === "A")` |
| some() | At least one? | `arr.some(n => n > 10)` |
| every() | All true? | `arr.every(n => n > 0)` |
| sort() | Sort array | `arr.sort((a, b) => a - b)` |
| reverse() | Reverse | `arr.reverse()` |
| slice() | Copy portion | `arr.slice(1, 3)` |
| spread | Copy/combine | `[...arr, 4, 5]` |

---

**Master arrays to master data manipulation! 🚀**
