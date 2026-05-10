# 🧪 Practice Zone - Functions Exercises

11 practical function exercises with complete solutions and explanations.

---

## 1️⃣ Write a BMI Calculator Function

**Problem**: Create a function that calculates BMI (Body Mass Index).

Formula: BMI = weight (kg) / (height (m))²

```javascript
// Basic version
function calculateBMI(weight, height) {
  return weight / (height * height);
}

console.log(calculateBMI(70, 1.75)); // 22.86

// With category
function calculateBMI(weight, height) {
  const bmi = weight / (height * height);
  
  let category;
  if (bmi < 18.5) {
    category = "Underweight";
  } else if (bmi < 25) {
    category = "Normal";
  } else if (bmi < 30) {
    category = "Overweight";
  } else {
    category = "Obese";
  }
  
  return { bmi: bmi.toFixed(2), category: category };
}

console.log(calculateBMI(70, 1.75));
// { bmi: '22.86', category: 'Normal' }

// Advanced version with object parameter
function calculateBMI(params) {
  const { weight, height } = params;
  const bmi = weight / (height * height);
  
  const categories = {
    underweight: [0, 18.5],
    normal: [18.5, 25],
    overweight: [25, 30],
    obese: [30, 200]
  };
  
  let category = "Unknown";
  for (let [key, [min, max]] of Object.entries(categories)) {
    if (bmi >= min && bmi < max) {
      category = key.charAt(0).toUpperCase() + key.slice(1);
      break;
    }
  }
  
  return {
    weight: weight,
    height: height,
    bmi: parseFloat(bmi.toFixed(2)),
    category: category,
    status: bmi < 25 ? "Healthy" : "Action needed"
  };
}

console.log(calculateBMI({ weight: 70, height: 1.75 }));
// { weight: 70, height: 1.75, bmi: 22.86, category: 'Normal', status: 'Healthy' }
```

---

## 2️⃣ Create a Greet Function with Default Name

**Problem**: Create a function that greets, using a default name if none provided.

```javascript
// Function declaration (no default)
function greet(name) {
  console.log("Hello " + name);
}

greet("John");  // "Hello John"
greet();        // "Hello undefined"

// With default parameter
function greet(name = "Guest") {
  console.log("Hello " + name);
}

greet("John");  // "Hello John"
greet();        // "Hello Guest"

// Function expression
const greet2 = function(name = "Friend") {
  return `Welcome, ${name}!`;
};

console.log(greet2("Alice"));  // "Welcome, Alice!"
console.log(greet2());         // "Welcome, Friend!"

// Arrow function with default
const greet3 = (name = "User") => {
  return `Hi ${name}!`;
};

console.log(greet3());         // "Hi User!"

// Advanced: Multiple defaults
function greetFull(name = "Guest", greeting = "Hello") {
  return `${greeting}, ${name}!`;
}

console.log(greetFull("John", "Welcome")); // "Welcome, John!"
console.log(greetFull("John"));            // "Hello, John!"
console.log(greetFull());                  // "Hello, Guest!"
```

---

## 3️⃣ Sum All Numbers Using Rest Parameter

**Problem**: Create a function that sums any number of arguments using rest parameter.

```javascript
// Basic rest parameter
function sum(...numbers) {
  let total = 0;
  for (let num of numbers) {
    total += num;
  }
  return total;
}

console.log(sum(1, 2, 3));         // 6
console.log(sum(1, 2, 3, 4, 5));   // 15
console.log(sum(10, 20, 30, 40));  // 100

// Using reduce (cleaner)
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(5, 5, 5, 5));      // 20

// Mix regular and rest parameters
function greetAll(greeting, ...names) {
  console.log(greeting);
  names.forEach(name => console.log(`Hello ${name}`));
}

greetAll("Welcome everyone!", "John", "Sarah", "Mike");
// Output:
// "Welcome everyone!"
// "Hello John"
// "Hello Sarah"
// "Hello Mike"

// With default and rest
function calculate(operation = "sum", ...nums) {
  if (operation === "sum") {
    return nums.reduce((a, b) => a + b, 0);
  } else if (operation === "multiply") {
    return nums.reduce((a, b) => a * b, 1);
  }
}

console.log(calculate("sum", 1, 2, 3, 4));       // 10
console.log(calculate("multiply", 2, 3, 4));     // 24
```

---

## 4️⃣ Create a Closure Counter Function

**Problem**: Create a function that returns a counter using closure.

```javascript
// Basic counter
function createCounter() {
  let count = 0; // Enclosed variable
  
  return function() {
    count++;
    return count;
  };
}

const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3

// Counter with controls
function createCounter(start = 0) {
  let count = start;
  
  return {
    increment: function() {
      count++;
      return count;
    },
    decrement: function() {
      count--;
      return count;
    },
    reset: function() {
      count = start;
      return count;
    },
    getCount: function() {
      return count;
    }
  };
}

const counter = createCounter(10);
console.log(counter.increment()); // 11
console.log(counter.increment()); // 12
console.log(counter.decrement()); // 11
console.log(counter.reset());     // 10
console.log(counter.getCount());  // 10

// Private variable (secure)
function createBankAccount(initialBalance) {
  let balance = initialBalance; // Private
  
  return {
    deposit: (amount) => {
      balance += amount;
      console.log(`Deposited: $${amount}. Balance: $${balance}`);
      return balance;
    },
    withdraw: (amount) => {
      if (amount > balance) return "Insufficient funds";
      balance -= amount;
      console.log(`Withdrew: $${amount}. Balance: $${balance}`);
      return balance;
    },
    getBalance: () => balance
  };
}

const account = createBankAccount(1000);
account.deposit(500);    // "Deposited: $500. Balance: $1500"
account.withdraw(200);   // "Withdrew: $200. Balance: $1300"
console.log(account.getBalance()); // 1300
```

---

## 5️⃣ Write a Function That Returns Another Function

**Problem**: Create a function factory that returns customized functions.

```javascript
// Simple example
function createGreeter(greeting) {
  return function(name) {
    return `${greeting}, ${name}!`;
  };
}

const sayHello = createGreeter("Hello");
const sayHi = createGreeter("Hi");

console.log(sayHello("John"));  // "Hello, John!"
console.log(sayHi("Sarah"));    // "Hi, Sarah!"

// Multiplier function
function createMultiplier(factor) {
  return function(number) {
    return number * factor;
  };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);
const quadruple = createMultiplier(4);

console.log(double(5));     // 10
console.log(triple(5));     // 15
console.log(quadruple(5));  // 20

// Power function
function createPowerFunction(power) {
  return function(base) {
    return Math.pow(base, power);
  };
}

const square = createPowerFunction(2);
const cube = createPowerFunction(3);

console.log(square(5));  // 25
console.log(cube(5));    // 125

// Formatter function
function createFormatter(prefix, suffix) {
  return function(text) {
    return `${prefix} ${text} ${suffix}`;
  };
}

const quoteFormatter = createFormatter('"', '"');
const bracketFormatter = createFormatter('[', ']');

console.log(quoteFormatter("Hello"));    // '" Hello "'
console.log(bracketFormatter("Error"));  // '[ Error ]'
```

---

## 6️⃣ Use a Function to Log Even Numbers in Array

**Problem**: Filter and log only even numbers from an array.

```javascript
// Simple approach
function logEvens(arr) {
  for (let num of arr) {
    if (num % 2 === 0) {
      console.log(num);
    }
  }
}

logEvens([1, 2, 3, 4, 5, 6]);
// Output: 2, 4, 6

// Using filter
function logEvens(arr) {
  const evens = arr.filter(num => num % 2 === 0);
  evens.forEach(num => console.log(num));
}

logEvens([10, 15, 20, 25, 30]);
// Output: 10, 20, 30

// Return array of evens
function getEvens(arr) {
  return arr.filter(num => num % 2 === 0);
}

console.log(getEvens([1, 2, 3, 4, 5, 6])); // [2, 4, 6]

// With forEach
function logEvens(arr) {
  arr.forEach(num => {
    if (num % 2 === 0) {
      console.log(num);
    }
  });
}

logEvens([7, 8, 9, 10, 11, 12]);
// Output: 8, 10, 12

// Advanced: Higher-order function
function filterAndLog(arr, condition) {
  arr.forEach(item => {
    if (condition(item)) {
      console.log(item);
    }
  });
}

filterAndLog([1, 2, 3, 4, 5, 6], num => num % 2 === 0);
// Output: 2, 4, 6

filterAndLog([1, 2, 3, 4, 5, 6], num => num > 3);
// Output: 4, 5, 6
```

---

## 7️⃣ Create a Pure Function to Add Tax

**Problem**: Create a pure function that calculates price with tax (no side effects).

```javascript
// Pure function
function addTax(price, taxRate) {
  return price + (price * taxRate);
}

console.log(addTax(100, 0.15)); // 115

// Pure with parameters
function calculateTotal(price, taxRate = 0.1) {
  return price * (1 + taxRate);
}

console.log(calculateTotal(100));      // 110
console.log(calculateTotal(100, 0.2)); // 120

// Pure function returning object
function addTax(price, taxRate) {
  const taxAmount = price * taxRate;
  const total = price + taxAmount;
  
  return {
    originalPrice: price,
    taxRate: taxRate,
    taxAmount: parseFloat(taxAmount.toFixed(2)),
    total: parseFloat(total.toFixed(2))
  };
}

console.log(addTax(100, 0.15));
// { originalPrice: 100, taxRate: 0.15, taxAmount: 15, total: 115 }

// Pure function - multiple items
function calculateCartTax(items, taxRate) {
  let subtotal = 0;
  
  items.forEach(item => {
    subtotal += item.price * item.quantity;
  });
  
  const tax = subtotal * taxRate;
  const total = subtotal + tax;
  
  return {
    subtotal: parseFloat(subtotal.toFixed(2)),
    tax: parseFloat(tax.toFixed(2)),
    total: parseFloat(total.toFixed(2))
  };
}

const cart = [
  { name: "Shirt", price: 50, quantity: 2 },
  { name: "Pants", price: 100, quantity: 1 }
];

console.log(calculateCartTax(cart, 0.1));
// { subtotal: 200, tax: 20, total: 220 }

// ✅ Pure vs ❌ Impure
// ❌ IMPURE - modifies external state
let total = 0;
function addToTotal(price, tax) {
  total += price * (1 + tax); // Modifies external variable!
}

// ✅ PURE - no side effects
function calculateTotal(price, tax) {
  return price * (1 + tax); // Returns new value
}
```

---

## 8️⃣ Use IIFE to Show Welcome Message

**Problem**: Use IIFE to display a welcome message with private scope.

```javascript
// Basic IIFE
(function() {
  console.log("Welcome to JavaScript!");
})();
// Output: "Welcome to JavaScript!"

// IIFE with parameter
(function(name) {
  console.log(`Welcome, ${name}!`);
})("John");
// Output: "Welcome, John!"

// IIFE with multiple statements
(function() {
  const greeting = "Welcome";
  const time = new Date().getHours();
  
  if (time < 12) {
    console.log(greeting + " Good Morning!");
  } else if (time < 18) {
    console.log(greeting + " Good Afternoon!");
  } else {
    console.log(greeting + " Good Evening!");
  }
})();

// IIFE returning value
const result = (function() {
  const a = 10;
  const b = 20;
  return a + b;
})();

console.log(result); // 30

// IIFE with module pattern
const calculator = (function() {
  let result = 0; // Private variable
  
  return {
    add: function(x) {
      result += x;
      return result;
    },
    subtract: function(x) {
      result -= x;
      return result;
    },
    multiply: function(x) {
      result *= x;
      return result;
    },
    reset: function() {
      result = 0;
      return result;
    }
  };
})();

console.log(calculator.add(10));      // 10
console.log(calculator.add(5));       // 15
console.log(calculator.multiply(2));  // 30
console.log(calculator.reset());      // 0
```

---

## 9️⃣ Write a Discount Calculator (HOF Style)

**Problem**: Create higher-order function that applies discounts.

```javascript
// Simple HOF discount
function applyDiscount(discountRate) {
  return function(price) {
    return price - (price * discountRate);
  };
}

const discount10 = applyDiscount(0.1);
const discount20 = applyDiscount(0.2);
const discount50 = applyDiscount(0.5);

console.log(discount10(100)); // 90
console.log(discount20(100)); // 80
console.log(discount50(100)); // 50

// HOF with multiple operations
function createDiscountCalculator(discountType) {
  const discounts = {
    student: (price) => price * 0.9,
    senior: (price) => price * 0.8,
    vip: (price) => price * 0.7,
    seasonal: (price) => price * 0.85
  };
  
  return discounts[discountType] || ((price) => price);
}

const studentDiscount = createDiscountCalculator("student");
const seniorDiscount = createDiscountCalculator("senior");

console.log(studentDiscount(100));  // 90
console.log(seniorDiscount(100));   // 80

// Advanced: Chainable discounts
function createDiscountFactory(basePrice) {
  return {
    applyPercentage: function(percent) {
      basePrice = basePrice - (basePrice * percent);
      return this; // Return for chaining
    },
    applyCoupon: function(couponValue) {
      basePrice = basePrice - couponValue;
      return this;
    },
    addTax: function(taxRate) {
      basePrice = basePrice + (basePrice * taxRate);
      return this;
    },
    getTotal: function() {
      return parseFloat(basePrice.toFixed(2));
    }
  };
}

const total = createDiscountFactory(100)
  .applyPercentage(0.1)  // 10% off
  .applyCoupon(5)        // $5 off
  .addTax(0.1)           // 10% tax
  .getTotal();

console.log(total); // 94.95

// HOF with condition
function createSmartDiscount(cartValue) {
  return function applyDiscount() {
    if (cartValue < 50) return cartValue * 0;      // No discount
    if (cartValue < 100) return cartValue * 0.05;  // 5% off
    if (cartValue < 200) return cartValue * 0.1;   // 10% off
    return cartValue * 0.15;                        // 15% off
  };
}

console.log(createSmartDiscount(75)());   // 3.75 (5% of 75)
console.log(createSmartDiscount(150)()); // 15 (10% of 150)
```

---

## 🔟 Make a toUpperCase Transformer Using HOF

**Problem**: Create higher-order function that transforms text.

```javascript
// Basic transformer HOF
function createTransformer(transformFn) {
  return function(text) {
    return transformFn(text);
  };
}

const toUpper = createTransformer(str => str.toUpperCase());
const toLower = createTransformer(str => str.toLowerCase());
const capitalize = createTransformer(str => str.charAt(0).toUpperCase() + str.slice(1));

console.log(toUpper("hello"));      // "HELLO"
console.log(toLower("WORLD"));      // "world"
console.log(capitalize("javascript")); // "Javascript"

// Text transformer HOF with options
function createTextTransformer(options = {}) {
  return function(text) {
    let result = text;
    
    if (options.uppercase) result = result.toUpperCase();
    if (options.lowercase) result = result.toLowerCase();
    if (options.capitalize) result = result.charAt(0).toUpperCase() + result.slice(1);
    if (options.reverse) result = result.split('').reverse().join('');
    if (options.addPrefix) result = options.addPrefix + result;
    if (options.addSuffix) result = result + options.addSuffix;
    
    return result;
  };
}

const formatTitle = createTextTransformer({ capitalize: true, addSuffix: "!" });
const formatCode = createTextTransformer({ uppercase: true, addPrefix: ">>> " });

console.log(formatTitle("hello world"));  // "Hello world!"
console.log(formatCode("const x = 5"));   // ">>> CONST X = 5"

// Array transformer HOF
function createArrayTransformer(transformFn) {
  return function(arr) {
    return arr.map(transformFn);
  };
}

const toUpperArray = createArrayTransformer(str => str.toUpperCase());
const doubleNumbers = createArrayTransformer(num => num * 2);

console.log(toUpperArray(["hello", "world"])); // ["HELLO", "WORLD"]
console.log(doubleNumbers([1, 2, 3, 4, 5]));  // [2, 4, 6, 8, 10]

// Compose transformers
function composeTransformers(...transformers) {
  return function(value) {
    return transformers.reduce((acc, fn) => fn(acc), value);
  };
}

const upperThenReverse = composeTransformers(
  str => str.toUpperCase(),
  str => str.split('').reverse().join('')
);

console.log(upperThenReverse("hello")); // "OLLEH"

// Builder pattern transformer
function createStringBuilder(text = "") {
  return {
    append: function(str) {
      text += str;
      return this;
    },
    toUpper: function() {
      text = text.toUpperCase();
      return this;
    },
    toLower: function() {
      text = text.toLowerCase();
      return this;
    },
    reverse: function() {
      text = text.split('').reverse().join('');
      return this;
    },
    build: function() {
      return text;
    }
  };
}

const result = createStringBuilder("hello")
  .append(" ")
  .append("world")
  .toUpper()
  .reverse()
  .build();

console.log(result); // "DLROW OLLEH"
```

---

## 📊 Understanding Hoisting

```javascript
// ❌ ERROR - Expression not hoisted
greet(); // ERROR: greet is not a function

const greet = function() {
  console.log("Hi");
};

// ✅ WORKS - Declaration is hoisted
hello(); // Prints "Hi"

function hello() {
  console.log("Hi");
}

// Why? JavaScript internally does this:
// Declaration (hoisted to top):
function hello() {
  console.log("Hi");
}
// Expression (stays in place):
const greet = function() {
  console.log("Hi");
};
```

---

## 🎯 Challenge Exercises

1. **Password Validator**: Create HOF that validates passwords
2. **Logger**: Create IIFE that logs with timestamp
3. **Data Transformer**: Create HOF chain that transforms data
4. **Debt Calculator**: Create closure that tracks multiple debts
5. **API Mock**: Create IIFE that simulates API responses
6. **Permission System**: Use closures for role-based access

---

## 📊 Quick Reference

| Exercise | Concept | Key Feature |
|----------|---------|-------------|
| BMI | Function basics | Calculation & categorization |
| Greet | Default parameters | Fallback values |
| Sum | Rest parameter | Variable arguments |
| Counter | Closure | Private state |
| Returns function | HOF | Function factory |
| Even numbers | Array methods | Filter & log |
| Pure function | Purity | No side effects |
| IIFE | Scope | Private variables |
| Discount | HOF | Function composition |
| Transformer | HOF | Data transformation |

---

**Master functions to unlock JavaScript power! 🚀**
