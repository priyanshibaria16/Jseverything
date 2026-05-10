# 🚦 Control Flow - Complete Guide

Master the art of decision-making in JavaScript. Control flow decides which code runs, when it runs, and how many times it runs.

**Remember**: If operators are the verbs, control flow is the traffic signal. 🚦

---

## 📚 Table of Contents

1. [What is Control Flow?](#what-is-control-flow)
2. [if, else if, else Statements](#if-else-if-else-statements)
3. [switch-case Statements](#switch-case-statements)
4. [Early Return Pattern](#early-return-pattern)
5. [Loops (for, while)](#loops)
6. [Common Confusions](#common-confusions)
7. [Best Practices](#best-practices)
8. [Practical Examples](#practical-examples)

---

## 🤔 What is Control Flow?

Control flow is the order in which statements execute in a program. Without control flow, every line would execute sequentially from top to bottom. Control flow allows your program to:

- **Make decisions** - Choose which code to run based on conditions
- **Repeat actions** - Run code multiple times with loops
- **Skip sections** - Bypass code when conditions aren't met
- **Handle different scenarios** - Respond differently to different inputs

### 🧠 Real-World Analogy

```
Without Control Flow (no intelligence):
→ Drive forward
→ Drive forward
→ Drive forward
(You crash into a wall!)

With Control Flow (decision-making):
→ If traffic light is green, drive forward
→ Else if traffic light is yellow, prepare to stop
→ Else, stop
(You navigate safely!)
```

### Visual Flowchart

```
         START
           ↓
      Condition?
      /        \
    YES         NO
    ↓            ↓
   Path A      Path B
    ↓            ↓
   ...          ...
    ↓            ↓
         END
```

---

## 🧱 if, else if, else Statements

### 📝 Syntax & Structure

```javascript
if (condition1) {
  // Executes if condition1 is true
} else if (condition2) {
  // Executes if condition1 is false AND condition2 is true
} else if (condition3) {
  // Executes if condition1 and condition2 are false AND condition3 is true
} else {
  // Executes if ALL previous conditions are false
  // This is optional (not required)
}
```

### 💡 Key Points
- **Only ONE block executes** - Once a condition is true, the rest are skipped
- **Order matters** - The chain checks from top to bottom
- **else is optional** - You don't always need an else block
- **Can have multiple else if** - No limit to how many you can chain

### ✅ Example 1: Grade System

```javascript
// Basic if-else if-else
let marks = 78;

if (marks >= 90) {
  console.log("Grade: A");
} else if (marks >= 75) {
  console.log("Grade: B");
} else if (marks >= 60) {
  console.log("Grade: C");
} else {
  console.log("Grade: F");
}
// Output: "Grade: B"

// Why B? Because:
// ✓ marks >= 90? NO (78 is not >= 90)
// ✓ marks >= 75? YES! (78 is >= 75) → Execute this block, skip the rest
```

### ✅ Example 2: Age-Based Access Control

```javascript
function getAccess(age) {
  if (age < 13) {
    return "Not allowed to use social media";
  } else if (age < 18) {
    return "Parental consent required";
  } else if (age < 65) {
    return "Full adult access";
  } else {
    return "Senior citizen discount available";
  }
}

console.log(getAccess(10));  // "Not allowed to use social media"
console.log(getAccess(16));  // "Parental consent required"
console.log(getAccess(25));  // "Full adult access"
console.log(getAccess(70));  // "Senior citizen discount available"
```

### ✅ Example 3: Multiple Conditions (Logical Operators)

```javascript
// Combining conditions with && (AND) and || (OR)
let hour = 14; // 2 PM
let hasTicket = true;

// Using && (AND) - BOTH must be true
if (hour >= 9 && hour <= 17 && hasTicket) {
  console.log("Entry granted"); // This executes
} else {
  console.log("Entry denied");
}

// Using || (OR) - At least ONE must be true
let isMember = false;
let isPremium = false;
let isAdmin = true;

if (isMember || isPremium || isAdmin) {
  console.log("You have access"); // This executes (isAdmin is true)
} else {
  console.log("No access");
}
```

### ✅ Example 4: Weather-Based Recommendation

```javascript
function getWeatherAdvice(weather, temperature) {
  if (weather === "rainy") {
    return "Take an umbrella";
  } else if (weather === "sunny" && temperature > 30) {
    return "Apply sunscreen and drink water";
  } else if (weather === "sunny") {
    return "Nice day for outdoor activities";
  } else if (weather === "snowy") {
    return "Wear warm clothes and be careful";
  } else {
    return "Check the weather forecast";
  }
}

console.log(getWeatherAdvice("rainy", 20));      // "Take an umbrella"
console.log(getWeatherAdvice("sunny", 35));      // "Apply sunscreen and drink water"
console.log(getWeatherAdvice("sunny", 25));      // "Nice day for outdoor activities"
console.log(getWeatherAdvice("snowy", 0));       // "Wear warm clothes and be careful"
console.log(getWeatherAdvice("cloudy", 22));     // "Check the weather forecast"
```

---

## 🌀 switch-case Statements

### 📝 Syntax & Structure

```javascript
switch (expression) {
  case value1:
    // Executes if expression === value1
    break; // Important: stops here
  
  case value2:
    // Executes if expression === value2
    break;
  
  case value3:
  case value4:
    // Executes if expression === value3 OR expression === value4
    break;
  
  default:
    // Executes if expression doesn't match any case
    // Optional, like else
}
```

### 💡 Key Points
- **Uses strict equality (===)** - Must match exactly
- **break is crucial** - Without it, execution "falls through" to the next case
- **One expression, many cases** - Great for checking one variable against multiple values
- **default is optional** - Like else in if-else statements

### ⚠️ Critical: Understanding break

```javascript
// ❌ WITHOUT break (WRONG - demonstrates fall-through)
let fruit = "apple";

switch (fruit) {
  case "banana":
    console.log("Yellow");
    // No break! Execution continues...
  case "apple":
    console.log("Red");
    // No break! Execution continues...
  case "orange":
    console.log("Orange");
    break; // Finally stops here
  default:
    console.log("Unknown");
}

// Output:
// "Red"
// "Orange"
// (All cases after matching case execute until break is found!)
```

```javascript
// ✅ WITH break (CORRECT)
let fruit = "apple";

switch (fruit) {
  case "banana":
    console.log("Yellow");
    break; // Stops execution
  case "apple":
    console.log("Red");
    break; // Stops execution
  case "orange":
    console.log("Orange");
    break; // Stops execution
  default:
    console.log("Unknown");
}

// Output:
// "Red"
// (Stops after the matching case)
```

### ✅ Example 1: Fruit Color Identifier

```javascript
function getFruitColor(fruit) {
  switch (fruit) {
    case "banana":
      return "Yellow";
    case "apple":
      return "Red";
    case "orange":
      return "Orange";
    case "grape":
      return "Purple";
    case "lime":
      return "Green";
    default:
      return "Unknown fruit";
  }
}

console.log(getFruitColor("banana")); // "Yellow"
console.log(getFruitColor("apple"));  // "Red"
console.log(getFruitColor("mango"));  // "Unknown fruit"
```

### ✅ Example 2: Day of Week Abbreviation

```javascript
function getDayAbbreviation(dayNumber) {
  switch (dayNumber) {
    case 0:
      return "Sun";
    case 1:
      return "Mon";
    case 2:
      return "Tue";
    case 3:
      return "Wed";
    case 4:
      return "Thu";
    case 5:
      return "Fri";
    case 6:
      return "Sat";
    default:
      return "Invalid day";
  }
}

console.log(getDayAbbreviation(0)); // "Sun"
console.log(getDayAbbreviation(3)); // "Wed"
console.log(getDayAbbreviation(7)); // "Invalid day"
```

### ✅ Example 3: Multiple Cases (Fall-Through - Intentional)

```javascript
// Intentional fall-through: when cases share the same code
function getWeekendStatus(day) {
  switch (day) {
    case "Saturday":
    case "Sunday":
      return "🎉 Weekend!";
    case "Monday":
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
    case "Friday":
      return "📚 Weekday - Work time";
    default:
      return "Invalid day";
  }
}

console.log(getWeekendStatus("Saturday")); // "🎉 Weekend!"
console.log(getWeekendStatus("Sunday"));   // "🎉 Weekend!"
console.log(getWeekendStatus("Monday"));   // "📚 Weekday - Work time"
```

### ✅ Example 4: HTTP Status Code Handler

```javascript
function handleHttpStatus(statusCode) {
  switch (statusCode) {
    case 200:
      return "✅ OK - Request successful";
    case 201:
      return "✅ Created - Resource created";
    case 400:
      return "❌ Bad Request - Invalid input";
    case 401:
      return "❌ Unauthorized - Authentication required";
    case 403:
      return "❌ Forbidden - Access denied";
    case 404:
      return "❌ Not Found - Resource doesn't exist";
    case 500:
      return "❌ Server Error - Something went wrong";
    default:
      return "❓ Unknown status code";
  }
}

console.log(handleHttpStatus(200)); // "✅ OK - Request successful"
console.log(handleHttpStatus(404)); // "❌ Not Found - Resource doesn't exist"
console.log(handleHttpStatus(500)); // "❌ Server Error - Something went wrong"
```

### 📊 switch vs if-else Comparison

| Aspect | switch | if-else if-else |
|--------|--------|-----------------|
| **Best for** | One variable, many values | Complex conditions |
| **Readability** | Better for 5+ cases | Better for 2-3 cases |
| **Flexibility** | Limited to === | Can use any operators |
| **Performance** | Slightly faster | Slightly slower |
| **Maintainability** | Easier to add cases | Easier to modify conditions |
| **Example** | `switch(userRole)` | `if(age && status && admin)` |

---

## 🔁 Early Return Pattern

### 📝 Concept

The early return pattern means returning from a function as soon as you know you should, rather than nesting multiple if-else blocks. This makes code flatter, more readable, and easier to understand.

### ❌ Without Early Return (Nested & Confusing)

```javascript
function validateUser(user) {
  if (user) {
    if (user.age) {
      if (user.age >= 18) {
        if (user.hasEmail) {
          return "User is valid";
        } else {
          return "Email required";
        }
      } else {
        return "Must be 18+";
      }
    } else {
      return "Age is required";
    }
  } else {
    return "User object required";
  }
}

// This is hard to read! It's like a pyramid of doom.
```

### ✅ With Early Return (Clean & Clear)

```javascript
function validateUser(user) {
  // Check conditions and return early if they fail
  if (!user) {
    return "User object required";
  }
  
  if (!user.age) {
    return "Age is required";
  }
  
  if (user.age < 18) {
    return "Must be 18+";
  }
  
  if (!user.hasEmail) {
    return "Email required";
  }
  
  // If we reach here, all checks passed
  return "User is valid";
}

// Much clearer! Each check is independent.
```

### 💡 Why Use Early Return?

1. **Avoids nesting** - Flat structure is easier to read
2. **Fail fast** - Exit immediately when a condition fails
3. **Single responsibility** - Each check is isolated
4. **Easier debugging** - Clear what each condition does

### ✅ Example 1: Input Validation

```javascript
function processPayment(amount, cardNumber, cvv) {
  // Early returns for validation
  if (!amount || amount <= 0) {
    return "Invalid amount";
  }
  
  if (!cardNumber || cardNumber.length !== 16) {
    return "Invalid card number";
  }
  
  if (!cvv || cvv.length !== 3) {
    return "Invalid CVV";
  }
  
  // If we reach here, all validations passed
  console.log(`Processing payment of $${amount}`);
  return "Payment successful";
}

console.log(processPayment(0, "1234567890123456", "123"));      // "Invalid amount"
console.log(processPayment(100, "123456789012345", "123"));     // "Invalid card number"
console.log(processPayment(100, "1234567890123456", "12"));     // "Invalid CVV"
console.log(processPayment(100, "1234567890123456", "123"));    // Processes payment
```

### ✅ Example 2: Function Argument Checking

```javascript
function calculateDiscount(price, category, hasVoucher) {
  // Early returns for invalid inputs
  if (!price || price <= 0) {
    return "Error: Invalid price";
  }
  
  if (!category) {
    return "Error: Category required";
  }
  
  // Apply discounts
  let discount = 0;
  
  if (category === "vip") {
    discount = price * 0.20; // 20% off
  } else if (category === "regular") {
    discount = price * 0.10; // 10% off
  }
  
  if (hasVoucher) {
    discount += price * 0.05; // Additional 5% off
  }
  
  return price - discount;
}

console.log(calculateDiscount(-50, "vip", false));         // "Error: Invalid price"
console.log(calculateDiscount(100, "", false));            // "Error: Category required"
console.log(calculateDiscount(100, "vip", false));         // 80 (20% discount)
console.log(calculateDiscount(100, "vip", true));          // 75 (20% + 5% discount)
```

### ✅ Example 3: Access Control with Early Return

```javascript
function grantAccess(user) {
  // Check each condition and return early if it fails
  if (!user) {
    return { allowed: false, reason: "User not found" };
  }
  
  if (!user.isActive) {
    return { allowed: false, reason: "User account is inactive" };
  }
  
  if (!user.email) {
    return { allowed: false, reason: "Email verification required" };
  }
  
  if (user.role === "admin" || user.role === "moderator") {
    return { allowed: true, reason: "Admin/Moderator access granted" };
  }
  
  if (user.isPremium) {
    return { allowed: true, reason: "Premium member access granted" };
  }
  
  // Default: regular user
  return { allowed: true, reason: "Regular member access granted" };
}

console.log(grantAccess(null));
// { allowed: false, reason: "User not found" }

console.log(grantAccess({ isActive: false }));
// { allowed: false, reason: "User account is inactive" }

console.log(grantAccess({ isActive: true, email: "test@test.com", role: "admin" }));
// { allowed: true, reason: "Admin/Moderator access granted" }
```

### 🎯 Early Return Template

```javascript
// Template for using early return pattern
function doSomething(input) {
  // Validate all inputs at the top
  if (!input) {
    return "Error: Input required";
  }
  
  if (typeof input !== "number") {
    return "Error: Input must be a number";
  }
  
  if (input < 0) {
    return "Error: Input must be positive";
  }
  
  // All validations passed, now do the actual work
  const result = input * 2;
  return result;
}
```

---

## 🔄 Loops

Control flow also includes repeating code multiple times. Loops let you execute the same code block repeatedly.

### 🔁 for Loop

```javascript
// Syntax: for (initialization; condition; increment)
for (let i = 0; i < 5; i++) {
  console.log(`Iteration ${i}`);
}
// Output:
// "Iteration 0"
// "Iteration 1"
// "Iteration 2"
// "Iteration 3"
// "Iteration 4"

// Real-world example: Print numbers 1-10
for (let num = 1; num <= 10; num++) {
  console.log(num);
}

// Loop through an array
const fruits = ["apple", "banana", "orange"];
for (let i = 0; i < fruits.length; i++) {
  console.log(fruits[i]);
}
```

### 🔁 while Loop

```javascript
// Syntax: while (condition)
let i = 0;
while (i < 5) {
  console.log(`Count: ${i}`);
  i++; // Important: increment, otherwise infinite loop!
}

// Real-world example: Wait for something
let attempts = 0;
while (attempts < 3) {
  console.log(`Attempt ${attempts + 1}`);
  attempts++;
}

// Be careful with while loops - they can be infinite!
// This is WRONG - infinite loop:
// while (true) {
//   console.log("This runs forever!");
// }
```

### 🔁 do...while Loop

```javascript
// Executes at least once, then checks condition
let password = "";
do {
  password = prompt("Enter password (minimum 4 characters):");
} while (password.length < 4);

// Useful when you want to execute the code at least once
```

### break and continue

```javascript
// break: Exit loop immediately
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break; // Exits the loop when i equals 5
  }
  console.log(i); // Prints: 0, 1, 2, 3, 4
}

// continue: Skip current iteration
for (let i = 0; i < 5; i++) {
  if (i === 2) {
    continue; // Skips this iteration, goes to next
  }
  console.log(i); // Prints: 0, 1, 3, 4 (skips 2)
}

// Real-world: Find first number divisible by 7
for (let i = 1; i <= 100; i++) {
  if (i % 7 === 0) {
    console.log(`Found: ${i}`);
    break; // Stop after finding first one
  }
}
```

### 📝 Loop Examples

```javascript
// Count down from 10 to 1
for (let i = 10; i >= 1; i--) {
  console.log(i);
}

// Multiplication table
for (let i = 1; i <= 10; i++) {
  console.log(`5 × ${i} = ${5 * i}`);
}

// Sum of numbers 1 to 100
let sum = 0;
for (let i = 1; i <= 100; i++) {
  sum += i;
}
console.log(sum); // 5050

// Find all even numbers between 1 and 20
for (let i = 1; i <= 20; i++) {
  if (i % 2 === 0) {
    console.log(i);
  }
}
```

---

## ⚠️ Common Confusions

### ❌ Confusion 1: Forgetting break in switch

```javascript
// WRONG
let day = "Monday";
switch (day) {
  case "Monday":
    console.log("Start of week");
  case "Tuesday":
    console.log("Second day");
  case "Wednesday":
    console.log("Midweek");
}
// Output:
// "Start of week"
// "Second day"
// "Midweek"
// All cases after Monday execute! (Fall-through)

// CORRECT
switch (day) {
  case "Monday":
    console.log("Start of week");
    break; // Add this!
  case "Tuesday":
    console.log("Second day");
    break; // And this!
  case "Wednesday":
    console.log("Midweek");
    break; // And this!
}
// Output: "Start of week"
```

### ❌ Confusion 2: Order Matters in if-else if

```javascript
// WRONG ORDER
let score = 85;
if (score >= 50) {
  console.log("Pass");
} else if (score >= 80) {
  console.log("Excellent");
}
// Output: "Pass" (Wrong! Should be "Excellent")
// The first condition matches, so others are never checked

// CORRECT ORDER
if (score >= 80) {
  console.log("Excellent");
} else if (score >= 50) {
  console.log("Pass");
}
// Output: "Excellent" ✓
// Check more specific conditions first!
```

### ❌ Confusion 3: Truthy/Falsy in if

```javascript
// These are falsy:
if (false) { } // false
if (0) { }     // zero
if ("") { }    // empty string
if (null) { }  // null
if (undefined) { } // undefined
if (NaN) { }   // NaN

// These are truthy:
if (true) { }      // true
if (1) { }         // any non-zero number
if ("hello") { }   // any non-empty string
if ({}) { }        // objects (even empty ones!)
if ([]) { }        // arrays (even empty ones!)
if (function(){}) { } // functions

// Common use:
let user = { name: "John" };
if (user) {
  console.log("User exists"); // Executes! (objects are truthy)
}

let data = null;
if (!data) {
  console.log("No data"); // Executes! (null is falsy, ! negates it)
}
```

### ❌ Confusion 4: === vs ==

```javascript
// Use === (strict equality) - ALWAYS!
console.log("5" === 5);  // false (different types)
console.log("5" == 5);   // true (loose equality - type coercion)

console.log(0 === false);  // false (different types)
console.log(0 == false);   // true (loose equality)

console.log(null === undefined);  // false
console.log(null == undefined);   // true

// In control flow, always use ===
if (userInput === "5") {
  // Only if input is the string "5"
}

if (userInput == 5) {
  // Matches if input is "5" or 5 (dangerous!)
}
```

### ❌ Confusion 5: Infinite Loops

```javascript
// INFINITE LOOP - DON'T DO THIS!
// for (let i = 0; i < 10; ) {
//   console.log(i);
//   // Missing i++, so i never increases!
// }

// INFINITE LOOP - DON'T DO THIS EITHER!
// while (true) {
//   console.log("This runs forever!");
// }

// How to fix:
for (let i = 0; i < 10; i++) { // Add i++
  console.log(i);
}

// Use break to exit intentional infinite loops:
let counter = 0;
while (true) {
  console.log(counter);
  counter++;
  if (counter >= 5) {
    break; // Exit the loop
  }
}
```

---

## 🎯 Best Practices

### ✅ 1. Keep Control Flow Simple

```javascript
// ❌ TOO COMPLEX
if (age >= 18 && (city === "NYC" || city === "LA") && !criminal && employed && hasLicense && !debt) {
  grantAccess();
}

// ✅ BETTER - Extract to a function
function isEligible(person) {
  if (person.age < 18) return false;
  if (!isValidCity(person.city)) return false;
  if (person.hasCriminalRecord) return false;
  if (!person.employed) return false;
  if (!person.hasLicense) return false;
  if (person.hasDebt) return false;
  return true;
}

if (isEligible(person)) {
  grantAccess();
}
```

### ✅ 2. Avoid Deep Nesting

```javascript
// ❌ DEEPLY NESTED (Hard to read)
if (user) {
  if (user.isActive) {
    if (user.hasPermission) {
      if (user.isPaid) {
        executeAction();
      }
    }
  }
}

// ✅ BETTER - Use early returns
function executeIfAllowed(user) {
  if (!user) return;
  if (!user.isActive) return;
  if (!user.hasPermission) return;
  if (!user.isPaid) return;
  executeAction();
}
```

### ✅ 3. Use Guard Clauses

```javascript
// Guard clause: Return/exit early if condition fails
function getDiscount(customer) {
  // Guard: must have customer object
  if (!customer) return 0;
  
  // Guard: customer must be active
  if (!customer.isActive) return 0;
  
  // Guard: must have purchase history
  if (!customer.totalPurchases) return 0;
  
  // Now we know all guards passed, calculate discount
  if (customer.totalPurchases > 10000) return 0.20; // 20%
  if (customer.totalPurchases > 5000) return 0.15;  // 15%
  return 0.10; // 10% default
}
```

### ✅ 4. Use Meaningful Variable Names

```javascript
// ❌ UNCLEAR
if (x > 18 && y) {
  z();
}

// ✅ CLEAR
if (age >= 18 && hasPermission) {
  grantAccess();
}
```

### ✅ 5. Add Comments for Complex Logic

```javascript
function validateEmail(email) {
  // Must have @ symbol and domain
  if (!email.includes("@")) {
    return false;
  }
  
  // Must have a domain extension (.com, .org, etc)
  const afterAt = email.split("@")[1];
  if (!afterAt.includes(".")) {
    return false;
  }
  
  return true;
}
```

### ✅ 6. Use switch for Many Cases

```javascript
// ❌ TOO MANY if-else
if (status === "pending") { } 
else if (status === "approved") { }
else if (status === "rejected") { }
else if (status === "archived") { }

// ✅ BETTER - Use switch
switch (status) {
  case "pending":
    // ...
    break;
  case "approved":
    // ...
    break;
  case "rejected":
    // ...
    break;
  case "archived":
    // ...
    break;
}
```

### ✅ 7. Use Ternary for Simple Cases

```javascript
// ✅ GOOD - Simple ternary
const status = age >= 18 ? "Adult" : "Minor";

// ❌ AVOID - Complex nested ternary
const grade = score >= 90 ? "A" : score >= 80 ? "B" : score >= 70 ? "C" : "F";

// ✅ BETTER - Use if-else for complex logic
let grade;
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else {
  grade = "F";
}
```

---

## 🧠 Practical Examples

### Example 1: E-Commerce Order Processing

```javascript
function processOrder(order) {
  // Guard clauses for validation
  if (!order) {
    return { success: false, message: "Order object required" };
  }
  
  if (!order.items || order.items.length === 0) {
    return { success: false, message: "Order must contain items" };
  }
  
  if (!order.customer) {
    return { success: false, message: "Customer information required" };
  }
  
  if (order.total <= 0) {
    return { success: false, message: "Invalid order total" };
  }
  
  // Calculate discount based on customer type
  let discount = 0;
  switch (order.customer.type) {
    case "vip":
      discount = order.total * 0.20;
      break;
    case "premium":
      discount = order.total * 0.10;
      break;
    case "regular":
      discount = order.total * 0.05;
      break;
  }
  
  // Apply any promotional codes
  if (order.promoCode) {
    // Additional 5% off with promo code
    discount += order.total * 0.05;
  }
  
  const finalTotal = order.total - discount;
  
  // Determine shipping based on total
  let shippingCost = 0;
  if (finalTotal < 50) {
    shippingCost = 10;
  } else if (finalTotal < 100) {
    shippingCost = 5;
  }
  // else: free shipping for orders over $100
  
  return {
    success: true,
    originalTotal: order.total,
    discount: discount,
    shippingCost: shippingCost,
    finalTotal: finalTotal + shippingCost
  };
}

// Test
const testOrder = {
  items: ["item1", "item2"],
  total: 150,
  customer: { type: "vip" },
  promoCode: "SAVE20"
};

console.log(processOrder(testOrder));
// Output: successful order with discounts applied
```

### Example 2: Game State Management

```javascript
function gameLoop(playerHealth, enemyHealth, round) {
  // Check win conditions first
  if (enemyHealth <= 0) {
    return "You won! 🎉";
  }
  
  // Check loss conditions
  if (playerHealth <= 0) {
    return "Game Over! You lost. 💀";
  }
  
  // Game is still running - determine actions
  switch (round % 3) {
    case 0:
      // Round 3, 6, 9... - Special attack
      console.log("Special attack! Double damage!");
      break;
    
    case 1:
      // Round 1, 4, 7... - Normal attack
      console.log("Normal attack!");
      break;
    
    case 2:
      // Round 2, 5, 8... - Heal
      console.log("Healing yourself...");
      break;
  }
  
  // Continue game
  return "Game continues...";
}

console.log(gameLoop(100, 50, 1));  // "Game continues..."
console.log(gameLoop(100, 0, 5));   // "You won! 🎉"
console.log(gameLoop(0, 50, 3));    // "Game Over! You lost. 💀"
```

### Example 3: Temperature Control System

```javascript
function controlTemperature(currentTemp, targetTemp) {
  // Early returns for invalid inputs
  if (currentTemp === null || currentTemp === undefined) {
    return "Error: Current temperature required";
  }
  
  if (targetTemp === null || targetTemp === undefined) {
    return "Error: Target temperature required";
  }
  
  // Check if already at target
  if (currentTemp === targetTemp) {
    return "✓ Temperature at target. System off.";
  }
  
  // Determine action needed
  if (currentTemp < targetTemp) {
    const difference = targetTemp - currentTemp;
    
    if (difference > 10) {
      return "🔥 Heating: HIGH (need " + difference + "°)";
    } else if (difference > 5) {
      return "🔥 Heating: MEDIUM (need " + difference + "°)";
    } else {
      return "🔥 Heating: LOW (need " + difference + "°)";
    }
  } else {
    // currentTemp > targetTemp
    const difference = currentTemp - targetTemp;
    
    if (difference > 10) {
      return "❄️ Cooling: HIGH (reduce " + difference + "°)";
    } else if (difference > 5) {
      return "❄️ Cooling: MEDIUM (reduce " + difference + "°)";
    } else {
      return "❄️ Cooling: LOW (reduce " + difference + "°)";
    }
  }
}

console.log(controlTemperature(20, 25)); // "🔥 Heating: MEDIUM (need 5°)"
console.log(controlTemperature(30, 20)); // "❄️ Cooling: HIGH (reduce 10°)"
console.log(controlTemperature(25, 25)); // "✓ Temperature at target. System off."
```

---

## 📊 Control Flow Decision Tree

```
START
  ↓
Is it ONE variable with MANY values?
  ├─ YES → Use switch statement
  └─ NO → Continue
     ↓
Is it a COMPLEX condition?
  ├─ YES → Use if-else if-else
  └─ NO → Continue
     ↓
Is it a SIMPLE condition?
  ├─ YES → Use ternary operator
  └─ NO → Use if-else
     ↓
Need to EXIT early from a function?
  ├─ YES → Use early return
  └─ NO → Continue
     ↓
Need to REPEAT code?
  ├─ YES → Use for/while loop
  └─ NO → Just use simple if
     ↓
END
```

---

## 🎓 Summary

| Concept | Use When | Example |
|---------|----------|---------|
| **if-else** | Need conditional execution | Check age, validate input |
| **switch** | One variable, many values | Check status, day of week |
| **Ternary** | Simple true/false choice | `age >= 18 ? "Adult" : "Minor"` |
| **Early return** | Need clean, flat code | Guard clauses in functions |
| **for loop** | Know number of iterations | Loop through array, count |
| **while loop** | Unknown iteration count | Process until condition met |
| **break** | Exit loop early | Stop searching when found |
| **continue** | Skip current iteration | Skip even numbers |

---

## 🧠 The Mindset

**Control flow = conditional storytelling.**

Your program is like a story:
- **if-else** = "If this happens, do that, otherwise do this"
- **switch** = "Based on this choice, here are your options"
- **loops** = "Keep doing this until something changes"
- **Early return** = "Stop if this isn't right, otherwise continue"

Write readable branches. Avoid nesting too deep — use early return if needed. Make your code tell a clear, logical story.

---

**Happy Coding! 🚦**
