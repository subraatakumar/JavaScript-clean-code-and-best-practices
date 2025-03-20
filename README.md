
### 1. Introduction to Clean Code  
Clean code is easy to read, maintain, and debug.  
**Key principles:**  
- [**KISS (Keep It Simple, Stupid)** – Avoid unnecessary complexity.](https://github.com/subraatakumar/JavaScript-clean-code-and-best-practices/blob/main/files/KISS.md)  
- [**DRY (Don’t Repeat Yourself)** – Reuse code instead of duplicating it.](https://github.com/subraatakumar/JavaScript-clean-code-and-best-practices/blob/main/files/DRY.md)
- [**SOLID ](https://github.com/subraatakumar/JavaScript-clean-code-and-best-practices/blob/main/files/SOLID.md)
- [**YAGNI (You Ain’t Gonna Need It)** – Avoid writing code for features you don’t need yet.](https://github.com/subraatakumar/JavaScript-clean-code-and-best-practices/blob/main/files/YAGNI.md)

---

### 2. Writing Readable JavaScript Code  
✅ **Variable & Function Naming Conventions**  
- Use meaningful and descriptive names.  
- Use camelCase for variables and functions (`userName`, `fetchData`).  
- Use PascalCase for classes and constructors (`UserModel`).  
- Boolean variables should start with `is`, `has`, `can` (e.g., `isLoggedIn`).  

✅ **Code Formatting & Structure**  
- Maintain consistent indentation (2 or 4 spaces).  
- Use line breaks and spacing to improve readability.  
- Avoid long functions – break them into smaller reusable functions.  

---

### 3. Modern JavaScript Best Practices (ES6+)  
✅ **Use `let` and `const` Instead of `var`**  
```javascript
// Bad
var age = 25;
age = 30;

// Good
let age = 25;
age = 30;

// Best
const name = "John"; // Immutable
```

✅ **Use Template Literals Instead of String Concatenation**  
```javascript
// Bad
const message = "Hello, " + name + "!";

// Good
const message = `Hello, ${name}!`;
```

✅ **Use Destructuring for Cleaner Code**  
```javascript
const user = { name: "Alice", age: 30 };

// Bad
const name = user.name;
const age = user.age;

// Good
const { name, age } = user;
```

---

### 4. Writing Cleaner Functions  
✅ **Keep Functions Short & Focused**  
- A function should do one thing well.  
- Avoid functions with more than 20-30 lines.  

✅ **Limit Function Parameters**  
- Avoid too many parameters.  
- Use an object instead:  
```javascript
// Bad
function createUser(name, age, email) { ... }

// Good
function createUser({ name, age, email }) { ... }
```

✅ **Use Arrow Functions for Simplicity**  
```javascript
// Bad
function add(a, b) {
  return a + b;
}

// Good
const add = (a, b) => a + b;
```

---

### 5. Avoiding Common JavaScript Mistakes  
✅ **Use `===` Instead of `==`**  
```javascript
// Bad
if (value == 0) { ... }

// Good
if (value === 0) { ... }
```

✅ **Avoid Modifying Global Variables**  
```javascript
// Bad
let count = 0;
function increment() {
  count++;
}

// Good
function increment(count) {
  return count + 1;
}
```

✅ **Always Handle `undefined` & `null` Values**  
```javascript
// Bad
function getName(user) {
  return user.name.toUpperCase(); // Error if user is undefined
}

// Good : use optional chaining and or operator 
function getName(user) {
  return user?.name?.toUpperCase() || "Guest";
}
```

---

### 6. Asynchronous JavaScript Best Practices  
✅ **Use `async/await` Instead of `.then()`**  
```javascript
// Bad
fetchData().then(data => process(data)).catch(err => console.error(err));

// Good
async function getData() {
  try {
    const data = await fetchData();
    process(data);
  } catch (err) {
    console.error(err);
  }
}
```

✅ **Use `Promise.all()` for Parallel Execution**  
```javascript
const [user, orders] = await Promise.all([fetchUser(), fetchOrders()]);
```

---

### 7. Error Handling & Debugging  
✅ **Use `try...catch` and Meaningful Error Messages**  
```javascript
try {
  processUser(user);
} catch (error) {
  console.error("User processing failed: ", error.message);
}
```

✅ **Use `console.log()`, `console.table()`, and DevTools Effectively**  
- Use `console.table(users)` for better visualization of arrays.  
- Set breakpoints in DevTools for debugging.  

---

### 8. Performance Optimization  
✅ **Debounce & Throttle for Event Handling**  
```javascript
function debounce(func, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => func(...args), delay);
  };
}

const handleSearch = debounce(() => console.log("Searching..."), 300);
```

✅ **Lazy Loading for Performance**  
```html
<img loading="lazy" src="image.jpg" alt="Optimized Image" />
```

✅ **Use Memoization for Expensive Computations**  
```javascript
const memoizedFunction = (function () {
  const cache = {};
  return function (n) {
    if (cache[n]) return cache[n];
    console.log("Computing result...");
    cache[n] = n * n;
    return cache[n];
  };
})();
```

---

### 9. Best Practices Summary  
✅ Keep code simple & readable.  
✅ Avoid unnecessary complexity.  
✅ Follow modern JavaScript practices.  
✅ Use async/await for clean async code.  
✅ Optimize performance & debugging.  

---

### 10. Q&A + Live Coding Demo  
- Discuss common code issues.  
- Live refactoring example.  

---

