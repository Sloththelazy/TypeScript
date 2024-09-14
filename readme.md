# Notes of TypeScript

## Variables in TypeScript

In TypeScript, variables can be declared using different types that help ensure type safety and proper use of values in a program. Here are the main types of variables in TypeScript:

### 1. **Primitive Types:**
   These types are the building blocks for TypeScript.

   - **`number`**: Represents both integer and floating-point numbers.
     ```typescript
     let age: number = 30;
     let price: number = 19.99;
     ```
   
   - **`string`**: Represents textual data.
     ```typescript
     let name: string = "John";
     let message: string = `Hello, ${name}`;
     ```

   - **`boolean`**: Represents true or false values.
     ```typescript
     let isLoggedIn: boolean = true;
     ```

   - **`null`**: Represents the intentional absence of any object value.
     ```typescript
     let data: null = null;
     ```

   - **`undefined`**: Represents a variable that has been declared but not assigned a value.
     ```typescript
     let result: undefined;
     ```

   - **`symbol`**: Represents unique and immutable values.
     ```typescript
     let uniqueKey: symbol = Symbol();
     ```

   - **`bigint`**: Represents large integers.
     ```typescript
     let largeNumber: bigint = 9007199254740991n;
     ```

### 2. **Reference / Complex Types:**
   These types build on primitive types and provide more structure.

   - **`Array<T>`** or `T[]`: Represents a collection of values of type `T`.
     ```typescript
     let numbers: number[] = [1, 2, 3, 4, 5];
     ```

   - **`Tuple`**: A fixed-length array where each element may have a different type.
     ```typescript
     let person: [string, number] = ["John", 25];
     ```

   - **`Object`**: Represents any non-primitive value.
     ```typescript
     let user: { name: string; age: number } = { name: "Alice", age: 30 };
     ```

   - **`Enum`**: A way of defining a set of named constants.
     ```typescript
     enum Direction { North, South, East, West }
     let dir: Direction = Direction.North;
     ```

### 3. **Union Types:**
   A variable can be one of several types.
   ```typescript
   let id: number | string = 123;
   id = "ABC123";
   ```

### 4. **Intersection Types:**
   Combines multiple types into one.
   ```typescript
   interface Person { name: string }
   interface Employee { id: number }
   let worker: Person & Employee = { name: "John", id: 101 };
   ```

### 5. **Any Type:**
   Allows a variable to hold any type of value. Use cautiously as it disables type checking.
   ```typescript
   let value: any = "hello";
   value = 10;  // No error
   ```

### 6. **Unknown Type:**
   Similar to `any`, but requires type checking before performing operations on the variable.
   ```typescript
   let value: unknown = "hello";
   if (typeof value === "string") {
     console.log(value.toUpperCase());  // Safe
   }
   ```

### 7. **Void Type:**
   Represents the absence of any type, commonly used for functions that do not return a value.
   ```typescript
   function logMessage(): void {
     console.log("This function returns nothing");
   }
   ```

### 8. **Never Type:**
   Represents the type of values that never occur, often used for functions that always throw an error or never return.
   ```typescript
   function throwError(message: string): never {
     throw new Error(message);
   }
   ```

### 9. **Literal Types:**
   Exact values can be used as types.
   ```typescript
   let direction: "left" | "right" = "left";
   ```

TypeScript's strong type system allows for more readable and maintainable code by catching type-related errors during development.
--------------------------------------------------------------------------------
In TypeScript, **type inference** and **type annotations** are two key concepts for working with types.

### 1. **Type Inference**
Type inference refers to TypeScript's ability to automatically determine the type of a variable based on the value assigned to it, without the need for explicit type declarations. TypeScript tries to infer the most specific type possible, allowing for cleaner and shorter code.

#### Example of Type Inference:
```typescript
let message = "Hello, World!";
// TypeScript infers 'message' as a 'string' based on the assigned value.

let age = 25;
// TypeScript infers 'age' as 'number'.
```

In this example, you don't need to explicitly state that `message` is a `string` or `age` is a `number`—TypeScript automatically understands this from the value assigned to the variable.

#### Function Example:
```typescript
function add(x: number, y: number) {
  return x + y;
}
// TypeScript infers that the return type of 'add' is 'number' based on the operation.
```

Here, the function `add` returns a number, and TypeScript infers the return type automatically based on the type of parameters and the operations performed.

### 2. **Type Annotations**
Type annotations are used when you explicitly declare the type of a variable, parameter, or function. You do this by adding a colon (`:`) followed by the type after the variable or function parameter name.

#### Example of Type Annotations:
```typescript
let message: string = "Hello, World!";
// Explicitly declaring that 'message' is of type 'string'.

let age: number = 25;
// Explicitly declaring that 'age' is of type 'number'.
```

Type annotations are particularly useful when the type isn't immediately obvious from the assigned value or when TypeScript can't infer the correct type.

#### Function Example:
```typescript
function multiply(x: number, y: number): number {
  return x * y;
}
// Here, the parameter types ('number') and the return type ('number') are explicitly declared.
```

### When to Use Type Annotations vs Type Inference
- **Use Type Annotations**:
  - When the type isn't clear or can't be inferred easily.
  - When you want to ensure a specific type for future readers or maintainers of the code.
  - For function parameters and return types where inference might not work or might be less clear.

- **Use Type Inference**:
  - When the type is clear from the assigned value, keeping the code clean and readable.
  - When the inferred type is accurate, and there's no need to enforce a specific type manually.

#### Example where Type Annotation is Necessary:
```typescript
let input: number | string = "Hello";
// TypeScript wouldn't be able to infer that 'input' can be both 'number' or 'string' without an annotation.
```

### Summary:
- **Type Inference**: TypeScript automatically deduces the type from the assigned value.
- **Type Annotations**: You explicitly specify the type to enforce stricter type checking or when inference isn't sufficient.

--------------------------------------------------------------------------------

### INFERENCES AND TYPE ALIASES
In TypeScript, both **interfaces** and **type aliases** are used to define the shapes of objects, but they have some differences in usage and capabilities. Here's an in-depth look at both:

### 1. **Interfaces**

An **interface** defines the structure of an object by specifying its properties and their types. Interfaces are primarily used for defining object shapes and are extendable, making them very useful for object-oriented programming.

#### Syntax:
```typescript
interface Person {
  name: string;
  age: number;
  greet(): void;
}
```

#### Example of Usage:
```typescript
let user: Person = {
  name: "John",
  age: 30,
  greet() {
    console.log("Hello");
  },
};
```

#### Key Features of Interfaces:
- **Optional Properties**: Properties can be marked as optional using the `?` symbol.
  ```typescript
  interface Car {
    brand: string;
    model?: string;  // Optional property
  }
  ```

- **Read-only Properties**: Properties can be marked as read-only using the `readonly` keyword, preventing modification after initialization.
  ```typescript
  interface Book {
    readonly title: string;
    author: string;
  }
  ```

- **Method Signatures**: Interfaces can define methods and their signatures, but the implementation is provided later.
  ```typescript
  interface Animal {
    sound(): string;
  }
  ```

- **Extending Interfaces**: Interfaces can be extended using the `extends` keyword, allowing you to combine multiple interfaces into one.
  ```typescript
  interface Employee extends Person {
    salary: number;
  }
  ```

- **Merging**: Interfaces can be merged or augmented across multiple declarations.
  ```typescript
  interface Shape {
    color: string;
  }

  interface Shape {
    sides: number;
  }

  const square: Shape = { color: "red", sides: 4 };
  ```

### 2. **Type Aliases**

A **type alias** is a way to give a name to a specific type. It can be used for any kind of type, including primitives, union types, tuples, arrays, or object types. It's more flexible than interfaces in terms of what it can describe.

#### Syntax:
```typescript
type Person = {
  name: string;
  age: number;
  greet(): void;
};
```

#### Example of Usage:
```typescript
let user: Person = {
  name: "Alice",
  age: 25,
  greet() {
    console.log("Hi!");
  },
};
```

#### Key Features of Type Aliases:
- **Union and Intersection Types**: Type aliases can define union or intersection types, which interfaces cannot.
  ```typescript
  type ID = number | string;  // Union type

  type Employee = Person & { salary: number };  // Intersection type
  ```

- **Tuple Types**: Type aliases can also define tuple types.
  ```typescript
  type Coordinates = [number, number];
  ```

- **Primitive and Function Types**: You can alias primitive types, functions, or even complex types.
  ```typescript
  type Name = string;
  type Add = (a: number, b: number) => number;
  ```

- **Cannot be Merged**: Unlike interfaces, type aliases cannot be merged. Each `type` definition is separate and doesn't allow declaration merging.

### Differences Between Interfaces and Type Aliases

| Feature                      | Interface                                   | Type Alias                                   |
|------------------------------|---------------------------------------------|---------------------------------------------|
| **Primary Use**               | Describes the shape of objects and classes. | Can alias any type (object, union, primitive, etc.). |
| **Object Type Description**   | Can only be used for objects.               | Can describe objects, primitives, functions, etc. |
| **Extension**                 | Can be extended using `extends`.            | Can create intersections using `&`.         |
| **Declaration Merging**       | Can be merged with the same name.           | Cannot be merged with the same name.        |
| **Union/Intersection Types**  | Not allowed.                               | Supports union (`|`) and intersection (`&`) types. |
| **Implements**                | Classes can implement interfaces.           | Classes can also implement type aliases (if they represent objects). |

### When to Use **Interface** vs **Type Alias**:
- **Use `interface`** when you're defining the shape of an object or class, especially if you need to use features like extension, merging, or method signatures.
- **Use `type`** when you need to create more complex types, such as union types, intersection types, tuples, or function types, and when you need flexibility beyond object shapes.

### Example Comparison:

#### Interface:
```typescript
interface User {
  name: string;
  age: number;
  greet(): void;
}
```

#### Type Alias:
```typescript
type User = {
  name: string;
  age: number;
  greet(): void;
};
```

Both of the above are equivalent when used to define object types, but type aliases provide more flexibility when it comes to unions, intersections, and more complex types.

## Classes and Objects

In TypeScript (and other object-oriented languages like JavaScript), **classes**, **objects**, and **constructors** are fundamental concepts used to organize code in a structured, modular, and reusable way.

### 1. **Classes**

A **class** is a blueprint for creating objects. It defines properties (data) and methods (behavior) that the objects created from the class will have. In TypeScript, classes support **inheritance**, **encapsulation**, and **polymorphism**, enabling object-oriented design.

#### Syntax:
```typescript
class Person {
  name: string;
  age: number;

  // Constructor: called when a new instance of the class is created
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  // Method
  greet() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}
```

### 2. **Objects**

An **object** is an instance of a class. When you create an object from a class, you can access the class's properties and methods. Objects are the actual data structures created based on the blueprint provided by the class.

#### Creating an Object:
```typescript
const person1 = new Person("John", 30);
person1.greet();  // Outputs: "Hello, my name is John and I'm 30 years old."
```

Here, `person1` is an object created from the `Person` class. You can create multiple objects from the same class, each with its own properties and behaviors.

### 3. **Constructors**

The **constructor** is a special method in a class that is called when a new object is instantiated. It initializes the object’s properties and performs any setup required when an instance is created. In TypeScript, the constructor is defined using the `constructor` keyword.

#### Constructor Example:
```typescript
class Car {
  brand: string;
  model: string;
  year: number;

  // Constructor method
  constructor(brand: string, model: string, year: number) {
    this.brand = brand;
    this.model = model;
    this.year = year;
  }

  describe() {
    console.log(`${this.year} ${this.brand} ${this.model}`);
  }
}

// Creating objects (instances)
const myCar = new Car("Toyota", "Corolla", 2022);
myCar.describe();  // Outputs: "2022 Toyota Corolla"
```

In this example, the `constructor` method accepts three parameters (`brand`, `model`, and `year`), and when a new `Car` object is created, these values are passed to initialize the properties of the `Car` object.

### Key Concepts in Classes

#### 1. **Properties**:
Properties are the attributes or data associated with a class. In TypeScript, you can define properties with specific types to ensure type safety.

```typescript
class Animal {
  species: string;
  legs: number;

  constructor(species: string, legs: number) {
    this.species = species;
    this.legs = legs;
  }
}
```

#### 2. **Methods**:
Methods are functions defined inside a class that operate on the properties of the class.

```typescript
class Calculator {
  add(a: number, b: number): number {
    return a + b;
  }

  subtract(a: number, b: number): number {
    return a - b;
  }
}

const calc = new Calculator();
console.log(calc.add(5, 3));  // Outputs: 8
```

#### 3. **Access Modifiers**:
TypeScript supports access modifiers (`public`, `private`, and `protected`) to control the visibility of class members.

- **`public`**: Members are accessible from anywhere (default behavior).
- **`private`**: Members are accessible only within the class they are defined in.
- **`protected`**: Members are accessible within the class and its subclasses.

```typescript
class Employee {
  public name: string;
  private salary: number;

  constructor(name: string, salary: number) {
    this.name = name;
    this.salary = salary;
  }

  public getSalary(): number {
    return this.salary;
  }
}

const emp = new Employee("Alice", 50000);
console.log(emp.name);     // Accessible
console.log(emp.getSalary());  // Accessible through a public method
// console.log(emp.salary);  // Error: 'salary' is private
```

#### 4. **Inheritance**:
Classes in TypeScript can **inherit** from other classes using the `extends` keyword. This allows a class to inherit properties and methods from a parent class.

```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(`Hello, I'm ${this.name}`);
  }
}

class Employee extends Person {
  jobTitle: string;

  constructor(name: string, age: number, jobTitle: string) {
    super(name, age);  // Call the parent class constructor
    this.jobTitle = jobTitle;
  }

  describe() {
    console.log(`I'm ${this.name}, a ${this.jobTitle}.`);
  }
}

const emp = new Employee("John", 28, "Software Developer");
emp.greet();       // Outputs: "Hello, I'm John"
emp.describe();    // Outputs: "I'm John, a Software Developer."
```

In the above example, `Employee` class inherits from the `Person` class, so it has access to the `greet` method from `Person`.

#### 5. **Static Methods and Properties**:
Static methods and properties belong to the class itself, not to instances of the class. They are accessed using the class name.

```typescript
class MathUtil {
  static pi = 3.14159;

  static calculateArea(radius: number): number {
    return this.pi * radius * radius;
  }
}

console.log(MathUtil.pi);                // Access static property
console.log(MathUtil.calculateArea(5));  // Access static method
```

### Summary:
- **Class**: A blueprint for creating objects that define properties and methods.
- **Object**: An instance of a class that has specific values for the properties and can use the class’s methods.
- **Constructor**: A special method used to initialize objects when they are created.

These concepts are essential for writing structured and maintainable code in object-oriented programming with TypeScript.
