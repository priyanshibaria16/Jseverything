- JavaScript is a programming language used to make websites interactive and lively. It was created in 1995 by Brendan Eich.

- It works along with HTML and CSS to build web pages.

- In simple words, JavaScript helps websites respond to user actions like clicking buttons, filling forms, or showing updates without reloading the page.

- Words vs Keywords
  Words vs Keywords in JavaScript (simple):

Words (Identifiers)
These are names you give in your code.
You can create them as you like.
Examples:
name, age, totalMarks

Keywords in JavaScript
These are special reserved words that already have a fixed meaning in JavaScript.
You cannot use them as names.
Examples:
var, let, const, if, else, for, while, return, function

- Variables and Declarations 

Variables are containers that hold data.
They help us store, reuse, and update information in JavaScript — from simple values like
numbers to complex data like arrays and objects.
Think of a variable as a box with a name on it. You can put something inside it (a value), and later
check or change what's inside.
In JavaScript, you create these boxes using keywords: var , let , or const

var – Old and Risky
Function scoped (not block scoped)
Can be redeclared 
Can be reassigned 
Hoisted with value undefined
var x = 10;
var x = 20; // allowed

let – Modern and Safe
Block scoped { }
Cannot be redeclared in same block
Can be reassigned
Hoisted but in TDZ (Temporal Dead Zone)
let age = 25;
age = 30; // 
let age = 40; // Error

const – Fixed Variable
Block scoped { }
Cannot be redeclared
Cannot be reassigned
Must assign value at declaration
Also has TDZ
const PI = 3.14;
PI = 3.14159; // Error

- Special Case (Important)

const protects the variable, not the data inside it:
const student = { name: "Riya" };
student.name = "Priya"; // allowed
student = {};           // not allowed

- Scope (Super Important)

Block Scope → inside { } (if, loops, etc.)
Function Scope → inside function
let & const follow block scope
var ignores block scope (causes bugs)

{
  var x = 5;
  let y = 10;
  const z = 15;
}

console.log(x); // 5
console.log(y); // Error
console.log(z); // Error

- TDZ (Temporal Dead Zone)

TDZ = Time where a variable exists but you cannot use it yet
It happens with let and const

Example:

console.log(a); // Error
let a = 10;

What happens internally:
JavaScript starts running code
It knows a will be created
But it is not initialized yet
So when you try to use it → ReferenceError
This period = TDZ

- Reassignment & Redeclaration

Reassignment
Changing the value of a variable

let x = 10;
x = 20; // reassignment

✔ Same variable
✔ New value


Redeclaration
Creating the same variable again

let x = 10;
let x = 20; // redeclaration (error)

Not allowed with let and const

With different keywords

var
var a = 10;
var a = 20; // redeclaration allowed
a = 30;     // reassignment allowed

let
let b = 10;
let b = 20; // redeclaration not allowed
b = 30;     // reassignment allowed

const
const c = 10;
const c = 20; // redeclaration not allowed
c = 30;       // reassignment not allowed

- Hoisting

Hoisting is when JavaScript moves variable declarations to the top of their scope before execution.

Two Parts of Hoisting
1️. Declaration goes to the top
JavaScript takes the variable declaration and places it at the top(Initialization)

2️. Initialization stays in the same place
The value assignment does NOT move(Declaration)

Example
console.log(a);
var a = 10;

JavaScript treats it like:

var a;          // declaration moved to top
console.log(a); // undefined
a = 10;         // initialization stays here

| Type    | Hoisted | Initial Value   | Use Before Declaration |
| ------- | ------- | --------------- | ---------------------- |
| `var`   | Yes   | `undefined`     | Allowed              |
| `let`   | Yes   | Not set (TDZ) |  Error                |
| `const` | Yes   | Not set (TDZ) |  Error                |

var → hoist + undefined
let → hoist + wait (TDZ)
const → hoist + strict wait (TDZ)

- Common Confusions in JavaScript

1. const is NOT fully constant

It protects the variable, not the value inside it

const obj = { name: "Riya" };
obj.name = "Priya"; // ✅ allowed
obj = {};           // ❌ not allowed

2. var is outdated

It can cause bugs, so avoid it
Prefer let and const

3. Scope Confusion
{
  var x = 5;
  let y = 10;
  const z = 15;
}
console.log(x); // ✅ 5
console.log(y); // ❌ Error
console.log(z); // ❌ Error

var → works outside block
let, const → only inside block { }

4. Hoisting Confusion
With var
console.log(a); // ✅ undefined
var a = 10;
No error, just undefined

With let
console.log(b); // ❌ Error
let b = 20;
Error due to TDZ

5. let vs const

Both are similar:
Block scoped
Hoisted with TDZ

Difference:
let → value can change
const → value cannot be reassigned
