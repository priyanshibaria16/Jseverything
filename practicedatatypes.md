# JavaScript Practice Zone — Complete Notes

## 1. Predict the Output

### `null + 1`

```js
console.log(null + 1); // 1
```

**Output:** `1`

**Why:** `null` is coerced to `0` in arithmetic operations. So `0 + 1 = 1` (type: `number`).

---

### `"5" + 3`

```js
console.log("5" + 3); // "53"
```

**Output:** `"53"`

**Why:** The `+` operator checks its operands left to right. When it sees a string (`"5"`), it switches to **string concatenation** mode. So `3` gets coerced to `"3"` and the result is `"53"` (type: `string`).

> ⚠️ `+` is the only arithmetic operator that doubles as concatenation. This is a very common source of bugs.

---

### `"5" - 3`

```js
console.log("5" - 3); // 2
```

**Output:** `2`

**Why:** `-` has no meaning for strings, so JS coerces `"5"` → `5` (number). Then `5 - 3 = 2` (type: `number`).

---

### `true + false`

```js
console.log(true + false); // 1
```

**Output:** `1`

**Why:** Booleans are coerced to numbers in arithmetic. `true → 1`, `false → 0`. So `1 + 0 = 1`.

---

### Summary Table

| Expression | Output | Type | Reason |
|---|---|---|---|
| `null + 1` | `1` | number | `null` → `0` |
| `"5" + 3` | `"53"` | string | `+` concatenates when string present |
| `"5" - 3` | `2` | number | `-` forces numeric coercion |
| `true + false` | `1` | number | `true` → `1`, `false` → `0` |

---

## 2. Check Types with `typeof`

### `typeof []`

```js
console.log(typeof []); // "object"
```

**Output:** `"object"`

**Why:** Arrays are objects in JavaScript. `typeof` cannot distinguish arrays from plain objects.

**How to detect arrays instead:**

```js
Array.isArray([]);   // true  ✅
Array.isArray({});   // false ✅
```

---

### `typeof null`

```js
console.log(typeof null); // "object"
```

**Output:** `"object"`

**Why:** This is a **historic bug** from JavaScript's first release in 1995. The internal type tag for `null` was `0` — same as for objects. It was never fixed to avoid breaking existing code.

**How to check for null:**

```js
value === null    // ✅ correct
typeof value === "object" && !value  // works, but verbose
```

---

### `typeof 123n`

```js
console.log(typeof 123n); // "bigint"
```

**Output:** `"bigint"`

**Why:** The `n` suffix creates a **BigInt** literal — a separate primitive type for arbitrarily large integers. `typeof` correctly returns `"bigint"`.

```js
123n + 1n   // 124n  ✅
123n + 1    // ❌ TypeError — cannot mix BigInt and Number
```

---

### `typeof` Quick Reference

| Value | `typeof` result | Notes |
|---|---|---|
| `42` | `"number"` | — |
| `"hello"` | `"string"` | — |
| `true` | `"boolean"` | — |
| `undefined` | `"undefined"` | — |
| `null` | `"object"` | ⚠️ historic bug |
| `[]` | `"object"` | ⚠️ use `Array.isArray()` |
| `{}` | `"object"` | — |
| `function(){}` | `"function"` | special case |
| `123n` | `"bigint"` | — |
| `Symbol()` | `"symbol"` | — |

---

## 3. Truthy or Falsy?

JavaScript has **exactly 6 falsy values**. Everything else is truthy.

### The Six Falsy Values

```
false | 0 | 0n | "" | null | undefined | NaN
```

### Examples

```js
console.log(Boolean(0));         // false ❌ — 0 is falsy
console.log(Boolean("0"));       // true  ✅ — non-empty string, always truthy
console.log(Boolean([]));        // true  ✅ — empty array is an object reference
console.log(Boolean(undefined)); // false ❌ — undefined is falsy
```

### Common Gotchas

| Expression | Boolean | Why |
|---|---|---|
| `Boolean(0)` | `false` | `0` is falsy |
| `Boolean("0")` | `true` | non-empty string → truthy |
| `Boolean([])` | `true` | objects (even empty) → truthy |
| `Boolean({})` | `true` | same — object reference |
| `Boolean("")` | `false` | empty string → falsy |
| `Boolean(null)` | `false` | null → falsy |
| `Boolean(NaN)` | `false` | NaN → falsy |
| `Boolean(-1)` | `true` | any non-zero number → truthy |

> 💡 `"0"` is truthy but `0` is falsy. This trips up beginners when reading user input from forms (which always returns strings).

---

## 4. `isEmpty(value)` Function

Write a function that returns `true` if a value is `null`, `undefined`, or `""`.

### Solution

```js
function isEmpty(value) {
  return value === null || value === undefined || value === "";
}
```

### Test Cases

```js
isEmpty(null);      // true  ✅
isEmpty(undefined); // true  ✅
isEmpty("");        // true  ✅
isEmpty("hello");   // false ✅
isEmpty(0);         // false ✅ — 0 is not "empty" by this definition
isEmpty([]);        // false ✅ — [] is not null/undefined/""
isEmpty({});        // false ✅
```

### Alternative Using `==` (shorter, but less explicit)

```js
function isEmpty(value) {
  return value == null || value === "";
}
// value == null catches both null AND undefined (loose equality)
```

> ⚠️ Use `===` in production for clarity. The `== null` shortcut is common in codebases but requires knowing why it works.

---

## 5. Loose `==` vs Strict `===`

### The Difference

| Operator | Name | What it does |
|---|---|---|
| `==` | Loose equality | Coerces types before comparing |
| `===` | Strict equality | No coercion — types must match |

### Examples

```js
console.log(5 == "5");  // true  — "5" coerced to 5, then 5 == 5
console.log(5 === "5"); // false — number ≠ string, no coercion
```

### Why `===` is Preferred

```js
// Surprising == results
0 == false      // true
"" == false     // true
null == undefined // true
[] == false     // true
[] == 0         // true

// === has no surprises
0 === false     // false
"" === false    // false
null === undefined // false
```

### `==` Coercion Rules (Abstract Equality Algorithm)

1. If same type → compare directly (same as `===`)
2. `null == undefined` → always `true`
3. Number vs String → coerce string to number
4. Boolean vs anything → coerce boolean to number first
5. Object vs primitive → call `.valueOf()` or `.toString()`

### Rule of Thumb

> **Always use `===`** unless you specifically want type coercion. Most linters (ESLint) enforce this with the `eqeqeq` rule.

---

## Summary

| Topic | Key Takeaway |
|---|---|
| `+` with strings | Switches to concatenation — use `Number()` to force numeric |
| `typeof null` | Returns `"object"` — use `=== null` to check |
| `typeof []` | Returns `"object"` — use `Array.isArray()` |
| Falsy values | Only 6: `false, 0, 0n, "", null, undefined, NaN` |
| `"0"` is truthy | Non-empty string — always truthy |
| `[]` is truthy | Object reference — always truthy |
| `isEmpty()` | Check `=== null`, `=== undefined`, `=== ""` explicitly |
| `==` vs `===` | Prefer `===` — avoids implicit coercion surprises |
