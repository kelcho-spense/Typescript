# Typescript

## OOP

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

const person:Person = new Person("John", 30); // Create a new Person object
console.log(person.name); // "John"
console.log(person.myAge) // 30
```

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
