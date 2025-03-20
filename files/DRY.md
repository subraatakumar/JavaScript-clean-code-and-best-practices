# DRY Principle in Software Development

## What is DRY Principle?

The **DRY (Don't Repeat Yourself)** principle is a fundamental concept in software development that aims to reduce code duplication by ensuring that every piece of knowledge in a system has a **single, unambiguous representation**. 

By following the DRY principle, developers can:
- Improve code **maintainability**
- Reduce **redundancy** and **bugs**
- Enhance **scalability** and **efficiency**

## Live Coding Examples

### Example 1: Without DRY Principle (Code Duplication)

```javascript
// Function to calculate the area of a rectangle
function rectangleArea(length, width) {
    return length * width;
}

// Function to calculate the area of a square (code duplication)
function squareArea(side) {
    return side * side;
}

console.log(rectangleArea(10, 5)); // Output: 50
console.log(squareArea(4)); // Output: 16
```

In the above example, the `squareArea` function duplicates the logic of `rectangleArea`, which violates the DRY principle.

### Example 2: Applying DRY Principle (Refactored Code)

```javascript
// Single function to calculate area
function calculateArea(length, width = length) {
    return length * width;
}

console.log(calculateArea(10, 5)); // Rectangle Area: 50
console.log(calculateArea(4)); // Square Area: 16
```

By using **default parameters**, we eliminate code duplication and achieve a more reusable function.

### Example 3: DRY in React Components

#### Without DRY (Duplicate Button Components)

```jsx
const PrimaryButton = () => {
    return <button style={{ backgroundColor: 'blue', color: 'white' }}>Primary</button>;
};

const SecondaryButton = () => {
    return <button style={{ backgroundColor: 'gray', color: 'white' }}>Secondary</button>;
};
```

Here, the button components are **redundant** since they share similar logic with minor variations.

#### With DRY (Reusable Button Component)

```jsx
const Button = ({ label, bgColor }) => {
    return <button style={{ backgroundColor: bgColor, color: 'white' }}>{label}</button>;
};

const App = () => (
    <>
        <Button label="Primary" bgColor="blue" />
        <Button label="Secondary" bgColor="gray" />
    </>
);
```

This approach ensures **reusability** and avoids code repetition.

## Conclusion

The DRY principle is crucial for writing **clean**, **maintainable**, and **efficient** code. By identifying repeated logic and refactoring it into **reusable** functions, components, or modules, developers can enhance their code quality and scalability.

---

**Follow the DRY principle and write better code!** 🚀

Here are some **complex DRY principle examples using pure Vanilla JavaScript (no frameworks or libraries like React or jQuery):**

---

### 1. ⚡️ **Dynamic Form Generation and Validation**

**Problem:**  
You have multiple forms with similar fields and validations that need to be created dynamically.

**Solution:**
Use a **dynamic form generator** with a reusable validation system.

```javascript
// formGenerator.js
const validationRules = {
  text: (value, label) => (value.trim() ? "" : `${label} is required.`),
  email: (value, label) =>
    /\S+@\S+\.\S+/.test(value) ? "" : `${label} must be a valid email.`,
  password: (value, label) =>
    value.length >= 8 ? "" : `${label} must be at least 8 characters.`,
};

const createForm = (formId, fields) => {
  const form = document.createElement("form");
  form.id = formId;

  fields.forEach(({ name, label, type }) => {
    const inputLabel = document.createElement("label");
    inputLabel.innerText = label;
    const input = document.createElement("input");
    input.type = type;
    input.name = name;
    form.appendChild(inputLabel);
    form.appendChild(input);
    form.appendChild(document.createElement("br"));
  });

  const submitBtn = document.createElement("button");
  submitBtn.innerText = "Submit";
  submitBtn.type = "submit";
  form.appendChild(submitBtn);

  document.body.appendChild(form);

  form.addEventListener("submit", (event) => {
    event.preventDefault();
    handleFormSubmission(form, fields);
  });
};

const handleFormSubmission = (form, fields) => {
  let isValid = true;
  fields.forEach(({ name, label, type }) => {
    const value = form[name].value;
    const errorMsg = validationRules[type](value, label);
    if (errorMsg) {
      alert(errorMsg);
      isValid = false;
    }
  });

  if (isValid) {
    alert("Form submitted successfully!");
  }
};
```

✅ **Usage:**

```javascript
const userFormConfig = [
  { name: "username", label: "Username", type: "text" },
  { name: "email", label: "Email", type: "email" },
  { name: "password", label: "Password", type: "password" },
];

createForm("userForm", userFormConfig);
```

👉 **Why it’s DRY:**  
- Eliminates repetitive form creation logic.
- Centralizes validation with reusable rules.

---

### 2. 🔥 **Higher-Order Function for API Calls with Error Handling**

**Problem:**  
Multiple API calls are made with duplicate error-handling logic.

**Solution:**
Use a **higher-order function** to centralize and reuse error-handling.

```javascript
// apiHandler.js
const withErrorHandling = (fn) => async (...args) => {
  try {
    const result = await fn(...args);
    return result;
  } catch (error) {
    console.error("API Error:", error.message);
    return { error: "Something went wrong. Please try again." };
  }
};

const fetchData = async (url) => {
  const response = await fetch(url);
  if (!response.ok) throw new Error(`Failed to fetch from ${url}`);
  return response.json();
};

const postData = async (url, data) => {
  const response = await fetch(url, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });
  if (!response.ok) throw new Error(`Failed to post to ${url}`);
  return response.json();
};

// Wrap the functions with error handling
const safeFetchData = withErrorHandling(fetchData);
const safePostData = withErrorHandling(postData);
```

✅ **Usage:**

```javascript
// Fetch data
safeFetchData("https://jsonplaceholder.typicode.com/posts/1").then((data) =>
  console.log(data)
);

// Post data
safePostData("https://jsonplaceholder.typicode.com/posts", {
  title: "New Post",
  body: "This is a new post.",
}).then((data) => console.log(data));
```

👉 **Why it’s DRY:**  
- Avoids duplicating `try-catch` logic for multiple API calls.
- Centralizes error-handling logic.

---

### 3. 📚 **Factory Pattern for Creating Different Types of Objects**

**Problem:**  
You need to create different types of objects with similar methods, but with different logic or properties.

**Solution:**
Use a **factory pattern** to generate objects dynamically.

```javascript
// shapeFactory.js
const shapeFactory = (type, dimensions) => {
  const shapes = {
    circle: {
      type: "circle",
      radius: dimensions.radius,
      area: () => Math.PI * Math.pow(dimensions.radius, 2),
    },
    rectangle: {
      type: "rectangle",
      width: dimensions.width,
      height: dimensions.height,
      area: () => dimensions.width * dimensions.height,
    },
    square: {
      type: "square",
      side: dimensions.side,
      area: () => Math.pow(dimensions.side, 2),
    },
  };

  return shapes[type] || null;
};
```

✅ **Usage:**

```javascript
const circle = shapeFactory("circle", { radius: 5 });
console.log(`Circle Area: ${circle.area()}`);

const rectangle = shapeFactory("rectangle", { width: 10, height: 5 });
console.log(`Rectangle Area: ${rectangle.area()}`);

const square = shapeFactory("square", { side: 4 });
console.log(`Square Area: ${square.area()}`);
```

👉 **Why it’s DRY:**  
- Removes duplicated object creation logic.
- Centralizes object creation in a single function.

---

### 4. 🔄 **Debounce and Throttle for Optimized Event Handling**

**Problem:**  
You have multiple event listeners (like `scroll` or `input`) that fire too frequently, leading to performance issues.

**Solution:**
Create reusable **debounce** and **throttle** functions to limit how often a function is called.

```javascript
// debounceThrottle.js
const debounce = (fn, delay) => {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
};

const throttle = (fn, limit) => {
  let lastCall = 0;
  return function (...args) {
    const now = Date.now();
    if (now - lastCall >= limit) {
      lastCall = now;
      fn.apply(this, args);
    }
  };
};
```

✅ **Usage:**

```javascript
const logResize = () => console.log("Window resized!");
const logScroll = () => console.log("User scrolled!");

// Debounce resize to prevent excessive calls
window.addEventListener("resize", debounce(logResize, 300));

// Throttle scroll to limit event calls
window.addEventListener("scroll", throttle(logScroll, 500));
```

👉 **Why it’s DRY:**  
- Prevents repeating logic for throttling and debouncing events.
- Increases performance and reduces unnecessary calls.

---

### 5. 📢 **Event Emitter for Pub/Sub Pattern**

**Problem:**  
You need to notify multiple parts of your application when an event occurs, but you’re duplicating event-handling logic.

**Solution:**
Create a reusable **Event Emitter (Pub/Sub)** pattern to manage events.

```javascript
// eventEmitter.js
class EventEmitter {
  constructor() {
    this.events = {};
  }

  on(event, listener) {
    if (!this.events[event]) this.events[event] = [];
    this.events[event].push(listener);
  }

  off(event, listenerToRemove) {
    if (!this.events[event]) return;
    this.events[event] = this.events[event].filter(
      (listener) => listener !== listenerToRemove
    );
  }

  emit(event, data) {
    if (!this.events[event]) return;
    this.events[event].forEach((listener) => listener(data));
  }
}

// Create an instance
const eventBus = new EventEmitter();
```

✅ **Usage:**

```javascript
const onUserCreated = (user) => console.log("User created:", user.name);
const onUserDeleted = (user) => console.log("User deleted:", user.name);

// Subscribe to events
eventBus.on("USER_CREATED", onUserCreated);
eventBus.on("USER_DELETED", onUserDeleted);

// Emit events
eventBus.emit("USER_CREATED", { name: "John Doe" });
eventBus.emit("USER_DELETED", { name: "Alice Smith" });

// Unsubscribe from events
eventBus.off("USER_DELETED", onUserDeleted);
```

👉 **Why it’s DRY:**  
- Centralizes event handling logic.
- Allows multiple subscribers to listen to the same events without tight coupling.

---

## 🎯 **Summary**

These complex vanilla JavaScript examples demonstrate how to apply the **DRY principle** effectively by:

✅ Abstracting repetitive logic.  
✅ Reusing higher-order functions, factories, and event handlers.  
✅ Improving maintainability and scalability of the codebase.

Which of these patterns would you like to implement in your next project? 🚀

