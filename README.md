### 🌱 Array Methods — *To Do Practice to Become Better* 😇 ✨
###### 📅 06-10 -2026 
---
## 🔹Array.isArray()

> **Array hai ya nahi check karta hai.**

📌 `Array.isArray(value)` → **Kya value Array hai?**

- `value` → check hone wali value
-  Return → **Always Boolean** `true` / `false`

```js
Array.isArray([1, 2, 3]) // true
Array.isArray([])        // true
Array.isArray(new Array()) // true

Array.isArray(123)       // false
Array.isArray(true)      // false
Array.isArray(false)     // false

Array.isArray("hello")   // false

// {} outer value Object → false
Array.isArray({})        // false

const result = { name: "Chandan" };
Array.isArray(result); // false

Array.isArray(null);       // false
Array.isArray(undefined);  // false

Array.isArray(NaN)       // false
Array.isArray(Infinity)  // false

// important special cases
Array.isArray(() => {})    // false
Array.isArray(/abc/)       // false
Array.isArray(new Date())  // false
```

### 🧩 Nested Values

> 📌 **`Array.isArray()` sirf di gayi value ka outer type check karta hai.**
> Array ke andar `object`, `array` ya koi aur value ho, result **outer value** ke according aata hai.

```js

// 🛠️ Note:- Array containing an object

// [] outer value Array → true
Array.isArray([{}])      // true

Array.isArray([[], [], []]) // true
Array.isArray([{}, {}, {}]) // true

// Invalid syntax
Array.isArray({[]})  // SyntaxError ❌

// Invalid syntax
Array.isArray({[{}]}) // SyntaxError ❌

// Object containing an array
Array.isArray({ data: [] })  // false
Array.isArray({ data: [{}, {}] }) // false

// Array containing an array
// [] outer value Array → true
Array.isArray([[]])          // true

// Object containing an object
Array.isArray({ data: {} })  // false

Array.isArray({ data: [[],[],[]] }) // false

// Array containing an object containing an array
Array.isArray([{ data: [] }]) // true

// Deeply nested Array
Array.isArray([{a:{b:{c:[]}}}]) // true

// Deeply nested Object
Array.isArray({data:{x:{y:[]}}}) // false
```
📌 **Note:** `Array.isArray()` ka **purpose** kisi **value** ko reliably **Array hai ya nahi check karna** hai, kyunki `typeof` Array ke liye `"object"` return karta hai.

```js
typeof [1, 2, 3] // "object"
typeof {}        // "object"
```

- `typeof` Array ke liye `"object"` return karta hai:
  **`typeof [1, 2, 3]` → `"object"`**
### 🔹Syntax Breakdown

- **`Array`** → JavaScript ka built-in **Array object**
- **`isArray`** → `Array` ka **static method**
- **`data`** → Jis **value ko check** karna hai

> 🛠️ **`Array.isArray` fixed hai** → Name aur **case exactly same** hona chahiye **tabhi method** kaam karega.

```js
 const data = [10, 20, 30];
 
 Array.isArray(data); // true
```

> 📌 `Array.isArray(variable)` → **variable mein Array hona chahiye**, tabhi `true`, warna `false`.

### 🧩 Object ke andar Array Check

> 📌 Object ki kisi **property ke andar Array hai ya nahi** check karne ke liye bhi `Array.isArray()` use kar sakte hain.

```js
function checkUserData(data) {
  if (!Array.isArray(data.likes)) {
    console.log("❌ Rejected: 'likes' must be an Array.");
    return;
  }

  console.log("✅ Accepted: 'likes' is an Array.");
}
```
### 🛠️ Example

```js
checkUserData({
  username: "Chandan",
  likes: ["Music", "Coding", "Chess"]
});
// ✅ Accepted: 'likes' is an Array.

checkUserData({
  username: "Chandan",
  likes: "Music"
});
// ❌ Rejected: 'likes' must be an Array.

checkUserData({
  username: "Chandan",
  likes: 100
});
// ❌ Rejected: 'likes' must be an Array.
```
### 🔎 Main Point

```js
Array.isArray(data.likes)
```

- `data` → **Object**
- `likes` → Object ki **property**
- `data.likes` → Property ki **value**
- `Array.isArray(data.likes)` → Check karta hai ki value **Array hai ya nahi**

**Array → `true` → Accepted ✅**  
**Array nahi → `false` → Rejected ❌**

> 📌 **Object ke andar ki value check:**  
> `Array.isArray(object.property)` → `true` / `false

### 🧩 Array → Multiple Objects → Object ke andar Array

> 📌 Real-world data mein aksar **Array ke andar multiple Objects** hote hain, aur Object ki kisi property mein **Array** ho sakta hai.

```js
const usersData = [
  { id: 1, name: "Chandan", likes: ["Music", "Coding"] },
  { id: 2, name: "Sonu", likes: "Gaming" },
  { id: 3, name: "Amit" }
];

for (const user of usersData) {
  // likes Array hai ya nahi
  if (!Array.isArray(user.likes)) {
    console.log(`❌ ${user.name} → Invalid likes`);
    continue;
  }

  console.log(`✅ ${user.name} → Valid likes`);

  user.likes.forEach(like => {
    console.log(`  - ${like}`);
  });
}
````
### 📤 Output

```text
✅ Chandan → Valid likes
  - Music
  - Coding

❌ Sonu → Invalid likes

❌ Amit → Invalid likes
```
### 🔎 Main Point

- `usersData` → **Array**
- `user` → Array ka **ek Object**
- `user.likes` → Object ke andar ki **value**
- `Array.isArray(user.likes)` → Check करता है ki `likes` **Array hai ya nahi**
- Invalid data → `continue` → **next user par chala jata hai**

> 📌 **Pattern:**  
> `Array → Object → Property → Array`

> `Array.isArray(user.likes)` → **Object ke andar Array check**

💡 `typeof []` → `"object"` → **Array check ke liye `Array.isArray()` use karo**.

```js
if (Array.isArray(value)) {
  // Array
}
```

# 🔹map() 

> **Har element ko process karke ek `New Array` create karta hai.**

📌 **Transform Data** → Har `element` ko **transform** karke **new data** banata hai.

- `map()` **filter ki tarah sirf matching data return nahi karta** → Ye har element ko process karke **new value create** karta hai.

🔁 **Return always:** Har **element** ki `true` / `false` **dono values** `New Array` mein add hoti hain.

- 📏 **Length:** `Original Array.length === New Array.length`→ **Dono equal hote hain.**
### 📌 Return Value

```js
users.map(user => user.age > 30);

// [true, false, true]
```

> `true` / `false` → Dono return hote hain.

🛠️ `Match` aur `non-match` **dono ka result** New Array mein aata hai.
### 📌 Example

```js
const users = [
  { name: "A", age: 35 },
  { name: "B", age: 20 },
  { name: "C", age: 40 }
];

const result = users.map(user => user.age > 30);

// [true, false, true]
````

> `true` → condition match  
> `false` → condition match nahi

##### 🛠️ `map()`  → Match + Non-Match

```js
const users = [
  { name: "A", age: 35 },
  { name: "B", age: 20 },
  { name: "C", age: 40 }
];

const result = users.map(user => {
  if (user.age > 30) {
    return user;
  }

  return user;
});

// true → A(35), C(40) | false → B(20)

// New Array → 3
console.log(result);
// [
//   { name: "A", age: 35 },
//   { name: "B", age: 20 },
//   { name: "C", age: 40 }
// ]
```

- **Match** → `All` data
- **Non-Match** → `All` data
- **Original `3`** → **New Array `3`**
### 🔹 Apne According Data Create

```js
const result = users.map(user => {
  if (user.age > 30) {
    return user.name; // ya return false
  }

  return null;
});

// return user.name → ["A", null, "C"]
// return false → [false, null, false]
```

 > **Kisi bhi type ka data** → `map()` mein use kar sakte hain.
 
**Return:** `number` | `boolean` | `string` | `object` | `null` | `undefined` | etc.
### ⚡ `map()` vs `filter()`

- **`map()`** → Sabhi elements process → **New data create**
- **`filter()`** → Condition match → **Sirf matching elements return**

> 📌 Agar **sirf matching/single type ka data** chahiye, to `filter()` use karo.  
> `map()` ke saath `filter()` bhi chain kar sakte ho.

```js
users
  .filter(user => user.age > 30)
  .map(user => user.name);

// ["A", "C"]
```

```js
const users = [
  { name: "A", age: 35 },
  { name: "B", age: 20 },
  { name: "C", age: 40 },
  { name: "D", age: 25 },
  { name: "E", age: 50 }
];

const result = users
  .map(user => {
    if (user.age > 30) {
      return user.name;
    }

    return null;
  })
  .filter(value => value !== null);

// ["A", "C", "E"]
```

- `map()` → Match → `user.name`
- `map()` → Not Match → `null`
- `filter()` → `null` remove
- Final → Sirf matching data

> 📌 `map()` **data transform** karta hai → `filter()` **unwanted data remove** karta hai.
### 🔹 `map()` ke Advantages

- **Data Transform** → Har element ko apne according `new value` mein badal sakte hain.
- **Pura Data Available** → `matching` aur `non-matching` dono ka result milta hai.
- **New Array** → **`map()`** Array ke **har ek element ko transform** karke uska **result ek Naye Array** mein deta hai — 

> **1:1 Mapping** → Har element se **1 result**, bina **Original Array** ko modify kiye hota hai.
### 📝 Limitations

- `map()` mein **`break` / `continue`** se process ko **beech mein stop** ya element ko **skip** nahi kar sakte.
- Ek baar start hone ke baad **callback sabhi elements par chalega**.
- `map()` mein **short-circuit** karke loop ko beech mein stop nahi kar sakte.

> 💡 **Core Flow:** `map()` → **Every element process → Transform → Return → New Array**

### ⚡ Short-Circuit

> 📌 **Short-circuit** → Process ko condition/result milte hi **beech mein rok dena**.

📌 **Common ways:** `return` | `break` | `throw` | `process.exit()`

- `return` → **Function** ko stop karta hai.
- `break` → **Loop / `switch`** ko stop karta hai.
- `throw` → **Error** throw karke **current execution** ko stop karta hai.
- `process.exit()` → **Node.js process** ko stop karta hai.

> 📌 **Use:** Jab aage ka **code execute** nahi karna ho.

> 📝 **Kyon?** Beech mein **`validation / condition`** check karke **invalid** ya **unwanted data** ko aage **`process`** hone se rokne ke liye.

- **Invalid data** ko **`database`** mein save hone se rok sakte hain.
- **Unwanted result** aane par aage ka **`process`** stop kar sakte hain.
### 🛠️ Core Points

- **Har element par `1` baar chalta hai** → Koi element skip nahi hota.
- **Original Array ko modify nahi karta** → `New Array` create karta hai.
- **Callback se kisi bhi type ki value return** kar sakte hain → `string`, `number`, `boolean`, `object`, ya **original value**
- **Callback ka `return`** → New Array mein **usi position par** aata hai.
- **New Array ki `length`** → **Original Array** ke elements ke **barabar** hoti hai.

---
### 📌 `true` / `false` bhi return kar sakta hai

```js

const result = users.map(user => user.age > 30);

// [true, false, true, false]
```

> Condition ka result bhi **New Array ka data** ban jata hai.

---
### 🔥 Condition ke saath

```js
const result = users.map(user => {
  if (user.age > 30) {
    return user;
  }

  return false;
});
```

- **Condition `true`** → `user` return
- **Condition `false`** → `false` return

> `map()` condition fail hone wale elements ko **remove nahi karta**.
### 📦 Example

```js
const numbers = [10, 20, 30, 40];

const result = numbers.map(num => num * 2);

// [20, 40, 60, 80]
```

> Original Array same rahta hai:

```js
// Original
[10, 20, 30, 40]

// New Array
[20, 40, 60, 80]
```

---
### 📏 Length Rule

> **New Array ki length = Original Array ki length**

```js
const numbers = [10, 20, 30, 40];

const result = numbers.map(num => num * 2);

numbers.length; // 4
result.length;  // 4
```

> `map()` **jitne elements process karta hai, utne hi elements ka New Array deta hai.**
### 🛠️ Working 

```text
Original Array
      ↓
    map()
      ↓
Har element process
      ↓
Callback ka return
      ↓
   New Array
```

###### 📅 07-10 -2026 
---
# 🔹 filter() 🔍

> 📌 `filter()` → **Condition check** karke matching elements se **New Array** banata hai.

🎯 `filter()` → **Multiple items select** kar sakta hai → jo condition **pass** kare, unhe `New Array` mein rakhta hai.

- 📌 `filter()` → **Condition `true`** hone par  **Original value** ko `New Array` mein add karta hai, khud **new value create** nahi karta.

>⚙️ **Condition required:** `filter()` mein **condition/check** hona chahiye → `true` = **Keep**, `false` = **Skip**.

💡 **Without condition:** Direct **truthy/falsy value** return karne par bhi `filter()` uske basis par element ko **Keep/Skip** karega.

🔁 **Return always:** `true` → **Original value** `New Array` mein | `false` / `falsy` → **Skip**

- 📭 **No Match:** Agar **koi bhi element** condition pass nahi karta → `New Array` **empty `[]`** return hota hai.
### 🛠️ Syntax

```js
const result = arr.filter(item => condition);
````
### ⚡ Short-Circuit

> 📌 `filter()` **short-circuit nahi kar sakta** → condition match hone ke baad bhi baaki elements process hote hain.

- `return true` → Current element **New Array** mein add
- `return false` / `falsy` → Current element **Skip**
- Lekin `filter()` ko beech mein **stop** karne ke liye `break` / `return` directly use nahi kar sakte.

> 💡 **Kyon?** Kabhi-kabhi result milte hi **poora process stop** karna hota hai, taaki **unnecessary** elements process na hon.

📌 **Short-circuit ke common ways:**
`break` | `return` | `throw`

📌 **Short-circuit wale Array methods:**
`some()` | `every()` | `find()` | `findIndex()` | `findLast()` | `findLastIndex()`

> ⚙️ **Actual loop** (`for`, `for...of`) mein `break` / `return` se **process ko beech** mein **stop** kar sakte hain.

### 🔄 `map()` + `filter()` → Transform + Remove

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 },
  { name: "D", age: 15 },
  { name: "E", age: 40 }
];

const mappedData = users.map(user => {
  if (user.age > 20) {
    return user.name;
  }

  return null;
});

console.log(mappedData);
// ["A", null, "C", null, "E"]

const result = mappedData.filter(value => value !== null);

console.log(result);
// ["A", "C", "E"]
```
### 📌 Main Point

- `map()` → **New Array create** karta hai → `["A", null, "C", null, "E"]`
- `filter()` → `null` ko **remove** karta hai → `["A", "C", "E"]`

> 💡 `map()` → **Transform** | `filter()` → **Remove unwanted values**

### 🔍 `filter()` → `true` / `false` & `!==`

> 📌 `filter()` mein callback ka **truthy result → element keep** aur **falsy result → element skip** hota hai.

### 1️⃣ `return true / false`

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 }
];

const result = users.filter(user => {
  if (user.age > 20) {
    return true;   // ✅ Keep
  }

  return false;    // ❌ Skip
});

console.log(result);
// A(25), C(30)
````

> 📌 Yahan `return false` **element ko skip** karne ka signal deta hai.

### 2️⃣ `return false` na likhne par

```js
const result = users.filter(user => {
  if (user.age > 20) {
    return true;
  }
});
```

> 📌 `age > 20` false hone par callback **kuch return nahi karta**, isliye `undefined` milta hai → **falsy** → element skip.

➡️ Isliye dono ka result **same** hai.

### 3️⃣ `!==` ka direct use

```js
const result = users.filter(user => user.age !== 18);

console.log(result);
// A(25), C(30)
```

> 📌 `user.age !== 18` khud **true / false** return karta hai:
> 
> `25 !== 18` → `true` → Keep ✅  
> `18 !== 18` → `false` → Skip ❌  
> `30 !== 18` → `true` → Keep ✅

### 💡 Main Difference

- `return false` → **Explicitly** skip karne ka signal.
- `return` na ho → `undefined` → **Falsy** → automatically skip.
- `!==` → Condition khud **boolean (`true/false`)** return karti hai.

> 📌 **Rule:** `filter()` ko final result mein **truthy → Keep** aur **falsy → Skip** chahiye.

### 📌 `return true` / `return false` ka Difference

- **Dono likhne par** → code explicitly batata hai:
  `true` → **Keep** ✅ | `false` → **Skip** ❌  
  ➜ Koi conflict nahi, bas code thoda **zyada** ho jata hai.

- **`return false` na likhne par** → condition false hone par `undefined` return hota hai → **Falsy** → element skip.  
  ➜ `filter()` mein **koi problem/conflict nahi** hota.

### ⚡ Most Efficient

```js
users.filter(user => user.age > 20);
```

> 📌 **Direct condition return** sabse simple aur efficient hai, kyunki condition khud hi `true / false` deti hai.

```js
// Unnecessary
users.filter(user => {
  if (user.age > 20) {
    return true;
  }

  return false;
});
```

> 💡 **Rule:** `filter()` mein `true` = **Keep**, `false` / `undefined` = **Skip**.

### 🔎 Core Points

- **Original Array ko modify nahi karta**.
- **New Array** create karta hai.
- Callback ka **`return`** `true` / `false` decide karta hai:
    - `true` → **Original element** New Array mein add
    - `false` / `null` / `undefined` → **Element skip**
- `filter()` **return value ko add nahi karta**, balki **original element** ko add karta hai.
- New Array mein **sirf matching elements** aate hain.
- New Array ki length **Original Array se equal ya kam** hoti hai.

### 🛠️  Example

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 }
];

const result = users.filter(user => {
  if (user.age > 20) {
    return true;
  }

  return false;
});

console.log(result);
```

```text
📤 Output:
[
  { name: "A", age: 25 },
  { name: "C", age: 30 }
]
```

> 📌 Yahan `return true` **A aur C ke original objects** ko New Array mein add karta hai.

### 🔄 `return true` vs `return data`

```js
arr.filter(user => {
  if (user.age > 20) {
    return true;
  }
});
```

```js
arr.filter(user => {
  if (user.age > 20) {
    return user;
  }
});
```

> ✅ Dono mein **same original `user`** New Array mein aayega, kyunki object `truthy` hai.

### ❌ `return null`

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 }
];

const result = users.filter(user => {
  if (user.age > 20) {
    return null;
  }
});

console.log(result);
// []
```

> `Falsy value` → **element skip** ho jayega → New Array mein **kuchh nahi aayega**.

> 📌 **Rule:  Falsy Return = Element Skip**

- **Agar `return null` likha:** `null` (falsy) hai → isliye element **skip**.

 - **Agar `if` condition false hui:** Toh default `undefined` (falsy) return hota hai → isliye element **skip**.

➡️ Isliye **koi bhi element New Array mein nahi aaya**.
### 🎯 Non-Matching Data Chahiye

Condition ko **ulta** kar do:

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 }
];

const result = users.filter(user => user.age <= 20);

console.log(result);
// [{ name: "B", age: 18 }]
```

> 📌 **`filter()` mein return value output nahi banti.**  
> `return` sirf decide karta hai → **element New Array mein aaye ya skip ho.**

### 🔄 `!` Not Operator ke saath `filter()`

> 📌 Agar humein **condition ka opposite data** chahiye, to condition ke aage **`!` (Not Operator)** laga sakte hain.

```js
const users = [
  { name: "A", age: 25 },
  { name: "B", age: 18 },
  { name: "C", age: 30 },
  { name: "D", age: 15 },
  { name: "E", age: 40 }
];

// Implicit Return
const result = users.filter(user => !(user.age > 20));

// Explicit Return
const result = users.filter(user => {
  return !(user.age > 20);
});

console.log(result);
// [
//   { name: "B", age: 18 },
//   { name: "D", age: 15 }
// ]
```
### ⚠️ `!user.age > 20`

```js
const result = users.filter(user => !user.age > 20);
````

> 📌 **Error nahi aayega**, lekin result **galat condition** par based hoga.

```js
!user.age > 20
// roughly → (!user.age) > 20
```

❌ `age > 20` ka opposite nahi hai.

✅ Sahi:

```js
!(user.age > 20)

// ── ya ──

user.age <= 20
```

> 📌 **Rule:** `!` ko **poori condition** par lagao.

### 🚫 `!==` ke saath `filter()`

> 📌 `!==` → **Not Equal** check karta hai.  
> `filter()` mein iska use karke **specific value ko hata** sakte hain aur baaki elements rakh sakte hain.

```js
const users = [
  { name: "Chandan", role: "user" },
  { name: "Sonu", role: "admin" },
  { name: "Amit", role: "user" },
  { name: "Rahul", role: "editor" }
];

const result = users.filter(user => user.role !== "admin");

console.log(result);
````

📤 **Output:**

```js
[
  { name: "Chandan", role: "user" },
  { name: "Amit", role: "user" },
  { name: "Rahul", role: "editor" }
]
```

> 📌 **`role !== "admin"`** → Jo user **admin nahi hai**, wahi New Array mein aayega.

### 💡 Mostly Use

- **Specific role** ko exclude karna
- **Specific status** ko remove karna
- **Specific category** ko exclude karna
- **Specific value** ko hata kar baaki data lena

> 🔎 **Rule:** `filter()` + `!==` → **Jis value se match karega, woh skip; baaki data milega.**

### ⚡ `map()` vs `filter()`

- `map()` → **Return value** New Array mein aati hai.
- `filter()` → **Original element** New Array mein aata hai, agar `return` truthy ho.

> 💡 **Core Flow:**  
> `filter()` → **Condition Check → true = Keep → false = Skip → New Array**

###### 📅 08-10 -2026 
---
