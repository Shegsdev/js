# JavaScript Classes and Object-Oriented Programming (OOP)

## Table of Contents

1. [Introduction to Classes](#introduction-to-classes)
   - What is a Class?
   - Creating Classes
2. [Object-Oriented Programming (OOP) Concept](#object-oriented-programming-oop-concept)
   - Entity-Relationship Diagram (ERD)
   - Key OOP Concepts
     - Encapsulation
     - Inheritance
     - Polymorphism
     - Abstraction
3. [Private Properties](#private-properties)
   - Syntax and Use Cases
4. [Overriding Derived Properties](#overriding-derived-properties)
   - Example Use Cases
5. [Getters and Setters](#getters-and-setters)
   - Definition and Example
6. [Static Methods](#static-methods)
   - Definition and Example
7. [Use Case Example](#use-case-example)
8. [Building a Small Real-World Project](#building-a-small-real-world-project)
   - Project Overview
   - Building the Classes
   - Final Integration
9. [Best Practices for OOP in JavaScript](#best-practices-for-oop-in-javascript)

---

## Introduction to Classes

### What is a Class?

A **class** in JavaScript is a blueprint for creating objects with shared properties and methods. It serves as a template for creating instances of the object, encapsulating both data and behavior into a single entity. Classes provide a more structured way to organize code compared to using traditional function constructors.

In JavaScript, classes were introduced in **ECMAScript 6 (ES6)** as syntactic sugar over the existing prototype-based inheritance system.

### Creating Classes

A class is defined using the `class` keyword, followed by the name of the class, and contains a constructor and methods. The `constructor()` method is called when a new instance of the class is created.

#### Example:
```javascript
class Animal {
  constructor(name, species) {
    this.name = name;
    this.species = species;
  }

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

const dog = new Animal('Buddy', 'Dog');
dog.speak();  // Output: Buddy makes a sound.
```

---

## Object-Oriented Programming (OOP) Concept

**Object-Oriented Programming (OOP)** is a programming paradigm that organizes software design around data, or **objects**, rather than functions and logic. The goal of OOP is to model real-world entities and interactions in software.

### Entity-Relationship Diagram (ERD)

An **Entity-Relationship Diagram (ERD)** helps visualize the relationships between different entities in a system. In the context of OOP, we can consider **classes** as entities, and **instances of classes** as objects.

#### Example ERD for OOP in JavaScript:

```plaintext
  +-------------------+
  |    Person         |<------------------+
  +-------------------+                   |
  | - name            |                   |
  | - age             |                   |
  | + greet()         |                   |
  +-------------------+                   |
            |                             |
            | extends                    |
            |                             |
  +-------------------+                   |
  |    Employee       |                   |
  +-------------------+                   |
  | - position        |                   |
  | + getDetails()    |                   |
  +-------------------+                   |
```

- **Person** is a base class with attributes like `name` and `age`, and a method `greet()`.
- **Employee** is a derived class that inherits from `Person` and adds a new property `position` and method `getDetails()`.

This represents **inheritance** and **encapsulation**, key pillars of OOP.

### Key OOP Concepts

1. **Encapsulation**: Bundling data (properties) and methods that operate on the data into a single unit (class), restricting access to some of the object's components. This hides the internal state and only exposes necessary methods.
2. **Inheritance**: A class can inherit properties and methods from another class, enabling reuse of code.
3. **Polymorphism**: A method in the base class can be overridden in the derived class, allowing for different implementations.
4. **Abstraction**: Hiding the complex reality and showing only the essential features of an object.

---

## Private Properties

Private properties are variables within a class that cannot be accessed or modified directly from outside the class. In JavaScript, private properties were introduced using **WeakMaps** in earlier versions and, in ES2022, through the `#` syntax.

#### Example of Private Properties:
```javascript
class Person {
  #name; // Private property
  #age;  // Private property

  constructor(name, age) {
    this.#name = name;
    this.#age = age;
  }

  getDetails() {
    return `${this.#name}, Age: ${this.#age}`;
  }

  // Setters and getters for private properties
  setName(name) {
    this.#name = name;
  }

  getName() {
    return this.#name;
  }
}

const person = new Person('John', 30);
console.log(person.getDetails());  // Output: John, Age: 30

// Direct access to private properties will throw an error
// console.log(person.#name);  // SyntaxError
```

In this example:
- `#name` and `#age` are private properties, which cannot be accessed directly from outside the class.
- Methods like `getDetails()`, `setName()`, and `getName()` are used to interact with these properties.

---

## Overriding Derived Properties

In OOP, when a derived class extends a base class, it can override properties and methods of the base class. This is called **method overriding**.

#### Example of Overriding:
```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a sound.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);  // Calls the parent class constructor
    this.breed = breed;
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog('Buddy', 'Golden Retriever');
dog.speak();  // Output: Buddy barks.
```

- The `Dog` class overrides the `speak()` method from `Animal` to provide its own implementation.

---

## Getters and Setters

**Getters and Setters** are methods used to access and update the value of private properties in a class.

- **Getter**: Allows you to retrieve the value of a private property.
- **Setter**: Allows you to set or modify the value of a private property.

#### Example of Getters and Setters:
```javascript
class Circle {
  #radius;  // Private property

  constructor(radius) {
    this.#radius = radius;
  }

  // Getter
  get radius() {
    return this.#radius;
  }

  // Setter
  set radius(value) {
    if (value <= 0) {
      console.log('Radius must be positive.');
    } else {
      this.#radius = value;
    }
  }

  area() {
    return Math.PI * this.#radius ** 2;
  }
}

const circle = new Circle(5);
console.log(circle.radius);  // Output: 5
circle.radius = 10;
console.log(circle.radius);  // Output: 10
console.log(circle.area());  // Output: 314.159...
circle.radius = -3;  // Output: Radius must be positive.
```

- The `radius` property is private, and the getter and setter methods are used to access and modify its value.

---

## Static Methods

**Static methods** belong to the class itself, rather than to instances of the class. They are typically used for utility functions that don’t require an instance of the class to be created.

#### Example of Static Methods:
```javascript
class MathUtility {
  static add(a, b) {
    return a + b;
  }

  static subtract(a, b) {
    return a - b;
  }
}

console.log(MathUtility.add(5, 3));  // Output: 8
console.log(MathUtility.subtract(5, 3));  // Output: 2
```

- Static methods are accessed directly from the class (e.g., `MathUtility.add(5, 3)`), not from an instance.

---

## Use Case Example

Let’s say you are building a **Library System** for managing books and authors. Here’s how we can structure the classes:

### Step 1: Create the Base and Derived Classes
```javascript
class Author {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  getDetails() {
    return `${this.name}, Age: ${this.age}`;
  }
}

class Book {
  static totalBooks = 0;  // Static property

  constructor(title, author) {
    this.title = title;
    this.author = author; // An instance of Author class
    Book.totalBooks += 1;  // Update static property
  }

  getBookInfo() {
    return `"${this.title}" by ${this.author.name}`;
  }

  static getTotalBooks() {
    return Book.totalBooks;
  }
}

// Create instances
const author1 = new Author('J.K. Rowling', 55);
const book1 = new Book('Harry Potter', author1);

console.log(book1.getBookInfo());  // Output: "Harry Potter" by J.K. Rowling
console.log(Book

.getTotalBooks());  // Output: 1
```

- We have an `Author` class and a `Book` class.
- `Book` has a **static method** `getTotalBooks()` to track the total number of books created.

---

## Project - Inventory System

### Project Overview

Let’s build a simple **Inventory System** for managing items in a store. We'll create classes for **Item** and **Inventory**, demonstrating private properties, getters, setters, static methods, and inheritance.

### Step 1: Define the Classes

```javascript
class Item {
  #name;
  #price;
  #quantity;

  constructor(name, price, quantity) {
    this.#name = name;
    this.#price = price;
    this.#quantity = quantity;
  }

  getDetails() {
    return `${this.#name} - $${this.#price} (Quantity: ${this.#quantity})`;
  }

  set price(value) {
    if (value < 0) {
      console.log('Price must be positive');
    } else {
      this.#price = value;
    }
  }

  get price() {
    return this.#price;
  }
}

class Inventory {
  static totalItems = 0;

  constructor() {
    this.items = [];
  }

  addItem(item) {
    this.items.push(item);
    Inventory.totalItems++;
  }

  static getTotalItems() {
    return Inventory.totalItems;
  }

  showInventory() {
    this.items.forEach(item => console.log(item.getDetails()));
  }
}

const inventory = new Inventory();

const item1 = new Item('Laptop', 1000, 10);
const item2 = new Item('Phone', 500, 20);

inventory.addItem(item1);
inventory.addItem(item2);

inventory.showInventory();
console.log(`Total items in inventory: ${Inventory.getTotalItems()}`);
```

### Step 2: Final Integration

- We created `Item` and `Inventory` classes.
- `Item` uses private properties (`#name`, `#price`, `#quantity`) and getters/setters.
- `Inventory` manages a list of items and includes a static method for counting total items.

### Final Output:

```
Laptop - $1000 (Quantity: 10)
Phone - $500 (Quantity: 20)
Total items in inventory: 2
```

---

## Best Practices for OOP in JavaScript

1. **Use Encapsulation**: Always encapsulate properties and methods that should not be accessible outside the class. Use private properties with `#`.
2. **Leverage Inheritance**: Use inheritance when there are shared behaviors across classes. This allows for code reuse and cleaner designs.
3. **Use Static Methods for Utility Functions**: Keep utility functions that do not rely on instance data in static methods.
4. **Use Getters and Setters for Controlled Access**: When you need control over property modification, use getters and setters.
5. **Abstraction**: Hide complex logic within methods and only expose the necessary functionality.
