# Typescript
## OOP
### Classes
Classes are the blueprint for creating objects in TypeScript. They can have properties (variables) and methods (functions). TypeScript supports constructors, access modifiers, and static methods in classes.

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

const person = new Person("John", 30,true);
person.greet(); // "Hello, my name is John, I'm am 30 years old and I am married."
```

### Encapsulation
Encapsulation is the concept of hiding the internal details of an object and exposing only the necessary parts. In TypeScript, this can be achieved using access modifiers like public, private, and protected.

- public: The property or method is accessible anywhere.
- private: The property or method is only accessible within the class.
- protected: The property or method is accessible within the class and its subclasses.

