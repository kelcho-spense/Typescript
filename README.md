# Typescript

## OOP Concepts in TypeScript

### Classes

Classes are the blueprint for creating objects in TypeScript. They can have properties (variables) and methods (functions). TypeScript supports constructors, access modifiers, and static methods in classes.

#### Object

An object is an instance of a class. It can have its own properties and methods.

```typescript
class Person {
  public name: string;
  private age: number;
  protected married: boolean;

  constructor(_name: string, _age: number, _married:boolean) {
    this.name = _name;
    this.age = _age;
    this.married = _married;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old , I'm am ${ this.married ? "married" : "not married"}.`);
  }
}

const person:Person = new Person("John", 30,true); // Create a new Person object
person.greet(); // "Hello, my name is John, I'm am 30 years old and I am married."
```

#### Setter and Getters

Setters and getters are used to set and get the values of private properties in a class.

```typescript
class Person {
  private _age: number;

  constructor(private _name: string) {}

  // Getter method to access the private property 'age'
  get age(): number {
    return this._age;
  }

  // Setter method to set the private property 'age'
  set age(value: number) {
    if (value < 0) {
      throw new Error("Age cannot be negative.");
    }
    this._age = value;
  }
}

let newGuy:Person = new Person("John"); // Create a new Person object
newGuy.age = 30; // Set the age using the setter method
console.log(newGuy.age); // Get the age using the getter method

```

#### Parameter Properties

Parameter properties allow you to declare and initialize properties in a class without explicitly declaring them.

```typescript
class Person {
  constructor(public name: string, private age: number) {}

  get myAge() {
    return this.age
  }
}
```

#### Public Static Methods

Public Static methods are methods that belong to the class itself and not to the objects created from the class. They can be called without creating an instance of the class.

```typescript
class MathUtils {
  static add(a: number, b: number): number {
    return a + b;
  }
}

console.log(MathUtils.add(2, 3)); // 5
```

##### Private Static Methods

Private static methods are static methods that are only accessible within the class.

```typescript
class MathUtils {
  private static add(a: number, b: number): number {
    return a + b;
  }

  static addNumbers(a: number, b: number): number {
    return MathUtils.add(a, b);
  }
}

console.log(MathUtils.addNumbers(2, 3)); // 5


const person:Person = new Person("John", 30); // Create a new Person object
console.log(person.name); // "John"
console.log(person.myAge) // 30
```

### Abstract Classes

Abstract classes are classes that cannot be instantiated directly. They are used as base classes for other classes to inherit from.

```typescript
abstract class Animal {
  abstract makeSound(): void;
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Woof");
  }
}

const dog: Dog = new Dog();
dog.makeSound(); // "Woof"

```

### Interfaces

Interfaces are used to define the structure of an object. They can be used to define properties, methods, and index signatures that an object must have.

```typescript
interface Person {
  name: string;
  age: number;
  married: boolean;
}

const person: Person = {
  name: "John",
  age: 30,
  married: true
};

console.log(person.name); // "John"
console.log(person.age); // 30
console.log(person.married); // true
```

### Implementing Interfaces

A class can implement an interface by using the `implements` keyword. The class must provide an implementation for all the properties and methods defined in the interface. The gatch here is that the class must have the same properties and methods as the interface. ie 

- the class must have the same properties and methods as the interface.
- the class must have the same access modifiers as the interface.

#### Public Implementing Interfaces

```typescript
interface Person {
  name: string;
  age: number;
  married: boolean;
}

class Employee implements Person {
  constructor(public name: string, public age: number, public married: boolean) {}

  public nowMe(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old , I'm am ${ this.married ? "married" : "not married"}.`);
  }
}

const employee: Employee = new Employee("John", 30, true);
console.log(employee.name); // "John"
console.log(employee.age); // 30
console.log(employee.married); // true
employee.nowMe(); // "Hello, my name is John and I am 30 years old , I'm am married."
```

#### Private Implementing Interfaces

```typescript
interface Person {
  name: string;
  age: number;
  married: boolean;
}

class Employee implements Person {
  constructor(private _name: string, private _age: number, private _married: boolean) {}

  get name(): string {
    return this._name;
  }

  get age(): number {
    return this._age;
  }

  get married(): boolean {
    return this._married;
  }

  public nowMeet(): void {
    console.log(`Hello, my name is ${this._name} and I am ${this._age} years old , I'm am ${ this._married ? "married" : "not married"}.`);
  }
}

const employee: Employee = new Employee("John", 30, true);
console.log(employee.name); // "John"
console.log(employee.age); // 30
console.log(employee.married); // true
employee.nowMeet(); // "Hello, my name is John and I am 30 years old , I'm am married."
```

#### Generics

Generics allow you to create reusable components that can work with a variety of data types rather than a single data type. They are used to create classes, interfaces, and functions that can work with any data type.

```typescript 
class Box<T> {
  private value: T;

  constructor(value: T) {
    this.value = value;
  }

  getValue(): T {
    return this.value;
  }
}

const box1: Box<number> = new Box<number>(10);
console.log(box1.getValue()); // 10

const box2: Box<string> = new Box<string>("Hello");
console.log(box2.getValue()); // "Hello"
```

#### Mixins

Mixins are a way to combine multiple classes into a single class. They are used to add functionality to a class without using inheritance.

```typescript 
class Person {
  constructor(public name: string) {}
}

class Employee {
  constructor(public position: string) {}
}
// Mixin to combine Person and Employee classes
type Constructor<T = {}> = new (...args: any[]) => T;

function withEmployee<TBase extends Constructor>(Base: TBase) {
  return class extends Base {
    position: string;

    constructor(...args: any[]) {
      super(...args);
      this.position = "Developer";
    }
  };
}

const EmployeePerson = withEmployee(Person);
const employeePerson = new EmployeePerson("John");
console.log(employeePerson.name); // "John"
console.log(employeePerson.position); // "Developer"
```

## OOP Principles

### Encapsulation

Encapsulation is the concept of hiding the internal details of an object and exposing only the necessary parts. In TypeScript, this can be achieved using access modifiers like public, private, and protected.

- public: The property or method is accessible anywhere.
- private: The property or method is only accessible within the class.
- protected: The property or method is accessible within the class and its subclasses.

```typescript
class Person {
  public name: string;
  private age: number;
  protected married: boolean;

  constructor(_name: string, _age: number, _married:boolean) {
    this.name = _name;
    this.age = _age;
    this.married = _married;
  }

// Method to greet
  greet(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old , I'm am ${ this.married ? "married" : "not married"}.`);
  }
  // Getter method to access the private property 'age'
    get myAge(): number {
    return this.age
  }
}

const person:Person = new Person("John", 30,true); // Create a new Person object
person.greet(); // "Hello, my name is John, I'm am 30 years old and I am married."
console.log(person.age); // Error: Property 'age' is private and only accessible within class 'Person'.
console.log(person.married); // Error: Property 'married' is protected and only accessible within class 'Person' and its subclasses.
console.log(person.myAge); // age can be accessed using the getter method

```

### Inheritance

Inheritance allows you to create a new class based on an existing class. The new class (child) inherits the properties and methods of the existing class (parent).

```typescript

class human {
  public name: string;
  protected age: number;
  protected married: boolean;

  constructor(_name: string, _age: number, _married:boolean) {
    this.name = _name;
    this.age = _age;
    this.married = _married;
  }

  greet(): void {
    console.log(`Hello, my name is ${this.name} and I am ${this.age} years old , I'm am ${ this.married ? "married" : "not married"}.`);
  }
}

class Employee extends human {
  public position: string;

  constructor(_name: string, age: number, married:boolean, _position: string) {
    super(_name, age, married);
    this.position = _position;
  }

  work(): void {
    console.log(`${this.name} of age ${this.age} who is ${this.married ? "married" : "not married"} is working as a ${this.position}.`);
  }
}

const employee:Employee = new Employee("John", 30,true, "Developer");
employee.greet(); // "Hello, my name is John, I'm am 30 years old and I am married."
employee.work(); // "John of age 30 who is married is working as a Developer."
```

### Polymorphism

Polymorphism is the ability of an object to take on many forms. In TypeScript, polymorphism can be achieved through method overriding.

```typescript
class Animal {
  makeSound(): void {
    console.log("Some sound");
  }
}

class Dog extends Animal {
  makeSound(): void {
    console.log("Woof");
  }
}

class Cat extends Animal {
  makeSound(): void {
    console.log("Meow");
  }
}

const dog: Dog = new Dog();
const cat: Cat = new Cat();

dog.makeSound(); // "Woof"
cat.makeSound(); // "Meow"
```

### Abstraction

Abstraction is the concept of hiding the complex implementation details and showing only the necessary parts. In TypeScript, abstraction can be achieved using abstract classes and methods.

Using a banking system as an example

- Defines an `abstract class` Bank with two abstract methods
- `Abstract methods` must be implemented by any class that extends this class

```typescript
abstract class Bank {
  abstract deposit(amount: number): void;
  abstract withdraw(amount: number): void;
}
```

Create a class `SavingsAccount` that extends the Bank class and implements the `deposit` and `withdraw` methods. Includes balance validation logic for withdrawals.

```typescript 

class SavingsAccount extends Bank {
  private balance: number = 0;

  deposit(amount: number): void {
    this.balance += amount;
    console.log(`Deposited ${amount}. Balance is now ${this.balance}.`);
  }

  withdraw(amount: number): void {
    if (this.balance < amount) {
      console.log("Insufficient balance.");
      return;
    }
    this.balance -= amount;
    console.log(`Withdrawn ${amount}. Balance is now ${this.balance}.`);
  }
}
```

- Demonstrates how to use the SavingsAccount class
- Shows the abstraction principle in action - users only interact with the public methods
- Hides the internal balance property

This example shows how `abstraction` hides the `internal balance property` while exposing only the necessary

```TypeScript
const savingsAccount: SavingsAccount = new SavingsAccount();
savingsAccount.deposit(1000); // "Deposited 1000. Balance is now 1000."
savingsAccount.withdraw(500); // "Withdrawn 500. Balance is now 500."
savingsAccount.withdraw(600); // "Insufficient balance."
```
