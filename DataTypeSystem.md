# Data Types in JavaScript

---

## What Are Data Types in JavaScript?

In JavaScript, every value has a data type.
It defines:
- What kind of value is stored
- What operations can be performed on it

JavaScript is a **dynamically typed language**
→ You don't need to declare data types explicitly.
```js
let x = 10;     // number
x = "hello";    // now string
```

---

## Categories of Data Types

JavaScript has 2 main categories:

| Category | Description |
|---|---|
| **Primitive** | Simple, immutable, stored directly |
| **Reference** | Complex, stored via memory reference |

---

## 1. Primitive Data Types

- Stored by value
- Immutable (cannot be changed)

---

### String (Text)

Used to store textual data.
```js
let name = "Priyanshi";
let city = 'Anand';
```

**Features:**
- Can use single (`''`) or double (`""`) quotes
- Strings are immutable
```js
let str = "hello";
str[0] = "H"; // no change
```

---

### Number

Represents both integers and floating-point numbers.
```js
let a = 10;
let b = -5;
let c = 3.14;
```

**Special Values:**
- `Infinity`
- `-Infinity`
- `NaN`

---

### Boolean

Represents logical values.
```js
let isActive = true;
let isLogin = false;
```

**Used in:**
- Conditions
- Comparisons

---

### Undefined

A variable declared but not assigned.
```js
let x;
console.log(x); // undefined
```

---

### Null

Represents intentional absence of value.
```js
let data = null;
```

**Difference:**

| `undefined` | `null` |
|---|---|
| Default value | Assigned manually |

---

### Symbol (ES6)

Used to create unique identifiers.
```js
let id1 = Symbol("id");
let id2 = Symbol("id");

console.log(id1 === id2); // false
```

---

### BigInt (ES11)

Used for very large integers beyond Number limit.
```js
let big = 123456789012345678901234567890n;
```

---

## 2. Reference Data Types

- Stored by reference (memory address)
- Mutable

---

### Object

Collection of key-value pairs.
```js
let person = {
  name: "Priyanshi",
  age: 20
};
```

---

### Array

Ordered collection of values.
```js
let arr = [10, 20, 30];
```

---

### Function

Functions are also objects in JavaScript.
```js
function greet() {
  console.log("Hello");
}
```

---

## Primitive vs Reference (Important)

| Feature | Primitive | Reference |
|---|---|---|
| Storage | Direct | Memory reference |
| Mutability | Immutable | Mutable |
| Copy | Value copy | Reference copy |

**Example:**
```js
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 

let obj1 = { name: "A" };
let obj2 = obj1;
obj2.name = "B";
console.log(obj1.name); // "B" 
```

---

## typeof Operator

Used to check data type:
```js
typeof "hello"      // "string"
typeof 100          // "number"
typeof true         // "boolean"
typeof undefined    // "undefined"
typeof null         // "object" ❗ bug
typeof []           // "object"
typeof {}           // "object"
typeof function(){} // "function"
```

**Important Bug:**
```js
typeof null === "object" // historical bug
```

---

## Type Coercion (Automatic Conversion)

JavaScript automatically converts types.

### 1. Implicit Coercion
```js
"5" + 1       // "51"
"5" - 1       // 4
true + 1      // 2
null + 1      // 1
undefined + 1 // NaN
```

### 2. Explicit Conversion
```js
Number("123")  // 123
String(123)    // "123"
Boolean(0)     // false
```

---

## Equality Operators

### Loose Equality (`==`)
Converts type before comparing
```js
5 == "5" // true
```

### Strict Equality (`===`)
No type conversion
```js
5 === "5" // false
```

Always prefer `===`

---

## NaN (Not a Number)
```js
typeof NaN // "number"
```

**Occurs when:**
- `0 / 0`
- `parseInt("abc")`

---

## Truthy & Falsy Values

### Falsy Values (IMPORTANT)
- `false`
- `0`
- `""`
- `null`
- `undefined`
- `NaN`

### Truthy Values

Everything else:
- `"0"`
- `"false"`
- `[]`
- `{}`
- `function(){}`

**Example:**
```js
if ("0") {
  console.log("Runs"); //  truthy
}
```

---

##  Important Interview Tricky Cases
```js
[] == false        // true
null == undefined  // true
NaN == NaN         // false
```

---

##  Memory Concept (Deep Understanding)

**Primitive:**
- Stored directly in stack memory

**Reference:**
- Stored in heap, variable stores address

---

##  Best Practices

- Always use `===`
- Avoid unnecessary type coercion
- Check types using `typeof`
- Be careful with truthy/falsy values

```markdown
# JavaScript — Deep Concepts

---

## 1. Why `typeof null` is `"object"` (Bug)

### Output

```js
typeof null // "object"
```

### Why?

This is a **historical bug** in JavaScript from its early days (1995).

Internally, JavaScript used a **type tagging system:**
- Objects were represented with a specific tag (`0`)
- `null` was represented as **all zero bits** (`0`)

So JavaScript mistakenly treated `null` as an object.

### Important
- This is **not correct** logically
- But it **cannot be fixed** now because it would break existing code

### Example

```js
let x = null;

if (typeof x === "object") {
  console.log("This is misleading!");
}
```

Even though it prints `"object"`, **null is NOT an object** — it's a primitive

---

## 2. `undefined` vs `null`

### `undefined`

Means: A variable is declared but **no value is assigned**

```js
let a;
console.log(a); // undefined
```

Also happens when:

```js
function test() {}
console.log(test()); // undefined (no return)
```

---

### `null`

Means: You **intentionally assign** "no value"

```js
let b = null;
console.log(b); // null
```

---

### Key Difference

| Feature | `undefined` | `null` |
|---|---|---|
| Assigned by | JavaScript | Developer |
| Meaning | Not assigned | Empty intentionally |
| Type | `undefined` | `object` (bug) |

---

### Practical Example

```js
let user;

if (user === undefined) {
  console.log("User not defined yet");
}
// Output: "User not defined yet"

user = null;

if (user === null) {
  console.log("User intentionally removed");
}
// Output: "User intentionally removed"
```

---

## 3. Why `'5' + 1 = "51"` but `'5' - 1 = 4`

This is due to **type coercion** (automatic conversion).

---

### Case 1: `'5' + 1`

```js
"5" + 1 // "51"
```

### Why?

`+` operator works for:
- Addition
- String concatenation

If one operand is a string, JS converts **everything to string**

```js
"5" + 1
→ "5" + "1"
→ "51"
```

---

### Case 2: `'5' - 1`

```js
"5" - 1 // 4
```

### Why?

`-` operator **only works with numbers**
 So JavaScript converts string → number

```js
"5" - 1
→ 5 - 1
→ 4
```

---

### More Examples

```js
"10" * 2   // Output: 20
"10" / 2   // Output: 5
"10" - "5" // Output: 5
```

All arithmetic operators **force number conversion**

---

### Special Case

```js
"hello" - 1 // Output: NaN
```

 Because `"hello"` **cannot convert** to a number

---

### Final Concept (VERY IMPORTANT)

**JavaScript Rule:**

| Operator | Behavior |
|---|---|
| `+` | String + Number → String |
| `- * /` | Always convert to Number |

---

## Combined Example

```js
let x = null;
let y;

console.log(typeof x); // Output: "object"
console.log(typeof y); // Output: "undefined"

console.log("5" + 1);  // Output: "51"
console.log("5" - 1);  // Output: 4
```
```
