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
