- Practice Zone

1. Declare your name and city using const , and your age using let .

const name = "Priyanshi";
const city = "Anand";
let age = 20;

2. Try this and observe

let age = 20;
age = 25;
console.log(age);
✅ Output: 25

3. Guess the output

var a = 10;
var a = 20;
console.log(a);
✅ Output: 20
✔ var allows redeclaration

4. const object modification

const obj = { name: "Riya" };
obj.age = 20;
console.log(obj);
✅ Works
Output: { name: "Riya", age: 20 }
✔ You can change contents
❌ Cannot replace whole object

5. Access let before declaration

console.log(x);
let x = 10;
❌ Error: ReferenceError
✔ Due to TDZ (Temporal Dead Zone)

6. const array change

const arr = [1, 2];
arr.push(3);
console.log(arr);
✅ Output: [1, 2, 3]
✔ Allowed (modifying contents)
❌ Not allowed: arr = [4,5]