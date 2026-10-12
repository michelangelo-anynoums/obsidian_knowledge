# 🧩 JavaScript — Classes

> [!abstract] Overview **Classes** in JavaScript are templates for creating objects with shared properties and methods. They provide a clean, organized way to structure code and represent things such as users, products, cars, or animals. JavaScript classes use prototype-based inheritance behind the scenes.

## 1. Creating a Class

Use the `class` keyword to define a class.

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const person1 = new Person("Alice", 25);

console.log(person1.name); // "Alice"
console.log(person1.age);  // 25
```

- `class` defines a class.
- `constructor()` initializes a new object.
- `this` refers to the current instance.
- `new` creates a new instance of the class.

> [!tip] Remember The constructor is called automatically when you create an object using `new`.

## 2. Adding Methods

Methods are functions defined inside a class.

```js
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    return `Hello, my name is ${this.name}.`;
  }
}

const person = new Person("Alice");

console.log(person.greet());
// "Hello, my name is Alice."
```

Notice that we write `greet()` directly inside the class without using the `function` keyword.

## 3. Properties and `this`

Properties store information about an object.

```js
class Car {
  constructor(brand, year) {
    this.brand = brand;
    this.year = year;
  }

  getInfo() {
    return `${this.brand}, ${this.year}`;
  }
}

const car = new Car("Toyota", 2024);

console.log(car.brand);    // "Toyota"
console.log(car.getInfo()); // "Toyota, 2024"
```

Here, `this.brand` and `this.year` belong to the particular object being created.

> [!warning] Common mistake Inside an ordinary instance method, `this` depends on how the method is called. Extracting a method and calling it separately may cause `this` to be `undefined` in strict mode.

## 4. Getters and Setters

Getters and setters let you access or update a value using property-like syntax.

```js
class Rectangle {
  constructor(width, height) {
    this.width = width;
    this.height = height;
  }

  get area() {
    return this.width * this.height;
  }

  set resize(value) {
    this.width = value;
    this.height = value;
  }
}

const rectangle = new Rectangle(4, 5);

console.log(rectangle.area); // 20

rectangle.resize = 3;

console.log(rectangle.area); // 9
```

- `get` defines a getter.
- `set` defines a setter.
- Getters are accessed like properties, without parentheses.

## 5. Static Methods

A static method belongs to the class itself, not to its individual instances.

```js
class MathHelper {
  static add(a, b) {
    return a + b;
  }
}

console.log(MathHelper.add(3, 4)); // 7
```

You call the method using the class name.

```js
MathHelper.add(3, 4);
```

You cannot normally call it on an instance:

```js
const helper = new MathHelper();

// helper.add(3, 4); // TypeError
```

> [!tip] When to use static methods Use them for utility operations that do not need an individual object's properties.

## 6. Inheritance with `extends`

Inheritance allows one class to reuse and extend another class.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    return `${this.name} makes a sound.`;
  }
}

class Dog extends Animal {
  speak() {
    return `${this.name} barks.`;
  }
}

const dog = new Dog("Buddy");

console.log(dog.speak());
// "Buddy barks."
```

- `extends` establishes inheritance.
- `Dog` inherits from `Animal`.
- `Dog` overrides the `speak()` method with its own implementation.

## 7. Using `super()`

The `super` keyword allows a subclass to call functionality from its parent class.

```js
class Animal {
  constructor(name) {
    this.name = name;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);
    this.breed = breed;
  }
}

const dog = new Dog("Buddy", "Labrador");

console.log(dog.name);  // "Buddy"
console.log(dog.breed); // "Labrador"
```

> [!warning] Important In a derived class constructor, you must call `super()` before accessing `this`.

## 8. Private Properties

Use `#` to declare private fields that cannot be accessed directly from outside the class.

```js
class BankAccount {
  #balance = 0;

  deposit(amount) {
    if (amount > 0) {
      this.#balance += amount;
    }
  }

  getBalance() {
    return this.#balance;
  }
}

const account = new BankAccount();

account.deposit(100);

console.log(account.getBalance()); // 100

// console.log(account.#balance);
// SyntaxError: private field is inaccessible
```

Private fields help protect an object's internal state from direct external access.

## 9. Class Expressions

Classes can also be assigned to variables.

```js
const Person = class {
  constructor(name) {
    this.name = name;
  }
};

const person = new Person("Alice");

console.log(person.name); // "Alice"
```

This is called a **class expression**. The more familiar `class Person {}` syntax is a class declaration.

## 10. Classes vs. Objects

|Class|Object|
|---|---|
|Defines a template|Represents a particular value or entity|
|Can be used to create instances|Contains its own properties and behavior|
|Defined using `class`|Often created using `{}` or `new`|
|Can define constructors and methods|Can hold properties and methods|

Example:

```js
class User {
  constructor(name) {
    this.name = name;
  }
}

const user = new User("Alice");
```

Here, `User` is the class and `user` is an instance of that class.

## 11. Important Things to Remember

- Use `class` to define a class.
- Use `new` to create an instance.
- Use `constructor()` to initialize instance properties.
- Use `this` to access the current instance.
- Use `extends` to inherit from another class.
- Use `super()` to call the parent constructor.
- Use `static` for methods called on the class itself.
- Use `#` for private fields.
- Class methods are stored on the class prototype rather than copied into every instance.
- Classes are built on JavaScript's prototype system.

## 12. Quick Reference

|Keyword / Syntax|Purpose|
|---|---|
|`class`|Define a class|
|`constructor()`|Initialize an instance|
|`new`|Create an instance|
|`this`|Refer to the current instance|
|`extends`|Inherit from another class|
|`super()`|Call the parent constructor|
|`static`|Define a class-level method|
|`get`|Define a getter|
|`set`|Define a setter|
|`#property`|Declare a private field|

---
