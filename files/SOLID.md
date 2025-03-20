# SOLID Principles in TypeScript

## Introduction
SOLID is an acronym representing five design principles for writing maintainable and scalable object-oriented software. These principles help developers build flexible, reusable, and testable code. In this article, we'll explore each principle with step-by-step TypeScript examples.

### 🎯 **Core Ideas of SOLID Principles**

---

### 1. ✅ **S - Single Responsibility Principle (SRP)**  
> **"A class should have only one reason to change."**

- **Idea:** Each class/module should have a single, well-defined responsibility.  
- **Goal:** Make code easier to maintain, test, and extend by avoiding tightly coupled functionality.

---

### 2. 📚 **O - Open/Closed Principle (OCP)**  
> **"Software entities should be open for extension, but closed for modification."**

- **Idea:** New functionality should be added by extending existing code, not modifying it.  
- **Goal:** Protect existing functionality from breaking when adding new features.

---

### 3. 🪓 **L - Liskov Substitution Principle (LSP)**  
> **"Derived classes should be substitutable for their base classes."**

- **Idea:** Subtypes must be able to replace their parent types without altering correct behavior.  
- **Goal:** Ensure that subclass instances can be used interchangeably with base class instances.

---

### 4. 🎚️ **I - Interface Segregation Principle (ISP)**  
> **"Clients should not be forced to depend on interfaces they do not use."**

- **Idea:** Split large interfaces into smaller, more specific ones.  
- **Goal:** Avoid forcing classes to implement unnecessary methods.

---

### 5. 🔗 **D - Dependency Inversion Principle (DIP)**  
> **"Depend on abstractions, not on concretions."**

- **Idea:** High-level modules should not depend on low-level modules. Both should depend on abstractions.  
- **Goal:** Reduce coupling by using abstractions to control dependencies.


## 1. Single Responsibility Principle (SRP)
*A class should have only one reason to change.*

### ❌ Violation of SRP
```typescript
class User {
  constructor(private name: string, private email: string) {}
  
  saveToDatabase() {
    console.log(`Saving ${this.name} to database...`);
  }
  
  sendEmail() {
    console.log(`Sending email to ${this.email}...`);
  }
}
```
Here, the `User` class has two responsibilities: managing user data and handling persistence.

### ✅ Following SRP
```typescript
class User {
  constructor(public name: string, public email: string) {}
}

class UserRepository {
  save(user: User) {
    console.log(`Saving ${user.name} to database...`);
  }
}

class EmailService {
  send(user: User) {
    console.log(`Sending email to ${user.email}...`);
  }
}
```
Now, each class has a single responsibility.

---

## 2. Open/Closed Principle (OCP)
*Software entities should be open for extension but closed for modification.*

### ❌ Violation of OCP
```typescript
class Rectangle {
  constructor(public width: number, public height: number) {}
}

class AreaCalculator {
  calculate(shape: any) {
    if (shape instanceof Rectangle) {
      return shape.width * shape.height;
    }
  }
}
```
Adding new shapes requires modifying `AreaCalculator`, violating OCP.

### ✅ Following OCP
```typescript
interface Shape {
  getArea(): number;
}

class Rectangle implements Shape {
  constructor(public width: number, public height: number) {}
  getArea(): number {
    return this.width * this.height;
  }
}

class Circle implements Shape {
  constructor(public radius: number) {}
  getArea(): number {
    return Math.PI * this.radius * this.radius;
  }
}

class AreaCalculator {
  calculate(shape: Shape) {
    return shape.getArea();
  }
}
```
New shapes can be added without modifying `AreaCalculator`.

---

## 3. Liskov Substitution Principle (LSP)
*Subtypes must be substitutable for their base types.*

## ✅ **Core Idea of LSP**
- A subclass should behave like its parent class.
- It should not:
  - Change the expected behavior of parent class methods.
  - Violate the contract defined by the superclass.
  - Introduce unexpected results or throw errors where the parent succeeds.

### ❌ Violation of LSP
```typescript
class Bird {
  fly() {
    console.log("Flying");
  }
}

class Penguin extends Bird {
  fly() {
    throw new Error("Penguins can't fly!");
  }
}
```
Penguin violates LSP as it changes the expected behavior of `Bird`.

### ✅ Following LSP
```typescript
interface FlyingBird {
  fly(): void;
}

interface NonFlyingBird {
  walk(): void;
}

class Sparrow implements FlyingBird {
  fly() {
    console.log("Flying");
  }
}

class Penguin implements NonFlyingBird {
  walk() {
    console.log("Walking");
  }
}
```
Now, subclasses correctly implement behaviors without violating expectations.

---

## 4. Interface Segregation Principle (ISP)
*Clients should not be forced to depend on interfaces they do not use.*

### ❌ Violation of ISP
```typescript
interface Animal {
  eat(): void;
  fly(): void;
}

class Dog implements Animal {
  eat() {
    console.log("Eating");
  }
  
  fly() {
    throw new Error("Dogs can't fly!");
  }
}
```
`Dog` is forced to implement `fly()`, which it doesn't need.

### ✅ Following ISP
```typescript
interface Eater {
  eat(): void;
}

interface Flyer {
  fly(): void;
}

class Dog implements Eater {
  eat() {
    console.log("Eating");
  }
}

class Bird implements Eater, Flyer {
  eat() {
    console.log("Eating");
  }

  fly() {
    console.log("Flying");
  }
}
```
Now, `Dog` only implements the `Eater` interface.

---

## 5. Dependency Inversion Principle (DIP)
*Depend on abstractions, not on concretions.*

### ❌ Violation of DIP
```typescript
class MySQLDatabase {
  save(data: string) {
    console.log(`Saving ${data} to MySQL database`);
  }
}

class UserService {
  db: MySQLDatabase;
  
  constructor() {
    this.db = new MySQLDatabase();
  }
  
  saveUser(data: string) {
    this.db.save(data);
  }
}
```
`UserService` is tightly coupled to `MySQLDatabase`, making it hard to switch databases.

### ✅ Following DIP
```typescript
interface Database {
  save(data: string): void;
}

class MySQLDatabase implements Database {
  save(data: string) {
    console.log(`Saving ${data} to MySQL database`);
  }
}

class UserService {
  constructor(private db: Database) {}
  
  saveUser(data: string) {
    this.db.save(data);
  }
}

const database = new MySQLDatabase();
const userService = new UserService(database);
userService.saveUser("John Doe");
```
Now, `UserService` depends on an abstraction (`Database`), making it easy to switch implementations.

---

## Conclusion
By applying SOLID principles, we create more maintainable, scalable, and testable applications. These principles help avoid tightly coupled code, making it easier to extend and modify without breaking existing functionality.

Happy coding! 🚀
