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

#### This Keyword

The `this` keyword in TypeScript (and JavaScript) refers to the context or object on which the current code is being executed. It helps in accessing properties and methods of the current object within a class or function.

### Key Aspects of the `this` Keyword:

1. **Inside a Class**: 
   In a class, `this` refers to the current instance of the class. It is used to access the class properties and methods.

#### Example:
```typescript
class Person {
  name: string;
  age: number;

  constructor(name: string, age: number) {
    this.name = name;  // 'this' refers to the current instance of the Person class
    this.age = age;
  }

  greet() {
    console.log(`Hello, my name is ${this.name} and I'm ${this.age} years old.`);
  }
}

const person1 = new Person("Alice", 25);
person1.greet();  // Outputs: Hello, my name is Alice and I'm 25 years old.
```

In the `greet` method, `this.name` and `this.age` refer to the instance properties of the object (`person1`) that called the method.

### 2. **In Regular Functions**:
When a function is a regular function (not an arrow function) and is called as a method of an object, `this` refers to the object that called the method.

#### Example:
```typescript
const car = {
  brand: "Toyota",
  model: "Corolla",
  describe() {
    console.log(`This car is a ${this.brand} ${this.model}.`);
  }
};

car.describe();  // 'this' refers to the 'car' object, Outputs: "This car is a Toyota Corolla."
```

In this example, `this` refers to the `car` object because `describe` is called as a method of `car`.

### 3. **Arrow Functions**:
In arrow functions, `this` is lexically bound, meaning it uses the value of `this` from the surrounding context where the arrow function was created. Arrow functions do not have their own `this`.

#### Example:
```typescript
class Counter {
  count = 0;

  increaseCount = () => {
    console.log(this.count);  // 'this' refers to the instance of the class
    this.count++;
  }
}

const counter = new Counter();
counter.increaseCount();  // Outputs: 0
counter.increaseCount();  // Outputs: 1
```

In this case, `this` in the arrow function refers to the instance of the `Counter` class, even if the method is called from a different context later.

### 4. **Binding `this` in Methods**:
Sometimes, when passing methods as callbacks, the value of `this` might change. To preserve the original value of `this`, you can use the `bind` method, arrow functions, or store `this` in a variable.

#### Example with `bind`:
```typescript
class Button {
  label: string;

  constructor(label: string) {
    this.label = label;
  }

  click() {
    console.log(`Button ${this.label} clicked!`);
  }
}

const button = new Button("Submit");
const handleClick = button.click.bind(button);  // Binding 'this' to 'button'
handleClick();  // Outputs: "Button Submit clicked!"
```

If you don't bind `this`, calling `handleClick` may result in `this` being `undefined` or referring to another object, depending on the context.

### 5. **Global Context**:
In global functions (outside of classes or objects), `this` refers to the global object. However, in TypeScript with `strict mode` (`"use strict"`), `this` in global functions will be `undefined`.

#### Example (Global Context):
```typescript
function show() {
  console.log(this);
}

show();  // In non-strict mode, 'this' refers to the global object (window in browsers).
```

In strict mode or when running TypeScript with `"strict": true` in `tsconfig.json`, `this` will be `undefined` inside functions that are not part of an object or class.

### Summary:
- **`this` in a class** refers to the instance of the class.
- **`this` in a method** refers to the object that called the method.
- **`this` in an arrow function** refers to the context in which the arrow function was created (lexical scoping).
- **`this` can be bound** to a specific context using `.bind()`, or you can use arrow functions to preserve the value of `this`.
- **In global functions**, `this` refers to the global object (in non-strict mode).


#### Access Modifiers

In TypeScript, **access modifiers** are used to control the visibility of class members (properties and methods). There are three main access modifiers:

### 1. **`public`** (Default)
   - The `public` access modifier allows class members to be accessible from **anywhere**. 
   - It is the default modifier, so even if no access modifier is explicitly defined, the member is treated as `public`.

#### Example:
```typescript
class Person {
  public name: string;  // 'public' keyword is optional since it is the default

  constructor(name: string) {
    this.name = name;
  }

  public greet() {
    console.log(`Hello, my name is ${this.name}.`);
  }
}

const person = new Person("Alice");
console.log(person.name);  // Accessible: "Alice"
person.greet();            // Accessible: "Hello, my name is Alice."
```

### 2. **`private`**
   - The `private` access modifier restricts the visibility of class members to **within the class itself**. 
   - Members marked as `private` cannot be accessed or modified from outside the class, even by instances of the class.

#### Example:
```typescript
class Employee {
  private salary: number;

  constructor(salary: number) {
    this.salary = salary;
  }

  public getSalary(): number {
    return this.salary;  // Accessible within the class
  }

  private setSalary(newSalary: number) {
    this.salary = newSalary;  // Private method, only accessible within the class
  }
}

const employee = new Employee(50000);
console.log(employee.getSalary());  // Accessible through public method: 50000
// console.log(employee.salary);    // Error: 'salary' is private
// employee.setSalary(60000);       // Error: 'setSalary' is private
```

Here, `salary` is a `private` property, and `setSalary` is a `private` method, both of which cannot be accessed outside the class.

### 3. **`protected`**
   - The `protected` access modifier allows members to be accessible **within the class** and **in subclasses** (derived classes), but **not from outside**.
   - This is useful when you want to allow derived classes to access or override the properties/methods, but not expose them publicly.

#### Example:
```typescript
class Person {
  protected age: number;

  constructor(age: number) {
    this.age = age;
  }

  protected getAge(): number {
    return this.age;  // Accessible within the class
  }
}

class Student extends Person {
  public showAge() {
    console.log(this.age);  // Accessible in the subclass
    console.log(this.getAge());  // Protected method accessible in subclass
  }
}

const student = new Student(21);
student.showAge();  // Accessible: 21
// console.log(student.age);  // Error: 'age' is protected
// console.log(student.getAge());  // Error: 'getAge' is protected
```

In this example, the `age` property and `getAge` method are marked as `protected`, so they are only accessible within the `Person` class and its subclass `Student`, but not outside.

### Summary of Access Modifiers

| Modifier    | Visibility                                                        |
|-------------|-------------------------------------------------------------------|
| **`public`**  | Accessible from **anywhere** (inside and outside the class).       |
| **`private`** | Accessible **only within the class** where it is defined.          |
| **`protected`** | Accessible **within the class** and its **subclasses**, but not outside. |

### Example Combining All Modifiers:

```typescript
class Vehicle {
  public brand: string;       // Can be accessed from anywhere
  private engineNumber: string;  // Can only be accessed inside the class
  protected speed: number;    // Can be accessed in this class and its subclasses

  constructor(brand: string, engineNumber: string, speed: number) {
    this.brand = brand;
    this.engineNumber = engineNumber;
    this.speed = speed;
  }

  public describe() {
    console.log(`This is a ${this.brand} moving at ${this.speed} km/h.`);
  }

  private getEngineNumber() {
    return this.engineNumber;  // Private method, accessible only within the class
  }

  protected increaseSpeed(increment: number) {
    this.speed += increment;  // Protected method, accessible in subclasses
  }
}

class Car extends Vehicle {
  constructor(brand: string, engineNumber: string, speed: number) {
    super(brand, engineNumber, speed);
  }

  public accelerate() {
    this.increaseSpeed(20);  // Can access protected method from superclass
    console.log(`${this.brand} is now moving at ${this.speed} km/h.`);
  }
}

const myCar = new Car("Tesla", "ENG123456", 60);
myCar.describe();  // Outputs: "This is a Tesla moving at 60 km/h."
myCar.accelerate();  // Outputs: "Tesla is now moving at 80 km/h."

// myCar.engineNumber;  // Error: 'engineNumber' is private
// myCar.increaseSpeed(30);  // Error: 'increaseSpeed' is protected
```

In this example, the `brand` is `public`, the `engineNumber` is `private`, and the `speed` and `increaseSpeed` are `protected`. These access levels control where and how each member can be accessed.


### Getters and Setters
In TypeScript, **getters** and **setters** allow you to define methods that are used to control access to the properties of a class. They provide a way to encapsulate data, enabling logic to be executed when accessing or modifying class properties.

### **Getters (`get`)**:
- Used to **retrieve** or **access** the value of a private or protected property.
- They act like a property but allow additional logic to be executed when the value is accessed.

### **Setters (`set`)**:
- Used to **set** or **update** the value of a private or protected property.
- They also act like a property but allow additional logic to be executed when the value is modified, such as validation or transformation.

### Syntax of Getter and Setter:

```typescript
class Person {
  private _name: string;  // Private property

  constructor(name: string) {
    this._name = name;
  }

  // Getter
  get name(): string {
    return this._name;
  }

  // Setter
  set name(newName: string) {
    if (newName.length > 0) {
      this._name = newName;
    } else {
      console.log("Name can't be empty!");
    }
  }
}

const person = new Person("John");
console.log(person.name);  // Using the getter, Outputs: "John"

person.name = "Alice";  // Using the setter
console.log(person.name);  // Outputs: "Alice"

person.name = "";  // Invalid value
// Outputs: "Name can't be empty!"
```

### Key Points:
- The `get` keyword defines a getter method, which is used to retrieve the value of a property.
- The `set` keyword defines a setter method, which is used to update the value of a property.
- Getters and setters are invoked like properties, not methods (i.e., no parentheses when accessing them).

### Example with Data Validation:

Getters and setters are particularly useful for validation, ensuring certain conditions are met before a value is set.

```typescript
class Rectangle {
  private _width: number;
  private _height: number;

  constructor(width: number, height: number) {
    this._width = width;
    this._height = height;
  }

  // Getter for width
  get width(): number {
    return this._width;
  }

  // Setter for width
  set width(value: number) {
    if (value > 0) {
      this._width = value;
    } else {
      console.log("Width must be positive.");
    }
  }

  // Getter for height
  get height(): number {
    return this._height;
  }

  // Setter for height
  set height(value: number) {
    if (value > 0) {
      this._height = value;
    } else {
      console.log("Height must be positive.");
    }
  }

  // Calculate area
  get area(): number {
    return this._width * this._height;
  }
}

const rectangle = new Rectangle(10, 20);
console.log(rectangle.area);  // Outputs: 200

rectangle.width = 15;  // Using the setter to change the width
console.log(rectangle.area);  // Outputs: 300

rectangle.height = -5;  // Invalid height
// Outputs: "Height must be positive."
```

### Explanation:
- The `width` and `height` properties are **private** (`_width`, `_height`), and they can only be accessed through the getter and setter methods.
- The setter methods include validation to ensure that only positive values are accepted.
- The `area` is a **read-only** property (only a getter) that calculates the area based on the width and height.

### Benefits of Getters and Setters:
1. **Encapsulation**: You can keep your class properties private or protected, and expose them only through controlled getter and setter methods.
2. **Validation**: Setters allow you to validate data before setting a property, ensuring that only valid data is assigned.
3. **Computed Properties**: Getters can calculate values dynamically, like the `area` in the example above.
4. **Data Transformation**: Setters can transform or manipulate data before setting the property.

### Summary:
- **Getters** (`get`) allow you to access and possibly compute property values.
- **Setters** (`set`) allow you to validate or modify property values before setting them.
- Getters and setters provide a way to encapsulate and protect class properties while offering controlled access and modification.

#### Static Members

In TypeScript, **static members** (also known as static properties and methods) belong to the class itself rather than to any instance of the class. They are shared among all instances of the class, meaning there is only one copy of a static member, which can be accessed directly on the class rather than on instances.

### Key Points:

1. **Static Properties**:
   - Defined using the `static` keyword.
   - Not accessible through instances of the class, but through the class itself.
   - Useful for constants, utility functions, or any data that is common to all instances.

2. **Static Methods**:
   - Defined using the `static` keyword.
   - Can be called directly on the class, not on instances.
   - Useful for operations or utilities that do not depend on instance-specific data.

### Syntax and Examples

#### Static Properties

```typescript
class MathUtility {
  static PI: number = 3.14159;  // Static property

  static getCircleArea(radius: number): number {
    return MathUtility.PI * radius * radius;  // Access static property in a static method
  }
}

console.log(MathUtility.PI);  // Access static property directly on the class: Outputs: 3.14159
console.log(MathUtility.getCircleArea(5));  // Call static method directly on the class: Outputs: 78.53975
```

In this example, `PI` is a static property, and `getCircleArea` is a static method. Both are accessed directly on the `MathUtility` class.

#### Static Methods

Static methods are typically used for utility functions or factory methods that don't need to access instance-specific data.

```typescript
class Converter {
  static inchesToCentimeters(inches: number): number {
    return inches * 2.54;
  }

  static kilogramsToPounds(kilograms: number): number {
    return kilograms * 2.20462;
  }
}

console.log(Converter.inchesToCentimeters(10));  // Outputs: 25.4
console.log(Converter.kilogramsToPounds(5));     // Outputs: 11.0231
```

In this example, `inchesToCentimeters` and `kilogramsToPounds` are static methods that perform conversions. They can be called directly on the `Converter` class.

### Static vs. Instance Members

- **Static Members**:
  - Belong to the class itself.
  - Accessed via `ClassName.memberName`.
  - Useful for data or functionality that is common to all instances.

- **Instance Members**:
  - Belong to instances of the class.
  - Accessed via `instanceName.memberName`.
  - Useful for data or behavior that is specific to each instance.

#### Example of Static vs. Instance Members

```typescript
class Example {
  static staticProperty: string = "Static";
  instanceProperty: string = "Instance";

  static staticMethod() {
    console.log("Static method called");
  }

  instanceMethod() {
    console.log("Instance method called");
  }
}

console.log(Example.staticProperty);  // Access static property
Example.staticMethod();  // Call static method

const exampleInstance = new Example();
console.log(exampleInstance.instanceProperty);  // Access instance property
exampleInstance.instanceMethod();  // Call instance method

// Static members cannot be accessed through instances
// console.log(exampleInstance.staticProperty);  // Error: Property 'staticProperty' does not exist on type 'Example'
// exampleInstance.staticMethod();  // Error: Property 'staticMethod' does not exist on type 'Example'
```

In this example, `staticProperty` and `staticMethod` are static members of `Example`, while `instanceProperty` and `instanceMethod` are instance members.

### Use Cases for Static Members

1. **Utility Functions**: Functions that perform operations not reliant on instance state, such as mathematical operations or conversions.
2. **Constants**: Values that are shared among all instances and do not change, such as configuration values or fixed constants.
3. **Factory Methods**: Methods that create and return instances of the class, often used to encapsulate complex creation logic.

### Summary

- **Static Properties and Methods** belong to the class and are accessed via `ClassName.memberName`.
- They are useful for functionality that is common to all instances or for utility functions that do not require instance-specific data.
- **Instance Properties and Methods** belong to individual instances of the class and are accessed via `instanceName.memberName`.


## Abstract Classes

In TypeScript, **abstract classes** are a way to define a base class that cannot be instantiated directly but can be extended by other classes. They are useful for defining a common interface or base functionality that derived classes must implement. Abstract classes can contain both fully implemented methods (concrete methods) and methods that must be implemented by derived classes (abstract methods).

### Key Points:

1. **Abstract Methods**:
   - Methods declared with the `abstract` keyword.
   - They do not have an implementation in the abstract class and must be implemented by any non-abstract subclasses.
   
2. **Concrete Methods**:
   - Regular methods that have an implementation in the abstract class.
   - Subclasses can use these methods as-is or override them if needed.

3. **Abstract Properties**:
   - Similar to abstract methods, abstract properties do not have an initializer in the abstract class and must be defined in subclasses.

### Syntax and Examples

#### Defining an Abstract Class

```typescript
abstract class Shape {
  abstract getArea(): number;  // Abstract method

  public describe(): void {
    console.log(`This is a shape with area: ${this.getArea()}`);
  }
}
```

In this example, `Shape` is an abstract class with an abstract method `getArea()` and a concrete method `describe()`.

#### Extending an Abstract Class

```typescript
class Rectangle extends Shape {
  constructor(private width: number, private height: number) {
    super();  // Call the constructor of the abstract base class
  }

  getArea(): number {
    return this.width * this.height;  // Implementing the abstract method
  }
}

class Circle extends Shape {
  constructor(private radius: number) {
    super();  // Call the constructor of the abstract base class
  }

  getArea(): number {
    return Math.PI * this.radius * this.radius;  // Implementing the abstract method
  }
}
```

In this example, `Rectangle` and `Circle` are concrete classes that extend `Shape` and provide implementations for the `getArea` method.

#### Using Abstract Classes

```typescript
const rectangle = new Rectangle(10, 5);
const circle = new Circle(7);

rectangle.describe();  // Outputs: "This is a shape with area: 50"
circle.describe();     // Outputs: "This is a shape with area: 153.93804002589985"

// const shape = new Shape();  // Error: Cannot create an instance of an abstract class
```

### Key Features of Abstract Classes:

1. **Cannot Be Instantiated**: Abstract classes cannot be instantiated directly. They are meant to be extended by other classes.

2. **Common Interface**: Abstract classes provide a common interface and/or base functionality for derived classes. This allows you to define a common set of methods and properties that all derived classes must implement or use.

3. **Partially Implemented**: Abstract classes can have both abstract methods and fully implemented methods. This allows you to provide default behavior that subclasses can either use or override.

4. **Abstract Properties**: You can also define abstract properties in abstract classes, which must be defined in derived classes.

#### Example with Abstract Properties

```typescript
abstract class Animal {
  abstract sound: string;  // Abstract property

  abstract makeSound(): void;  // Abstract method

  public sleep(): void {
    console.log("Zzz...");
  }
}

class Dog extends Animal {
  sound: string = "Bark";  // Implementing the abstract property

  makeSound(): void {
    console.log(this.sound);  // Implementing the abstract method
  }
}

const dog = new Dog();
dog.makeSound();  // Outputs: "Bark"
dog.sleep();      // Outputs: "Zzz..."
```

### Summary

- **Abstract Classes**: Serve as a blueprint for other classes. They cannot be instantiated directly.
- **Abstract Methods**: Methods without implementation that must be implemented in derived classes.
- **Concrete Methods**: Methods with implementation that can be used as-is or overridden in derived classes.
- **Abstract Properties**: Properties without initializers that must be defined in derived classes.

Abstract classes are a powerful tool for enforcing a common interface or base functionality across a hierarchy of classes, making your code more modular and maintainable.
