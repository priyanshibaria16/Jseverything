# JavaScript Operators

## What are Operators?

Operators are special symbols or keywords in JavaScript used to perform operations on values called **operands**.

You'll use them in:
- Calculations
- Comparisons
- Logic
- Assignments
- Type checks

> 💡 Think of operators as the **verbs** of your code — they act on data.

---

## ➕ Arithmetic Operators

Used for basic math.

| Operator | Name | Example | Result |
|---|---|---|---|
| `+` | Addition | `10 + 3` | `13` |
| `-` | Subtraction | `10 - 3` | `7` |
| `*` | Multiplication | `10 * 3` | `30` |
| `/` | Division | `10 / 3` | `3.33...` |
| `%` | Modulus (remainder) | `10 % 3` | `1` |
| `**` | Exponentiation (power) | `2 ** 3` | `8` |

### Example

```js
let a = 10, b = 3;

console.log(a + b);  // 13
console.log(a % b);  // 1
console.log(2 ** 3); // 8
```

---

## 🧮 Assignment Operators

Used to assign values to variables.

| Operator | Meaning | Equivalent |
|---|---|---|
| `=` | Assign | `a = 5` |
| `+=` | Add and assign | `a = a + b` |
| `-=` | Subtract and assign | `a = a - b` |
| `*=` | Multiply and assign | `a = a * b` |
| `/=` | Divide and assign | `a = a / b` |
| `%=` | Modulus and assign | `a = a % b` |

### Example

```js
let score = 5;
score += 2; // score = 7
score -= 1; // score = 6
score *= 2; // score = 12
```

---

## 🧾 Comparison Operators

Used in condition checks — always return `true` or `false`.

| Operator | Name | Example | Result |
|---|---|---|---|
| `==` | Equal (loose) | `5 == "5"` | `true` |
| `===` | Equal (strict) | `5 === "5"` | `false` |
| `!=` | Not equal (loose) | `5 != "5"` | `false` |
| `!==` | Not equal (strict) | `5 !== "5"` | `true` |
| `>` | Greater than | `10 > 3` | `true` |
| `<` | Less than | `10 < 3` | `false` |
| `>=` | Greater than or equal | `5 >= 5` | `true` |
| `<=` | Less than or equal | `4 <= 5` | `true` |

### Example

```js
console.log(5 == "5");  // true  — type coercion happens
console.log(5 === "5"); // false — strict: type must match too
```

> ⚠️ Always prefer `===` to avoid unexpected type coercion bugs.

---

## ✅ Logical Operators

Used to combine multiple conditions.

| Operator | Name | Description |
|---|---|---|
| `&&` | AND | Both conditions must be `true` |
| `\|\|` | OR | At least one condition must be `true` |
| `!` | NOT | Negates (flips) the truthiness |

### Example

```js
let age = 20, hasID = true;

if (age >= 18 && hasID) {
  console.log("Allowed"); // ✅ both true
}

if (age < 18 || hasID) {
  console.log("Allowed"); // ✅ at least one true
}

console.log(!true);  // false
console.log(!false); // true
```

### Short-circuit Evaluation

```js
// && stops at first false
false && console.log("never runs");

// || stops at first true
true || console.log("never runs");

// Common pattern: default value
let name = userInput || "Guest";
```

---

## 🌀 Unary Operators

Operate on a **single** operand.

| Operator | Name | Description |
|---|---|---|
| `+` | Unary plus | Tries to convert to number |
| `-` | Unary minus | Negates the value |
| `++` | Increment | Adds 1 |
| `--` | Decrement | Subtracts 1 |
| `typeof` | Type check | Returns the data type as a string |

### Example

```js
let x = "5";
console.log(+x);  // 5 — string converted to number
console.log(-x);  // -5

let count = 3;
console.log(++count); // 4 — pre-increment (increments first, then returns)
console.log(count++); // 4 — post-increment (returns first, then increments)
console.log(count);   // 5 — now updated
```

### Pre vs Post Increment

```js
let i = 5;

console.log(++i); // 6  — increment THEN return
console.log(i++); // 6  — return THEN increment
console.log(i);   // 7  — now updated
```

---

## ❓ Ternary Operator (Conditional)

Shorthand for a simple `if...else`. Works in a single line.

### Syntax

```js
condition ? valueIfTrue : valueIfFalse
```

### Example

```js
let score = 80;
let grade = score > 50 ? "Pass" : "Fail";
console.log(grade); // "Pass"

// Equivalent if...else:
let grade;
if (score > 50) {
  grade = "Pass";
} else {
  grade = "Fail";
}
```

> ⚠️ Use ternary for **simple** decisions only. Nest them sparingly — complex chains hurt readability.

---

## 🧪 `typeof` Operator

Returns the data type of a value as a string.

```js
typeof 123        // "number"
typeof "hi"       // "string"
typeof true       // "boolean"
typeof undefined  // "undefined"
typeof null       // "object"  ⚠️ JS bug — not really an object
typeof []         // "object"  ⚠️ use Array.isArray() instead
typeof {}         // "object"
typeof function(){} // "function"
typeof 123n       // "bigint"
typeof Symbol()   // "symbol"
```

---

## ❓ Common Confusions

### `+` vs `-` with strings

```js
"5" + 1  // "51"  — + sees string → concatenation
"5" - 1  // 4     — - forces numeric coercion
"5" * 2  // 10    — * forces numeric coercion
```

### `!!value` — Double NOT trick

```js
// Converts any value to its boolean equivalent
!!0         // false
!!""        // false
!!null      // false
!!"hello"   // true
!!42        // true
!![]        // true
```

### Pre-increment vs Post-increment

```js
let a = 5;
let b = ++a; // a becomes 6 first, then b = 6
let c = a++; // c = 6 first, then a becomes 7
```

---

## 🧠 Mindset & Best Practices

| Rule | Why |
|---|---|
| Use `===` instead of `==` | Avoids silent type coercion bugs |
| Use ternary for simple decisions only | Complex ternaries hurt readability |
| Think in truthy/falsy with `&&`, `\|\|`, `!` | Makes conditions more concise |
| Use `Array.isArray()` over `typeof` for arrays | `typeof []` misleadingly returns `"object"` |
| Use `=== null` to check for null | `typeof null` is a known JS bug |

---

## Summary Cheat Sheet

| Category | Operators |
|---|---|
| Arithmetic | `+ - * / % **` |
| Assignment | `= += -= *= /= %=` |
| Comparison | `== === != !== > < >= <=` |
| Logical | `&& \|\| !` |
| Unary | `+ - ++ -- typeof` |
| Ternary | `condition ? a : b` |
