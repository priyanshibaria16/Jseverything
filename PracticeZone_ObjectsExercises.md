# 🧪 Practice Zone - Objects Exercises

10 practical object exercises with complete solutions and explanations.

---

## 1️⃣ Create an Object for a Book

**Problem**: Create an object to store book information (title, author, price).

```javascript
// Basic book object
let book = {
  title: "JavaScript: The Good Parts",
  author: "Douglas Crockford",
  price: 599
};

console.log(book);
// { title: "JavaScript: The Good Parts", author: "Douglas Crockford", price: 599 }

// More detailed book object
let book2 = {
  title: "Eloquent JavaScript",
  author: "Marijn Haverbeke",
  price: 450,
  pages: 472,
  published: 2018,
  language: "English",
  isbn: "978-1593275844"
};

// Array of book objects
let books = [
  { title: "JavaScript: The Good Parts", author: "Douglas Crockford", price: 599 },
  { title: "Eloquent JavaScript", author: "Marijn Haverbeke", price: 450 },
  { title: "You Don't Know JS", author: "Kyle Simpson", price: 549 }
];

// Function to create book object
function createBook(title, author, price) {
  return { title, author, price }; // Shorthand property names
}

let myBook = createBook("Clean Code", "Robert Martin", 699);
console.log(myBook);
// { title: "Clean Code", author: "Robert Martin", price: 699 }

// With methods
let book3 = {
  title: "JavaScript: The Good Parts",
  author: "Douglas Crockford",
  price: 599,
  getInfo: function() {
    return `${this.title} by ${this.author} - $${this.price}`;
  },
  applyDiscount: function(percent) {
    return this.price * (1 - percent / 100);
  }
};

console.log(book3.getInfo());           // "JavaScript: The Good Parts by Douglas Crockford - $599"
console.log(book3.applyDiscount(10));   // 539.1
```

---

## 2️⃣ Access Properties Using Both Dot and Bracket

**Problem**: Access object properties using dot notation and bracket notation.

```javascript
let book = {
  title: "JavaScript Fundamentals",
  author: "John Smith",
  price: 599,
  "published year": 2022  // Multi-word key
};

// ✅ DOT NOTATION
console.log(book.title);    // "JavaScript Fundamentals"
console.log(book.author);   // "John Smith"
console.log(book.price);    // 599

// ✅ BRACKET NOTATION
console.log(book["title"]);    // "JavaScript Fundamentals"
console.log(book["author"]);   // "John Smith"
console.log(book["price"]);    // 599

// MUST use bracket for multi-word keys
console.log(book["published year"]); // 2022

// ❌ This doesn't work with multi-word keys
// console.log(book.published year); // ERROR!

// Dynamic access with bracket
let property = "author";
console.log(book[property]); // "John Smith"

// Checking existence
console.log("title" in book);      // true
console.log("pages" in book);      // false
console.log(book.pages);           // undefined
console.log(book["pages"]);        // undefined

// Loop and access all properties
let properties = ["title", "author", "price", "published year"];
properties.forEach(prop => {
  console.log(`${prop}: ${book[prop]}`);
});
// Output:
// title: JavaScript Fundamentals
// author: John Smith
// price: 599
// published year: 2022
```

---

## 3️⃣ Write a Nested Object (User with Address and Location)

**Problem**: Create nested object structure for user with address and location details.

```javascript
// Nested user object
let user = {
  id: 1,
  name: "John Doe",
  email: "john@example.com",
  address: {
    street: "123 Main Street",
    city: "New York",
    state: "NY",
    pincode: 10001,
    location: {
      latitude: 40.7128,
      longitude: -74.0060,
      timezone: "EST"
    }
  },
  phone: "555-1234"
};

// Access nested properties
console.log(user.name);              // "John Doe"
console.log(user.address.city);      // "New York"
console.log(user.address.location.latitude); // 40.7128

// Multi-level access
console.log(user["address"]["location"]["timezone"]); // "EST"

// Update nested property
user.address.city = "Boston";
user.address.location.latitude = 42.3601;

// Add new nested property
user.address.country = "USA";

// Create another user with similar structure
let users = [
  {
    id: 1,
    name: "Alice",
    address: {
      city: "San Francisco",
      location: { latitude: 37.7749, longitude: -122.4194 }
    }
  },
  {
    id: 2,
    name: "Bob",
    address: {
      city: "Los Angeles",
      location: { latitude: 34.0522, longitude: -118.2437 }
    }
  }
];

// Loop through users and access locations
users.forEach(user => {
  console.log(`${user.name}: ${user.address.city}`);
  console.log(`  Location: ${user.address.location.latitude}, ${user.address.location.longitude}`);
});
// Output:
// Alice: San Francisco
//   Location: 37.7749, -122.4194
// Bob: Los Angeles
//   Location: 34.0522, -118.2437

// Complex nested structure
let company = {
  name: "TechCorp",
  employees: [
    {
      name: "Manager 1",
      department: {
        name: "Engineering",
        projects: [
          { name: "Project A", status: "active" },
          { name: "Project B", status: "completed" }
        ]
      }
    }
  ]
};

console.log(company.employees[0].department.projects[1].name); // "Project B"
```

---

## 4️⃣ Destructure Name and Age from Student Object

**Problem**: Extract name and age properties from student object using destructuring.

```javascript
let student = {
  id: 1,
  name: "Ravi",
  age: 21,
  marks: 85,
  course: "JavaScript"
};

// Basic destructuring
let { name, age } = student;
console.log(name); // "Ravi"
console.log(age);  // 21

// Multiple properties
let { name, age, marks, course } = student;
console.log(name, age, marks, course);
// "Ravi", 21, 85, "JavaScript"

// Only specific properties
let { name, course } = student;
console.log(name, course);
// "Ravi", "JavaScript"

// Rename while destructuring
let { name: studentName, age: studentAge } = student;
console.log(studentName); // "Ravi"
console.log(studentAge);  // 21

// With default values
let { name, age, email = "ravi@example.com" } = student;
console.log(email); // "ravi@example.com" (default)

// Nested destructuring
let user = {
  name: "John",
  address: {
    city: "Delhi",
    state: "Delhi"
  }
};

let { name, address: { city, state } } = user;
console.log(name, city, state);
// "John", "Delhi", "Delhi"

// In function parameters
function displayStudent({ name, age }) {
  console.log(`${name} is ${age} years old`);
}

displayStudent(student);
// "Ravi is 21 years old"

// Function with defaults
function printInfo({ name = "Unknown", age = 0, marks = "--" } = {}) {
  console.log(`${name}: ${age} years, Marks: ${marks}`);
}

printInfo({ name: "Alice", age: 20, marks: 95 });
// "Alice: 20 years, Marks: 95"

printInfo({ name: "Bob" });
// "Bob: 0 years, Marks: --"

printInfo();
// "Unknown: 0 years, Marks: --"

// Array of students and destructure each
let students = [
  { name: "Alice", age: 20 },
  { name: "Bob", age: 21 },
  { name: "Charlie", age: 19 }
];

students.forEach(({ name, age }) => {
  console.log(`${name}: ${age}`);
});
// Alice: 20
// Bob: 21
// Charlie: 19
```

---

## 5️⃣ Loop Through Keys and Values of an Object

**Problem**: Iterate through object properties using different methods.

```javascript
let student = {
  name: "Ravi",
  age: 21,
  marks: 85,
  course: "JavaScript"
};

// Method 1: for-in loop
console.log("=== for-in loop ===");
for (let key in student) {
  console.log(`${key}: ${student[key]}`);
}
// Output:
// name: Ravi
// age: 21
// marks: 85
// course: JavaScript

// Method 2: Object.keys()
console.log("\n=== Object.keys() ===");
Object.keys(student).forEach(key => {
  console.log(`${key}: ${student[key]}`);
});

// Method 3: Object.values()
console.log("\n=== Object.values() ===");
Object.values(student).forEach(value => {
  console.log(value);
});
// Output:
// Ravi
// 21
// 85
// JavaScript

// Method 4: Object.entries()
console.log("\n=== Object.entries() ===");
Object.entries(student).forEach(([key, value]) => {
  console.log(`${key}: ${value}`);
});

// Get only keys
let keys = Object.keys(student);
console.log(keys); // ["name", "age", "marks", "course"]

// Get only values
let values = Object.values(student);
console.log(values); // ["Ravi", 21, 85, "JavaScript"]

// Get entries
let entries = Object.entries(student);
console.log(entries);
// [["name", "Ravi"], ["age", 21], ["marks", 85], ["course", "JavaScript"]]

// Count properties
console.log("Number of properties:", Object.keys(student).length); // 4

// Check if property exists
console.log("Has 'name'?", Object.keys(student).includes("name")); // true

// Transform values to uppercase
let uppercased = {};
Object.entries(student).forEach(([key, value]) => {
  uppercased[key] = typeof value === 'string' ? value.toUpperCase() : value;
});
console.log(uppercased);
// { name: "RAVI", age: 21, marks: 85, course: "JAVASCRIPT" }

// Sum numeric values
let numbers = { math: 85, english: 92, science: 88 };
let sum = Object.values(numbers).reduce((acc, val) => acc + val, 0);
console.log("Total marks:", sum); // 265

// Create new object from entries
let original = { a: 1, b: 2, c: 3 };
let doubled = Object.fromEntries(
  Object.entries(original).map(([key, val]) => [key, val * 2])
);
console.log(doubled); // { a: 2, b: 4, c: 6 }
```

---

## 6️⃣ Convert Object to Array Using Object.entries()

**Problem**: Convert object to array format using Object.entries().

```javascript
let student = {
  name: "Ravi",
  age: 21,
  marks: 85,
  course: "JavaScript"
};

// Convert to array of [key, value] pairs
let entries = Object.entries(student);
console.log(entries);
// [["name", "Ravi"], ["age", 21], ["marks", 85], ["course", "JavaScript"]]

// Array of keys only
let keys = Object.keys(student);
console.log(keys);
// ["name", "age", "marks", "course"]

// Array of values only
let values = Object.values(student);
console.log(values);
// ["Ravi", 21, 85, "JavaScript"]

// Transform entries to different format
let formatted = Object.entries(student).map(([key, value]) => ({
  property: key,
  value: value
}));
console.log(formatted);
// [
//   { property: "name", value: "Ravi" },
//   { property: "age", value: 21 },
//   { property: "marks", value: 85 },
//   { property: "course", value: "JavaScript" }
// ]

// Array of entries with filtered data
let filtered = Object.entries(student)
  .filter(([key, value]) => typeof value === 'number')
  .map(([key, value]) => [key, value]);
console.log(filtered);
// [["age", 21], ["marks", 85]]

// Create table-like structure
let tableData = Object.entries(student).map(([key, value]) => [
  key.toUpperCase(),
  value
]);
console.log(tableData);
// [["NAME", "Ravi"], ["AGE", 21], ["MARKS", 85], ["COURSE", "JavaScript"]]

// Convert array back to object
let newObj = Object.fromEntries(entries);
console.log(newObj);
// { name: "Ravi", age: 21, marks: 85, course: "JavaScript" }

// Filter and convert back
let filtered2 = Object.fromEntries(
  Object.entries(student).filter(([key, value]) => key !== "course")
);
console.log(filtered2);
// { name: "Ravi", age: 21, marks: 85 }

// Transform all values
let transformed = Object.fromEntries(
  Object.entries(student).map(([key, value]) => [
    key,
    value === "JavaScript" ? "JS" : value
  ])
);
console.log(transformed);
// { name: "Ravi", age: 21, marks: 85, course: "JS" }
```

---

## 7️⃣ Copy an Object Using Spread Operator

**Problem**: Create a shallow copy of an object using spread operator.

```javascript
let original = {
  name: "John",
  age: 30,
  city: "NYC"
};

// Copy using spread operator
let copy = { ...original };

console.log(copy);
// { name: "John", age: 30, city: "NYC" }

// Original unchanged when modifying copy
copy.name = "Sarah";
console.log(original.name); // "John" - unchanged
console.log(copy.name);     // "Sarah"

// Copy and add new properties
let extended = { ...original, country: "USA" };
console.log(extended);
// { name: "John", age: 30, city: "NYC", country: "USA" }

// Copy and override properties
let updated = { ...original, city: "Boston", state: "MA" };
console.log(updated);
// { name: "John", age: 30, city: "Boston", state: "MA" }

// Merge multiple objects
let personal = { name: "John", age: 30 };
let contact = { email: "john@example.com", phone: "555-1234" };
let merged = { ...personal, ...contact };
console.log(merged);
// { name: "John", age: 30, email: "john@example.com", phone: "555-1234" }

// Object property order matters
let obj1 = { a: 1, b: 2 };
let obj2 = { b: 3, c: 4 };
let combined = { ...obj1, ...obj2 };
console.log(combined); // { a: 1, b: 3, c: 4 } (obj2.b overrides obj1.b)

// Copy with Object.assign()
let copy2 = Object.assign({}, original);
console.log(copy2);
// { name: "John", age: 30, city: "NYC" }

// ⚠️ Shallow copy problem with nested objects
let original2 = {
  name: "John",
  address: { city: "NYC", state: "NY" }
};

let copy2 = { ...original2 };
copy2.address.city = "Boston";

console.log(original2.address.city); // "Boston" - CHANGED!
// Both reference the same address object

// Function to copy and extend
function extendObject(obj, properties) {
  return { ...obj, ...properties };
}

let user = { name: "Alice", age: 25 };
let extended2 = extendObject(user, { city: "SF", role: "Admin" });
console.log(extended2);
// { name: "Alice", age: 25, city: "SF", role: "Admin" }
```

---

## 8️⃣ Create a Deep Copy of an Object with Nested Structure

**Problem**: Create a deep copy that includes nested objects.

```javascript
let original = {
  name: "John",
  address: {
    city: "NYC",
    coordinates: {
      lat: 40.7128,
      long: -74.0060
    }
  },
  hobbies: ["reading", "gaming"]
};

// Method 1: JSON stringify/parse
let deepCopy1 = JSON.parse(JSON.stringify(original));

deepCopy1.address.city = "Boston";
deepCopy1.hobbies.push("coding");

console.log(original.address.city); // "NYC" - unchanged
console.log(original.hobbies); // ["reading", "gaming"] - unchanged
console.log(deepCopy1.address.city); // "Boston"
console.log(deepCopy1.hobbies); // ["reading", "gaming", "coding"]

// Method 2: Recursive function
function deepCopyRecursive(obj) {
  // Handle primitives and null
  if (obj === null || typeof obj !== 'object') {
    return obj;
  }

  // Handle arrays
  if (Array.isArray(obj)) {
    return obj.map(item => deepCopyRecursive(item));
  }

  // Handle objects
  let copy = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      copy[key] = deepCopyRecursive(obj[key]);
    }
  }
  return copy;
}

let deepCopy2 = deepCopyRecursive(original);
deepCopy2.address.coordinates.lat = 34.0522; // Los Angeles latitude

console.log(original.address.coordinates.lat); // 40.7128 - unchanged
console.log(deepCopy2.address.coordinates.lat); // 34.0522

// Method 3: Using spread and recursion
function deepCopySpread(obj) {
  if (obj === null || typeof obj !== 'object') return obj;

  if (Array.isArray(obj)) {
    return obj.map(item => deepCopySpread(item));
  }

  let copy = {};
  Object.entries(obj).forEach(([key, value]) => {
    copy[key] = deepCopySpread(value);
  });
  return copy;
}

let deepCopy3 = deepCopySpread(original);

// Complex nested structure
let user = {
  id: 1,
  profile: {
    name: "John",
    contact: {
      email: "john@example.com",
      phones: [
        { type: "mobile", number: "9999999999" },
        { type: "home", number: "1234567890" }
      ]
    }
  },
  permissions: ["read", "write"]
};

let userDeepCopy = deepCopyRecursive(user);
userDeepCopy.profile.contact.phones[0].number = "1111111111";

console.log(user.profile.contact.phones[0].number); // "9999999999"
console.log(userDeepCopy.profile.contact.phones[0].number); // "1111111111"

// Compare copies
console.log("Same reference?", original === deepCopy1); // false
console.log("Nested same reference?", original.address === deepCopy1.address); // false
```

---

## 9️⃣ Use Optional Chaining to Safely Access Deep Values

**Problem**: Access nested properties without errors using optional chaining.

```javascript
let user = {
  name: "John",
  address: {
    city: "NYC",
    location: {
      coordinates: {
        lat: 40.7128
      }
    }
  }
};

// ✅ WITH optional chaining
console.log(user?.address?.city); // "NYC"
console.log(user?.address?.location?.coordinates?.lat); // 40.7128

// ✅ Safe access to non-existent property
console.log(user?.profile?.avatar); // undefined (no error)
console.log(user?.address?.zip); // undefined (no error)

// ❌ WITHOUT optional chaining - ERRORS
// console.log(user.profile.avatar); // ERROR: Cannot read property 'avatar' of undefined
// console.log(user.address.zip.code); // ERROR: Cannot read property 'code' of undefined

// Optional chaining with arrays
let users = [
  { name: "Alice", email: "alice@example.com" },
  { name: "Bob" }
];

console.log(users[0]?.email); // "alice@example.com"
console.log(users[1]?.email); // undefined (no error)
console.log(users[5]?.email); // undefined (no error)

// Optional chaining with methods
let obj = {
  greet: () => "Hello"
};

console.log(obj?.greet?.()); // "Hello"
console.log(obj?.sayBye?.()); // undefined (no error)

// Optional chaining with array access
let data = {
  items: [
    { id: 1, name: "Item 1" },
    { id: 2, name: "Item 2" }
  ]
};

console.log(data?.items?.[0]?.name); // "Item 1"
console.log(data?.items?.[5]?.name); // undefined (no error)

// Combining with default values
let config = {
  theme: {
    primary: "#000"
  }
};

let primaryColor = config?.theme?.primary ?? "#fff"; // Use ?? for default
console.log(primaryColor); // "#000"

let secondaryColor = config?.theme?.secondary ?? "#ddd";
console.log(secondaryColor); // "#ddd" (default)

// In function
function getEmail(user) {
  return user?.contact?.email ?? "No email";
}

console.log(getEmail({ contact: { email: "john@example.com" } })); // "john@example.com"
console.log(getEmail({ name: "John" })); // "No email"
console.log(getEmail(null)); // "No email"

// Real API response handling
let apiResponse = {
  data: {
    user: {
      profile: {
        avatar: "https://..."
      }
    }
  }
};

// Safe extraction
let avatar = apiResponse?.data?.user?.profile?.avatar ?? "default.jpg";
console.log(avatar);

// Check and use
if (apiResponse?.data?.user) {
  console.log("User exists");
}
```

---

## 🔟 Use a Variable as a Key Using Computed Properties

**Problem**: Use variables as object property names using computed properties.

```javascript
// Basic computed property
let key = "name";
let obj = {
  [key]: "John"  // Uses value of 'key' as property name
};

console.log(obj.name); // "John"
console.log(obj["name"]); // "John"

// Dynamic key from user input
let field = "email";
let user = {
  [field]: "john@example.com"
};

console.log(user.email); // "john@example.com"

// Computed property with expression
let prefix = "user";
let config = {
  [prefix + "Name"]: "John",     // "userName"
  [prefix + "Email"]: "john@example.com" // "userEmail"
};

console.log(config.userName); // "John"
console.log(config.userEmail); // "john@example.com"

// Dynamic key creation in loop
let fields = ["name", "email", "phone"];
let formData = {};

fields.forEach(field => {
  formData[field] = null; // Creates properties: name, email, phone
});

console.log(formData);
// { name: null, email: null, phone: null }

// Using computed properties with array
let data = {
  ["item_" + 1]: "First",
  ["item_" + 2]: "Second",
  ["item_" + 3]: "Third"
};

console.log(data.item_1); // "First"

// Real example: Create object from array
let items = ["apple", "banana", "mango"];
let itemObj = {};

items.forEach((item, index) => {
  itemObj[`item_${index + 1}`] = item;
});

console.log(itemObj);
// { item_1: "apple", item_2: "banana", item_3: "mango" }

// API parameter object
function buildQuery(params) {
  const query = {};
  Object.entries(params).forEach(([key, value]) => {
    query["filter_" + key] = value;
  });
  return query;
}

let result = buildQuery({ status: "active", role: "admin" });
console.log(result);
// { filter_status: "active", filter_role: "admin" }

// Create object with computed properties and methods
let methodName = "greet";
let messageName = "greeting";

let dynamicObj = {
  [methodName]: function() {
    return this[messageName];
  },
  [messageName]: "Hello!"
};

console.log(dynamicObj.greet()); // "Hello!"

// Computed property with function result
function getKeyName(id) {
  return `user_${id}`;
}

let users = {
  [getKeyName(1)]: { name: "Alice" },
  [getKeyName(2)]: { name: "Bob" }
};

console.log(users.user_1.name); // "Alice"
console.log(users.user_2.name); // "Bob"

// Advanced: Create lookup table
let statusMap = {
  [1]: "pending",
  [2]: "active",
  [3]: "completed",
  [0]: "cancelled"
};

console.log(statusMap[1]); // "pending"
console.log(statusMap[2]); // "active"
```

---

## 📊 Quick Reference

| Operation | Syntax | Example |
|-----------|--------|---------|
| Create | `let obj = {}` | `let user = { name: "John" }` |
| Access dot | `obj.key` | `user.name` |
| Access bracket | `obj[key]` | `user["name"]` |
| Destructure | `let { x } = obj` | `let { name } = user` |
| Spread copy | `{...obj}` | `let copy = {...user}` |
| Deep copy | `JSON.parse(JSON.stringify())` | Deep copy with nesting |
| Optional chain | `obj?.key?.nested` | `user?.address?.city` |
| Computed key | `{ [key]: value }` | `{ [dynamic]: 123 }` |
| Loop keys | `Object.keys()` | `Object.keys(obj)` |
| Loop entries | `Object.entries()` | `Object.entries(obj)` |

---

**Master objects to master JavaScript data structures! 🚀**
