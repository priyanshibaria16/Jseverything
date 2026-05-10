# 🧠 Objects - Complete Guide

Master objects: the foundation of structured data in JavaScript.

---

## 📚 Quick Contents

1. [What are Objects?](#what-are-objects)
2. [Key-Value Structure](#key-value-structure)
3. [Dot vs Bracket Notation](#dot-vs-bracket-notation)
4. [Nesting & Deep Access](#nesting--deep-access)
5. [Object Destructuring](#object-destructuring)
6. [Looping Through Objects](#looping-through-objects)
7. [Copying Objects](#copying-objects)
8. [Optional Chaining](#optional-chaining)
9. [Computed Properties](#computed-properties)
10. [Common Confusions](#common-confusions)
11. [Practical Examples](#practical-examples)

---

## ❓ What are Objects?

Objects are collections of key-value pairs, like real-world records.

Perfect for storing structured data: student profiles, products, user accounts, etc.

**Analogy**: Contact card
- **Keys** = Labels (name, phone, email)
- **Values** = Information (John, 555-1234, john@example.com)

```javascript
// Object of a student
let student = {
  name: "Ravi",
  age: 21,
  isEnrolled: true,
  marks: 85
};

// Object of a product
let product = {
  id: 1,
  name: "Laptop",
  price: 50000,
  inStock: true
};

// Object of a user
let user = {
  username: "john_doe",
  email: "john@example.com",
  isActive: true,
  createdAt: "2024-01-15"
};
```

**Why use objects?**
- ✅ Group related data together
- ✅ Access data by meaningful names (not just indexes)
- ✅ Easy to represent real-world entities
- ✅ Flexible structure

---

## 🔑 Key-Value Structure

### Creating Objects

```javascript
// Literal syntax (preferred)
let student = {
  name: "Ravi",
  age: 21,
  isEnrolled: true
};

// Using constructor
let person = new Object();
person.name = "John";
person.age = 30;

// Empty object
let empty = {};

// With various value types
let mixed = {
  string: "hello",
  number: 42,
  boolean: true,
  array: [1, 2, 3],
  object: { nested: "value" },
  function: () => console.log("Hi"),
  null: null,
  undefined: undefined
};
```

### Understanding Keys

Keys are **always strings** (even if you write them differently).

```javascript
let obj = {
  name: "John",        // key is "name"
  123: "number",       // key is "123" (string)
  "full name": "John Doe" // key is "full name" (needs quotes)
};

console.log(obj.name);           // "John"
console.log(obj[123]);           // "number" (converted to string)
console.log(obj["full name"]);   // "John Doe" (multi-word key)
```

### Accessing Values

```javascript
let student = {
  name: "Ravi",
  age: 21,
  marks: 85
};

// Dot notation
console.log(student.name); // "Ravi"

// Bracket notation
console.log(student["age"]); // 21

// Both equivalent
console.log(student.marks === student["marks"]); // true

// Check if property exists
console.log("name" in student); // true
console.log("email" in student); // false
console.log(student.email); // undefined
```

### Adding & Updating Properties

```javascript
let student = { name: "Ravi" };

// Add new property
student.age = 21;
student["marks"] = 85;

// Update existing
student.name = "Ravi Kumar";

// Multi-word keys
student["full name"] = "Ravi Kumar Singh";

console.log(student);
// {
//   name: "Ravi Kumar",
//   age: 21,
//   marks: 85,
//   "full name": "Ravi Kumar Singh"
// }

// Delete property
delete student.marks;
console.log(student.marks); // undefined
```

---

## 📍 Dot vs Bracket Notation

### Dot Notation (.)

Use for:
- Fixed, known property names
- Valid identifier names (no spaces, no special chars)
- Cleaner, more readable

```javascript
let person = { name: "John", age: 30 };

// ✅ Use dot notation
console.log(person.name); // "John"
console.log(person.age);  // 30

person.city = "NYC"; // Add property
```

### Bracket Notation ([])

Use for:
- Dynamic/variable keys
- Multi-word keys
- Keys with spaces or special characters
- Keys starting with numbers

```javascript
// Multi-word keys (need bracket notation)
let student = {};
student["full name"] = "John Doe";  // ✅ Works
student["exam-1"] = 85;            // ✅ Works
student["email@"] = "john@example.com"; // ✅ Works

// Dynamic keys
let key = "name";
let obj = {};
obj[key] = "Ravi"; // Sets obj.name = "Ravi"

console.log(obj.name); // "Ravi"

// Choosing key dynamically
let user = {
  profile: { phone: "123-456", email: "john@example.com" },
  settings: { theme: "dark", notifications: true }
};

let section = "profile";
let field = "phone";

// Access dynamically
console.log(user[section][field]); // "123-456"
```

### Comparison

```javascript
// ✅ Use dot notation (readable)
let user = { name: "John", age: 30 };
console.log(user.name);

// ✅ Use bracket for dynamic keys
let key = "name";
console.log(user[key]); // Same as user.name

// ❌ This doesn't work with dot for dynamic
let key2 = "name";
console.log(user.key2); // undefined (looks for property "key2")
```

---

## 🏗️ Nesting & Deep Access

Objects can contain other objects, creating hierarchical data.

```javascript
let user = {
  name: "Amit",
  address: {
    city: "Delhi",
    pincode: 110001,
    country: "India"
  },
  contact: {
    phone: "9999999999",
    email: "amit@example.com"
  }
};

// Access nested properties
console.log(user.address.city); // "Delhi"
console.log(user.contact.email); // "amit@example.com"
console.log(user.address.pincode); // 110001

// Bracket notation with nested
console.log(user["address"]["city"]); // "Delhi"

// Mixed
console.log(user.address["pincode"]); // 110001
```

### Deep Nesting

```javascript
let company = {
  name: "TechCorp",
  departments: {
    it: {
      manager: {
        name: "John",
        email: "john@techcorp.com",
        experience: {
          years: 10,
          certifications: ["AWS", "Azure"]
        }
      }
    }
  }
};

// Deep access
console.log(company.departments.it.manager.name); // "John"
console.log(company.departments.it.manager.experience.years); // 10
console.log(company.departments.it.manager.experience.certifications[0]); // "AWS"
```

### Updating Nested Properties

```javascript
let user = {
  address: {
    city: "Delhi"
  }
};

// Update nested
user.address.city = "Mumbai";
console.log(user.address.city); // "Mumbai"

// Add nested property
user.address.state = "Maharashtra";

// Create nested structure
user.profile = {};
user.profile.bio = "Software Developer";
user.profile.avatar = "https://...";
```

---

## ✂️ Object Destructuring

Extract values from objects into variables.

### Basic Destructuring

```javascript
let student = {
  name: "Ravi",
  age: 21,
  marks: 85
};

// Extract variables
let { name, age } = student;
console.log(name); // "Ravi"
console.log(age);  // 21

// All at once
let { name, age, marks } = student;
console.log(name, age, marks); // "Ravi", 21, 85

// Only what you need
let { name } = student;
console.log(name); // "Ravi"
```

### Renaming Properties

```javascript
let user = { name: "John", email: "john@example.com" };

// Rename during destructuring
let { name: fullName, email: userEmail } = user;
console.log(fullName); // "John"
console.log(userEmail); // "john@example.com"
```

### Default Values

```javascript
let user = { name: "John" };

// Default values
let { name, age = 25 } = user;
console.log(name); // "John"
console.log(age);  // 25 (default)

// Overriding default
let user2 = { name: "Sarah", age: 30 };
let { name: n, age: a = 25 } = user2;
console.log(a); // 30 (not default)
```

### Nested Destructuring

```javascript
let user = {
  name: "Amit",
  address: {
    city: "Delhi",
    pincode: 110001
  }
};

// Destructure nested properties
let { address: { city, pincode } } = user;
console.log(city); // "Delhi"
console.log(pincode); // 110001

// Rename nested
let { address: { city: userCity } } = user;
console.log(userCity); // "Delhi"
```

### In Function Parameters

```javascript
// Without destructuring
function greet(person) {
  console.log(person.name);
}

// With destructuring
function greet({ name, age }) {
  console.log(`${name} is ${age}`);
}

greet({ name: "John", age: 30 }); // "John is 30"

// With defaults
function displayUser({ name = "Guest", role = "User" } = {}) {
  console.log(`${name} - ${role}`);
}

displayUser({ name: "Admin" }); // "Admin - User"
displayUser(); // "Guest - User"
```

---

## 🔁 Looping Through Objects

### for-in Loop

```javascript
let student = {
  name: "Ravi",
  age: 21,
  marks: 85
};

for (let key in student) {
  console.log(key + ": " + student[key]);
}
// Output:
// name: Ravi
// age: 21
// marks: 85
```

### Object.keys()

Returns array of property names.

```javascript
let student = { name: "Ravi", age: 21, marks: 85 };

let keys = Object.keys(student);
console.log(keys); // ["name", "age", "marks"]

// Loop through keys
keys.forEach(key => {
  console.log(`${key}: ${student[key]}`);
});
```

### Object.values()

Returns array of property values.

```javascript
let student = { name: "Ravi", age: 21, marks: 85 };

let values = Object.values(student);
console.log(values); // ["Ravi", 21, 85]

// Sum numeric values
let marks = { math: 85, english: 92, science: 88 };
let total = Object.values(marks).reduce((sum, val) => sum + val, 0);
console.log(total); // 265
```

### Object.entries()

Returns array of [key, value] pairs.

```javascript
let student = { name: "Ravi", age: 21, marks: 85 };

let entries = Object.entries(student);
console.log(entries);
// [["name", "Ravi"], ["age", 21], ["marks", 85]]

// Loop with entries
entries.forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});
```

---

## 📦 Copying Objects

### Shallow Copy

Copies only the first level. Nested objects still reference originals.

```javascript
let original = { name: "John", age: 30, city: "NYC" };

// Method 1: Spread operator
let copy1 = { ...original };

// Method 2: Object.assign()
let copy2 = Object.assign({}, original);

// Both create new object
copy1.name = "Sarah";
console.log(original.name); // "John" - unchanged
console.log(copy1.name);    // "Sarah"
```

### Shallow Copy Problem with Nested Objects

```javascript
let original = {
  name: "John",
  address: { city: "NYC", state: "NY" }
};

let copy = { ...original };

// Modify nested object
copy.address.city = "Boston";

// Original also changed!
console.log(original.address.city); // "Boston" (PROBLEM!)
// Both reference the same address object
```

### Deep Copy

Copies all levels, including nested objects.

```javascript
let original = {
  name: "John",
  address: { city: "NYC", state: "NY" }
};

// Method 1: JSON stringify/parse
let deepCopy = JSON.parse(JSON.stringify(original));

// Method 2: Recursive function
function deepCopyRecursive(obj) {
  if (obj === null || typeof obj !== "object") return obj;
  if (obj instanceof Array) return obj.map(item => deepCopyRecursive(item));
  
  let copy = {};
  for (let key in obj) {
    copy[key] = deepCopyRecursive(obj[key]);
  }
  return copy;
}

let copy1 = deepCopy;
copy1.address.city = "Boston";

console.log(original.address.city); // "NYC" - unchanged!
```

⚠️ **Limitation of JSON method**:
```javascript
let obj = {
  name: "John",
  greet: () => console.log("Hi"),  // Functions not copied
  date: new Date(),                 // Becomes string
  value: undefined                  // Becomes null
};

let copy = JSON.parse(JSON.stringify(obj));
// Functions, undefined, and special objects are lost!
```

---

## ❓ Optional Chaining

Access nested properties safely without errors.

```javascript
let user = {
  name: "John",
  address: {
    city: "NYC"
  }
};

// Without optional chaining (risky)
console.log(user.profile.email); // ERROR! profile doesn't exist

// With optional chaining (safe)
console.log(user.profile?.email); // undefined (no error)
console.log(user.address?.city); // "NYC"

// Multiple levels
console.log(user?.address?.city?.name); // undefined (no error)

// With methods
let person = { greet: () => "Hi" };
person?.greet?.(); // Works

let person2 = null;
person2?.greet?.(); // No error, returns undefined
```

---

## 🧮 Computed Properties

Use variables as object keys.

```javascript
// Static key
let obj1 = { name: "John" };

// Dynamic key using variable
let key = "age";
let obj2 = {
  [key]: 30  // Uses value of variable as key
};

console.log(obj2.age); // 30

// Computed property with expression
let field = "marks";
let report = {
  [field]: 85,
  [field + "_percentage"]: 85
};

console.log(report);
// { marks: 85, marks_percentage: 85 }

// Useful for loops
let formData = {};
["name", "email", "phone"].forEach(field => {
  formData[field] = null; // Create properties dynamically
});

console.log(formData);
// { name: null, email: null, phone: null }
```

---

## ⚠️ Common Confusions

### ❌ Shallow Copy Doesn't Copy Nested Objects

```javascript
let original = {
  name: "John",
  skills: ["JS", "Python"] // Array is an object!
};

let copy = { ...original };

// Modify nested array
copy.skills.push("Java");

// Original also changed!
console.log(original.skills); // ["JS", "Python", "Java"]
// Both reference the same array!
```

### ❌ for-in Includes Inherited Properties

```javascript
let person = { name: "John", age: 30 };

// Add inherited property (not recommended)
Object.prototype.inherited = "value";

for (let key in person) {
  console.log(key); // Prints: name, age, inherited
}

// Solution: Use hasOwnProperty()
for (let key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(key); // Prints: name, age (not inherited)
  }
}

// Better: Use Object.keys()
Object.keys(person).forEach(key => {
  console.log(key); // Prints: name, age (not inherited)
});
```

### ❌ delete Removes Property But Not From Arrays

```javascript
let obj = { a: 1, b: 2, c: 3 };
delete obj.b;

console.log(obj); // { a: 1, c: 3 }
console.log("b" in obj); // false

// With arrays - creates hole, doesn't remove
let arr = [1, 2, 3];
delete arr[1];

console.log(arr); // [1, empty, 3] - has hole!
console.log(arr.length); // 3 (length unchanged)

// Better: Use splice() for arrays
arr.splice(1, 1);
```

### ❌ Spread is NOT Deep Copy

```javascript
let original = {
  name: "John",
  address: { city: "NYC" }
};

let copy = { ...original };

// Nested objects still reference original
copy.address.city = "Boston";
console.log(original.address.city); // "Boston" - CHANGED!
```

---

## 🎯 Practical Examples

### Example 1: User Profile

```javascript
let user = {
  id: 1,
  name: "John Doe",
  email: "john@example.com",
  profile: {
    avatar: "https://...",
    bio: "Software Developer",
    social: {
      twitter: "@johndoe",
      github: "johndoe"
    }
  },
  preferences: {
    theme: "dark",
    notifications: true,
    language: "en"
  }
};

// Access deeply
console.log(user.profile.social.twitter); // "@johndoe"

// Destructure
let { name, email, profile: { bio } } = user;
console.log(name, bio); // "John Doe", "Software Developer"

// Loop preferences
Object.entries(user.preferences).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});

// Safe access
console.log(user.profile?.premium?.status); // undefined (no error)
```

### Example 2: Product Inventory

```javascript
let products = [
  { id: 1, name: "Laptop", price: 50000, stock: 5 },
  { id: 2, name: "Mouse", price: 500, stock: 50 },
  { id: 3, name: "Keyboard", price: 1500, stock: 20 }
];

// Find product
let product = products.find(p => p.id === 2);
console.log(product.name); // "Mouse"

// Update stock
product.stock -= 1;

// Calculate total value
let totalValue = products.reduce((sum, p) => sum + (p.price * p.stock), 0);
console.log(totalValue);

// Group by price range
let byPrice = {
  budget: products.filter(p => p.price < 1000),
  standard: products.filter(p => p.price >= 1000 && p.price < 10000),
  premium: products.filter(p => p.price >= 10000)
};
```

### Example 3: Form Data Handling

```javascript
let formData = {
  personal: {
    firstName: "John",
    lastName: "Doe",
    dob: "1990-01-15"
  },
  contact: {
    email: "john@example.com",
    phone: "9999999999"
  },
  preferences: {
    newsletter: true,
    smsNotifications: false
  }
};

// Validate form
function validateForm(data) {
  const errors = {};
  
  if (!data.personal.firstName) errors.firstName = "Required";
  if (!data.contact.email) errors.email = "Required";
  
  return Object.keys(errors).length === 0;
}

// Flatten object
function flatten(obj, parent = '', result = {}) {
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      let newKey = parent ? `${parent}.${key}` : key;
      if (typeof obj[key] === 'object') {
        flatten(obj[key], newKey, result);
      } else {
        result[newKey] = obj[key];
      }
    }
  }
  return result;
}

console.log(flatten(formData));
// {
//   'personal.firstName': 'John',
//   'personal.lastName': 'Doe',
//   'contact.email': 'john@example.com',
//   ...
// }
```

---

## 📊 Object Methods Cheat Sheet

| Method | Purpose | Returns |
|--------|---------|---------|
| Object.keys() | Get all keys | Array of keys |
| Object.values() | Get all values | Array of values |
| Object.entries() | Get key-value pairs | Array of [key, value] |
| Object.assign() | Copy/merge objects | Merged object |
| Object.freeze() | Make immutable | Original object |
| Object.seal() | Prevent add/remove | Original object |
| hasOwnProperty() | Check property exists | Boolean |
| in | Check property exists | Boolean |
| delete | Remove property | Boolean |

---

## 🧠 Mindset

**Objects = Structured State**

Think of objects as blueprints:
- Use for modeling real-world entities (user, product, etc.)
- Keep structures predictable and documented
- Use destructuring for cleaner code
- Use optional chaining for safe access
- Understand shallow vs deep copy
- Know when to use dot vs bracket notation

Objects are fundamental to JavaScript. Master them to master data management! 🚀

---

**Objects are everywhere in JavaScript – databases, APIs, components. Master them! 💪**
