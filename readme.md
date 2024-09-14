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

##Functions

In TypeScript, functions can accept other functions as parameters, which allows for the implementation of callbacks. Callbacks are a fundamental concept in JavaScript and TypeScript for handling asynchronous operations, events, or passing control between functions. Here’s a detailed overview of how to use callbacks in TypeScript.

### 1. **Basic Callback Function**

A callback function is simply a function passed as an argument to another function and executed after some operation or event.

#### Example:

```typescript
function greet(name: string, callback: (message: string) => void): void {
  const greeting = `Hello, ${name}!`;
  callback(greeting);
}

function logMessage(message: string): void {
  console.log(message);
}

greet('Alice', logMessage);  // Outputs: "Hello, Alice!"
```

In this example:
- `greet` function takes a `name` and a callback function `callback`.
- The `callback` function is invoked with a message after the greeting is created.
- `logMessage` is passed as a callback to `greet`, and it logs the message to the console.

### 2. **Callback with Parameters**

Callbacks can also have parameters that can be passed from the calling function.

#### Example:

```typescript
function processNumbers(a: number, b: number, callback: (result: number) => void): void {
  const sum = a + b;
  callback(sum);
}

processNumbers(5, 3, (result) => {
  console.log(`The sum is ${result}`);  // Outputs: "The sum is 8"
});
```

Here:
- `processNumbers` performs a calculation and passes the result to the callback.
- An inline callback function is used to log the result.

### 3. **Using Callback Types**

You can define a specific type for a callback function to ensure type safety.

#### Example:

```typescript
type Callback = (result: number) => void;

function multiplyNumbers(a: number, b: number, callback: Callback): void {
  const product = a * b;
  callback(product);
}

multiplyNumbers(4, 7, (result) => {
  console.log(`The product is ${result}`);  // Outputs: "The product is 28"
});
```

In this example:
- `Callback` is a type alias for functions that accept a `number` and return `void`.
- `multiplyNumbers` uses this type to ensure that the callback conforms to the expected signature.

### 4. **Async Callbacks**

Callbacks are often used in asynchronous operations, such as reading files or making network requests.

#### Example with Asynchronous Callback:

```typescript
function fetchData(callback: (data: string) => void): void {
  setTimeout(() => {
    const data = 'Fetched data';
    callback(data);
  }, 1000);  // Simulates an async operation with a 1-second delay
}

fetchData((data) => {
  console.log(`Received: ${data}`);  // Outputs: "Received: Fetched data"
});
```

Here:
- `fetchData` simulates an asynchronous operation using `setTimeout`.
- The callback function is called with the fetched data after the delay.

### 5. **Error Handling with Callbacks**

When dealing with asynchronous operations, it's common to handle errors through callbacks.

#### Example:

```typescript
function fetchDataWithErrorHandling(callback: (error: Error | null, data?: string) => void): void {
  setTimeout(() => {
    try {
      const data = 'Fetched data';
      callback(null, data);  // No error
    } catch (error) {
      callback(error as Error);  // Pass the error
    }
  }, 1000);
}

fetchDataWithErrorHandling((error, data) => {
  if (error) {
    console.error(`Error: ${error.message}`);
  } else {
    console.log(`Received: ${data}`);  // Outputs: "Received: Fetched data"
  }
});
```

In this example:
- `fetchDataWithErrorHandling` accepts a callback that handles both errors and data.
- The callback function checks for errors and processes the data accordingly.

### Summary

- **Basic Callback**: Functions passed as arguments and executed within another function.
- **Callback with Parameters**: Callbacks can take arguments, enabling more dynamic behavior.
- **Callback Types**: Define specific types for callbacks to enforce type safety.
- **Async Callbacks**: Useful for handling asynchronous operations with functions like `setTimeout`.
- **Error Handling**: Callbacks can be used to handle errors in asynchronous functions.

Callbacks are a powerful way to manage asynchronous operations and event-driven programming in TypeScript, and understanding how to use them effectively is crucial for writing robust, maintainable code.

## Rest Parameters

In TypeScript, **rest parameters** allow a function to accept an indefinite number of arguments as an array. This feature is useful when you don't know how many arguments will be passed to a function, or you want to handle multiple parameters efficiently.

### Key Points:

1. **Rest Parameters**:
   - Represent an unknown number of arguments.
   - The syntax uses the spread operator (`...`) followed by the parameter name.
   - The rest parameter must be the **last parameter** in the function signature.

2. **Type for Rest Parameters**:
   - The rest parameter can be typed as an array of a specific type (e.g., `number[]`, `string[]`).
   - This ensures that all elements passed in as arguments must conform to that type.

### Syntax

```typescript
function functionName(...paramName: type[]): returnType {
  // Function logic
}
```

### Example: Adding Multiple Numbers

```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((acc, curr) => acc + curr, 0);
}

console.log(sum(1, 2, 3));  // Outputs: 6
console.log(sum(10, 20, 30, 40));  // Outputs: 100
```

- `sum` is a function that accepts any number of `number` arguments.
- The `numbers` parameter is of type `number[]` (an array of numbers).
- Inside the function, the array is processed using `reduce` to compute the sum.

### Example: Rest Parameters with Other Parameters

You can combine regular parameters with rest parameters, but the rest parameter must always come last.

```typescript
function greet(greeting: string, ...names: string[]): string {
  return `${greeting}, ${names.join(', ')}!`;
}

console.log(greet('Hello', 'Alice', 'Bob', 'Charlie'));  // Outputs: "Hello, Alice, Bob, Charlie!"
```

In this example:
- The function `greet` accepts a regular parameter `greeting` and a rest parameter `names`.
- The `names` parameter collects all the additional string arguments into an array.

### Example: Rest Parameters in Callback Functions

Rest parameters can also be useful when working with callbacks, especially in situations where the number of arguments passed to a callback may vary.

```typescript
function executeCallback(callback: (...args: number[]) => void, ...numbers: number[]): void {
  callback(...numbers);
}

executeCallback((...nums) => {
  console.log(`Sum: ${nums.reduce((acc, curr) => acc + curr, 0)}`);
}, 1, 2, 3, 4);  // Outputs: "Sum: 10"
```

In this example:
- `executeCallback` accepts a callback function and a rest parameter `numbers`.
- The rest parameter `numbers` is spread into the callback function using the spread operator `...`.

### Benefits of Using Rest Parameters:

1. **Flexible Argument Length**: You can write functions that work with any number of arguments.
2. **Cleaner Code**: Reduces the need for overloading or checking the number of arguments manually.
3. **Works with Arrays**: The rest parameter is naturally an array, so you can use array methods like `map`, `filter`, `reduce`, etc.

### Example: Rest Parameters with Default Parameters

You can also combine rest parameters with default parameters, though the default parameter must come before the rest parameter.

```typescript
function createList(item: string = 'Item', ...otherItems: string[]): string[] {
  return [item, ...otherItems];
}

console.log(createList());  // Outputs: ["Item"]
console.log(createList('Apple', 'Banana', 'Cherry'));  // Outputs: ["Apple", "Banana", "Cherry"]
```

In this example:
- `item` has a default value, and `otherItems` is a rest parameter that collects the remaining arguments.

### Summary

- **Rest Parameters** allow functions to accept an indefinite number of arguments as an array.
- They are defined with the syntax `...paramName: type[]`, where `paramName` is the rest parameter and `type[]` is the array type.
- Rest parameters must always be the last parameter in the function signature.
- They are useful for handling varying numbers of arguments in a clean and efficient way.

## Method Overloading

In TypeScript, **function overloading** allows you to define multiple function signatures for a single function, enabling it to handle different types or numbers of arguments. While TypeScript doesn't allow true runtime function overloading (like some other languages such as Java or C++), it uses a feature called "overload signatures" to simulate this behavior at compile time.

### Key Points:

1. **Overload Signatures**: You can define multiple signatures for a function, specifying the different combinations of parameters and return types the function can accept.
2. **Implementation**: The actual function implementation must handle all the variations of the overloads.
3. **Type Safety**: TypeScript enforces type safety by checking the arguments passed to the overloaded function against the defined signatures.

### Syntax

```typescript
function functionName(param1: type1): returnType;
function functionName(param1: type1, param2: type2): returnType;
// ...additional signatures...
function functionName(param1: type1, param2?: type2): returnType {
  // Function implementation
}
```

### Example: Overloading Based on Number of Parameters

```typescript
function add(a: number, b: number): number;          // Overload 1
function add(a: string, b: string): string;          // Overload 2
function add(a: number, b: number, c: number): number; // Overload 3

// Function implementation
function add(a: any, b: any, c?: any): any {
  if (typeof a === "number" && typeof b === "number" && typeof c === "number") {
    return a + b + c;  // Handling three numbers
  } else if (typeof a === "number" && typeof b === "number") {
    return a + b;  // Handling two numbers
  } else if (typeof a === "string" && typeof b === "string") {
    return a + b;  // Handling two strings (concatenation)
  }
}

console.log(add(1, 2));           // Outputs: 3 (number)
console.log(add(1, 2, 3));        // Outputs: 6 (number)
console.log(add("Hello, ", "World!"));  // Outputs: "Hello, World!" (string)
```

### Explanation:

- **Overload Signatures**:
  - The function `add` is overloaded to handle three cases: adding two numbers, concatenating two strings, or adding three numbers.
  
- **Implementation**:
  - The actual `add` function checks the types of the arguments and handles each case accordingly.
  - The `c?` parameter is optional (`undefined` when only two arguments are passed).

### Example: Overloading with Different Return Types

You can also use overloads to define different return types based on the parameters passed.

```typescript
function reverse(value: string): string;   // Overload 1
function reverse(value: number[]): number[]; // Overload 2

// Function implementation
function reverse(value: string | number[]): string | number[] {
  if (typeof value === "string") {
    return value.split("").reverse().join("");  // Reverse the string
  } else {
    return value.slice().reverse();  // Reverse the array of numbers
  }
}

console.log(reverse("TypeScript"));  // Outputs: "tpircSepyT"
console.log(reverse([1, 2, 3, 4]));  // Outputs: [4, 3, 2, 1]
```

### Explanation:

- **Overload Signatures**:
  - The `reverse` function has two overloads: one for reversing a string and one for reversing an array of numbers.
  
- **Implementation**:
  - The function handles both strings and arrays, returning the appropriate type (`string` or `number[]`).

### Example: Overloading with Optional Parameters

You can combine function overloading with optional parameters to handle cases where not all parameters are always passed.

```typescript
function greet(name: string): string;                 // Overload 1
function greet(name: string, greeting: string): string; // Overload 2

// Function implementation
function greet(name: string, greeting?: string): string {
  if (greeting) {
    return `${greeting}, ${name}!`;
  } else {
    return `Hello, ${name}!`;
  }
}

console.log(greet("Alice"));              // Outputs: "Hello, Alice!"
console.log(greet("Alice", "Good morning")); // Outputs: "Good morning, Alice!"
```

### Explanation:

- **Overload Signatures**:
  - There are two overloads: one that accepts only a name, and one that accepts both a name and a custom greeting.
  
- **Optional Parameter**:
  - The `greeting` parameter is optional (`?`), and the function behaves differently based on whether it is provided.

### Rules for Overloading:

1. **Multiple Overload Signatures**: You can define multiple overload signatures for a single function.
2. **Implementation**: The actual function implementation should be a single function that can handle all overloads.
3. **Argument Matching**: TypeScript will match the function call with the correct overload based on the number and type of arguments.
4. **Return Type**: The return type of the overloads must be consistent with the function implementation. TypeScript checks that the implementation satisfies the declared overloads.

### Example: Handling Different Parameter Types

You can overload functions to accept different types of arguments, and handle them accordingly.

```typescript
function format(value: string): string;            // Overload 1
function format(value: number): string;            // Overload 2

// Function implementation
function format(value: string | number): string {
  if (typeof value === "string") {
    return value.toUpperCase();  // Handle string
  } else {
    return value.toFixed(2);     // Handle number, formatting to 2 decimal places
  }
}

console.log(format("hello"));   // Outputs: "HELLO"
console.log(format(123.456));   // Outputs: "123.46"
```

### Summary

- **Function Overloading** in TypeScript allows defining multiple signatures for a single function.
- You can overload based on the number of parameters, their types, or both.
- The function implementation must handle all the overload signatures, and TypeScript ensures type safety based on the overloads.
- Overloading provides flexibility while maintaining strict type-checking, enabling more robust code.


# Generics

Generics in TypeScript provide a way to create reusable components that work with a variety of data types, while maintaining type safety. They allow you to define functions, classes, and interfaces that can operate on different types without losing the benefits of strong typing.

### Why Use Generics?
Generics allow for:
1. **Type Safety:** They ensure that the data types being passed into functions, classes, or interfaces are consistent and correct.
2. **Code Reusability:** The same function or class can handle multiple types, avoiding the need to rewrite code for different types.

### Syntax
The typical syntax for a generic in TypeScript involves using angle brackets (`<>`) with a type variable (e.g., `T`).

### Example 1: Generic Function

A simple generic function to return the input value can look like this:

```typescript
function identity<T>(value: T): T {
    return value;
}

let stringResult = identity<string>("Hello");
let numberResult = identity<number>(42);
```

Here, `T` is a placeholder for the type, which will be inferred or explicitly provided when the function is called.

### Example 2: Generic Classes

Generics are also useful in classes. For example, a generic `Box` class can store and retrieve any type of data:

```typescript
class Box<T> {
    private content: T;

    constructor(value: T) {
        this.content = value;
    }

    getContent(): T {
        return this.content;
    }
}

let stringBox = new Box<string>("Hello");
let numberBox = new Box<number>(123);
```

### Example 3: Generic Interfaces

You can define interfaces that work with generics as well:

```typescript
interface Pair<K, V> {
    key: K;
    value: V;
}

let pair: Pair<string, number> = { key: "age", value: 30 };
```

### Example 4: Generic Constraints

You can constrain generics to specific types, ensuring that the types passed meet certain criteria. For example, if you want a function that works only with objects that have a `length` property:

```typescript
function logLength<T extends { length: number }>(value: T): void {
    console.log(value.length);
}

logLength("Hello"); // Works because string has a length
logLength([1, 2, 3]); // Works because array has a length
```

### Conclusion

Generics provide flexibility and reusability, allowing TypeScript code to be more adaptable while still enforcing strict typing.

# Problems with Generics and String

If you're encountering issues with generics while returning strings in TypeScript, it could stem from how the type is inferred or enforced by the generic. When you return a string but use a generic type, TypeScript expects the return type to match the generic parameter, which can cause a mismatch if you're not handling types correctly.

Let's break down a few common scenarios where this issue can occur:

### Scenario 1: Mismatched Return Type

Suppose you define a generic function but always return a string regardless of the input type. This will cause a type mismatch because the return type must match the generic type.

```typescript
function getValue<T>(value: T): T {
    return "This is a string"; // Error: Type 'string' is not assignable to type 'T'
}
```

### Solution:
You need to ensure that the return type is of the generic type `T`. If you want the function to always return a string regardless of the generic type, then you shouldn’t use a generic type for the return value.

#### Option 1: Remove the Generic and Return a String
If you always want to return a string, you don’t need a generic:

```typescript
function getValue(value: any): string {
    return "This is a string";
}
```

#### Option 2: Use a Generic with a Specific Return Type
If you need the flexibility of generics but also want to ensure that a string is returned in some cases, you can restrict the generic type or use conditional logic:

```typescript
function getValue<T>(value: T): T | string {
    if (typeof value === "string") {
        return value; // Return the input if it's a string
    } else {
        return "This is a string"; // Otherwise, return a default string
    }
}
```

### Scenario 2: Generic Function Returning a Fixed String

If your function is supposed to handle multiple types but return a fixed string regardless of the input type, TypeScript will complain because it expects the return type to match the generic type.

For example:

```typescript
function processValue<T>(value: T): T {
    return "Processed"; // Error: Type 'string' is not assignable to type 'T'
}
```

### Solution:
If your function must return a string regardless of the input type but you still want to accept different types, you can declare the return type as `string` explicitly:

```typescript
function processValue<T>(value: T): string {
    return "Processed";
}
```

Alternatively, if the return type must depend on the input type (while handling the string case), you could do something like this:

```typescript
function processValue<T>(value: T): T | string {
    if (typeof value === "string") {
        return `Processed: ${value}`;
    }
    return "Processed"; // Fallback to a string for other types
}
```

### Scenario 3: Returning a Specific Property of a String

If you are dealing with objects that could be strings and trying to access a property that only exists on strings, you need to narrow the type.

Example:

```typescript
function getLength<T>(value: T): number {
    return value.length; // Error: Property 'length' does not exist on type 'T'
}
```

### Solution:
You can constrain the generic to ensure that the type has a `length` property (like a string or an array):

```typescript
function getLength<T extends { length: number }>(value: T): number {
    return value.length;
}
```

### Conclusion

Generics are useful for maintaining flexibility, but they come with the responsibility of ensuring type consistency. If you are always returning a string but using generics, make sure you handle the return type properly, either by explicitly returning a `string` or by using conditional logic to satisfy TypeScript's type-checking system.

# TypeCasting and Type Assertion

Type assertion and type casting in TypeScript are used to tell the TypeScript compiler what the intended type of a variable or expression should be. While similar, they serve slightly different purposes and are syntactically distinct. Both allow you to override TypeScript's inferred types in cases where you are certain of the type, but the compiler isn't.

### 1. **Type Assertion**

Type assertion is used when you know the actual type of a variable more accurately than TypeScript. It's a way to tell the compiler to treat a variable as a certain type, overriding its inferred type. Type assertion doesn't change the actual data type at runtime; it only affects the static type checking during development.

There are two syntaxes for type assertions:
- **Angle bracket syntax**: `<Type>value`
- **`as` syntax**: `value as Type`

#### Example 1: Using `as` Syntax

```typescript
let someValue: unknown = "This is a string";
let stringLength: number = (someValue as string).length;
```

Here, `someValue` is of type `unknown` (it could be anything). By asserting `someValue` as a `string`, we can safely access its `length` property.

#### Example 2: Using Angle Brackets

```typescript
let anotherValue: unknown = "Another string";
let anotherLength: number = (<string>anotherValue).length;
```

Both the `as` syntax and the angle bracket syntax achieve the same result.

#### Important Notes:
- **Type assertion only works in TypeScript.** At runtime, this has no effect on the underlying value.
- **Use cases**: Type assertions are useful when interfacing with third-party libraries or APIs that return generic or ambiguous types such as `unknown`, `any`, or JSON data.
- **You can't cast to unrelated types**: For example, you can't directly cast a string to a number unless you're absolutely certain of how to handle the conversion.

### 2. **Type Casting**

TypeScript does not have "type casting" in the same way as languages like C++ or Java. Instead, type assertion can sometimes be referred to as "casting" since it forces the TypeScript compiler to treat a variable as another type.

If you come from languages with casting, it's worth noting that TypeScript's type assertion is a development-time feature, while casting in languages like C++ or Java actually transforms one data type into another at runtime.

### Example of Type Assertion (often called casting):

```typescript
let someValue: unknown = "1234";
let numericValue: number = parseInt(someValue as string, 10);  // "Casting" string to number using parseInt
```

In this case, while the `parseInt` function converts the string into a number, the type assertion tells the compiler that `someValue` is a string so that we can pass it to `parseInt`.

### 3. **Difference Between Type Assertion and Type Casting**

- **Type Assertion (in TypeScript)**: 
  - This is purely a compile-time construct. It doesn't change the type at runtime. Instead, it instructs the TypeScript compiler to override its inferred type, but the value itself remains unchanged.
  
- **Type Casting (in other languages)**:
  - This changes the type of a value at runtime, usually involving actual transformation of data (e.g., casting a floating-point number to an integer).

### Type Assertion with DOM Elements

Type assertion is often used when interacting with the DOM, where TypeScript doesn’t know the exact type of an element.

```typescript
let inputElement = document.getElementById("userInput") as HTMLInputElement;
inputElement.value = "Hello, world!";
```

Here, `document.getElementById` returns an `HTMLElement | null`, but we assert that the element is specifically an `HTMLInputElement` so we can safely access its `value` property.

### Type Assertion and Union Types

If a variable has a union type (e.g., `string | number`), you can use type assertion to treat the variable as one of the possible types.

```typescript
function formatValue(value: string | number) {
    if ((value as string).toUpperCase) {
        return (value as string).toUpperCase();  // Treating 'value' as a string
    }
    return value.toString();  // Otherwise treating it as a number
}
```

### Conclusion

- **Type Assertion**: Instructs TypeScript to treat a value as a certain type, useful for narrowing down ambiguous types (`any`, `unknown`, or union types).
- **Type Casting** (in TypeScript, through type assertions): No runtime transformation, only type checking during compile time.

# Type Guards  and TypeScript Utility Types

### **Type Guards in TypeScript**

Type guards in TypeScript are functions or expressions that allow you to **narrow down the type** of a variable within a conditional block. TypeScript uses these guards to ensure type safety by understanding the specific type of a value during runtime.

#### **Common Type Guards**

1. **`typeof` Operator:**
   The `typeof` operator is commonly used to narrow down types to primitive types like `string`, `number`, `boolean`, `symbol`, and `function`.

   ```typescript
   function printValue(value: string | number) {
       if (typeof value === "string") {
           console.log("String:", value.toUpperCase());  // Now TypeScript knows it's a string
       } else {
           console.log("Number:", value.toFixed(2));    // Here, it's narrowed to a number
       }
   }
   ```

2. **`instanceof` Operator:**
   The `instanceof` operator checks whether an object is an instance of a particular class or constructor function.

   ```typescript
   class Dog {
       bark() {
           console.log("Woof!");
       }
   }

   class Cat {
       meow() {
           console.log("Meow!");
       }
   }

   function animalSound(animal: Dog | Cat) {
       if (animal instanceof Dog) {
           animal.bark(); // Dog methods are available here
       } else {
           animal.meow(); // Cat methods are available here
       }
   }
   ```

3. **`in` Operator:**
   The `in` operator checks if an object has a particular property, which can be useful when working with objects that have different shapes.

   ```typescript
   interface Car {
       drive(): void;
   }

   interface Boat {
       sail(): void;
   }

   function operateVehicle(vehicle: Car | Boat) {
       if ("drive" in vehicle) {
           vehicle.drive(); // TypeScript knows it's a Car
       } else {
           vehicle.sail();  // TypeScript knows it's a Boat
       }
   }
   ```

4. **Custom Type Guards:**
   You can define your own type guards using functions that return `value is Type`. This allows you to create specific checks for complex types.

   ```typescript
   interface Fish {
       swim(): void;
   }

   interface Bird {
       fly(): void;
   }

   function isFish(animal: Fish | Bird): animal is Fish {
       return (animal as Fish).swim !== undefined;
   }

   function moveAnimal(animal: Fish | Bird) {
       if (isFish(animal)) {
           animal.swim();  // TypeScript knows it's a Fish
       } else {
           animal.fly();   // TypeScript knows it's a Bird
       }
   }
   ```

### **TypeScript Utility Types**

TypeScript provides a set of built-in utility types that make it easier to manipulate types, especially in complex cases where we want to extract, modify, or combine existing types.

#### **Common Utility Types**

1. **`Partial<Type>`**
   Constructs a type that makes all properties of `Type` optional.

   ```typescript
   interface User {
       id: number;
       name: string;
       email: string;
   }

   const updateUser = (user: Partial<User>) => {
       // Now all properties are optional
       if (user.name) {
           console.log(`Updating user name to: ${user.name}`);
       }
   };

   updateUser({ name: "Alice" });
   ```

2. **`Required<Type>`**
   Constructs a type that makes all properties of `Type` required.

   ```typescript
   interface User {
       id?: number;
       name?: string;
   }

   const fullUser: Required<User> = {
       id: 1,
       name: "Alice"
   };
   ```

3. **`Readonly<Type>`**
   Constructs a type where all properties of `Type` are read-only, meaning they cannot be reassigned.

   ```typescript
   interface Car {
       make: string;
       model: string;
   }

   const car: Readonly<Car> = {
       make: "Toyota",
       model: "Corolla"
   };

   // car.make = "Honda";  // Error: cannot reassign to a read-only property
   ```

4. **`Record<Keys, Type>`**
   Constructs an object type where the keys are from a union type `Keys` and the values are of type `Type`.

   ```typescript
   type Status = "success" | "error" | "loading";
   const statuses: Record<Status, string> = {
       success: "Operation was successful",
       error: "There was an error",
       loading: "Loading, please wait..."
   };
   ```

5. **`Pick<Type, Keys>`**
   Constructs a type by picking a set of properties from `Type`.

   ```typescript
   interface User {
       id: number;
       name: string;
       email: string;
       age: number;
   }

   type UserPreview = Pick<User, "id" | "name">;

   const user: UserPreview = {
       id: 1,
       name: "Alice"
   };
   ```

6. **`Omit<Type, Keys>`**
   Constructs a type by omitting a set of properties from `Type`.

   ```typescript
   interface User {
       id: number;
       name: string;
       email: string;
       age: number;
   }

   type UserWithoutEmail = Omit<User, "email">;

   const user: UserWithoutEmail = {
       id: 1,
       name: "Alice",
       age: 25
   };
   ```

7. **`Exclude<Type, ExcludedUnion>`**
   Constructs a type by excluding from `Type` all union members that are assignable to `ExcludedUnion`.

   ```typescript
   type MyUnion = "a" | "b" | "c";
   type ExcludedUnion = Exclude<MyUnion, "a">;  // "b" | "c"
   ```

8. **`Extract<Type, Union>`**
   Constructs a type by extracting from `Type` all union members that are assignable to `Union`.

   ```typescript
   type MyUnion = "a" | "b" | "c";
   type ExtractedUnion = Extract<MyUnion, "a" | "b">;  // "a" | "b"
   ```

9. **`NonNullable<Type>`**
   Constructs a type by excluding `null` and `undefined` from `Type`.

   ```typescript
   type NullableType = string | null | undefined;
   type NonNullableType = NonNullable<NullableType>;  // string
   ```

10. **`ReturnType<Type>`**
    Constructs a type consisting of the return type of a function `Type`.

    ```typescript
    function getUser() {
        return { id: 1, name: "Alice" };
    }

    type UserType = ReturnType<typeof getUser>;  // { id: number, name: string }
    ```

11. **`Parameters<Type>`**
    Constructs a tuple type from the types used in the parameters of a function `Type`.

    ```typescript
    function login(username: string, password: string) {
        // login logic
    }

    type LoginParams = Parameters<typeof login>;  // [string, string]
    ```

### **Conclusion**

- **Type Guards** in TypeScript are used to narrow down the type of a variable at runtime, ensuring the compiler knows what type a variable is at any point.
- **Utility Types** in TypeScript help transform, manipulate, and create new types from existing ones, improving code reusability and ensuring more precise type definitions.
