# Learn-Typescript

## Getting Started

#### What is typescript?
It adds type to JavaScript, as JavaScript is dyamically typed language it helps to check type during compile time.

#### Typescript setup
Node modules required.
```sh
npm install -g typescript
tsc --v

npm install -g ts-node
-> To run typescript file directly
```

#### Typescript Hello World!

let message: string = 'Hello, World!';
console.log(message);
```sh
--> tsc app.ts
--> node app.js

or
--> ts-node app.ts
```

#### Create the project structure
First, create a new directory called `nodets`. Directory name you can decide.
Second, create two sub-directories under the `nodets` called `build` and `src`.
You’ll store the TypeScript code in the `src` directory.
Once the TypeScript compiler compiles the source TypeScript files, it will store the output files in the `build` directory.

##### Configure the TypeScript compiler
Run the following command in the `nodets` directory to create the `tsconfig.json` file:
```sh
tsc --init
```
You’ll see the `tsconfig.json` created under the nodets directory:

Now, you can open the `tsconfig.json` file. There are many options. In this tutorial, you’ll focus on these two options:
- `rootdir` – specifies the root directory of the TypeScript input files.
- `outdir`-stores the JavaScript output files.

These options are commented by default. And you’ll need to uncomment ( remove the `//` at the beginning of the line) and change them as follows:

For the `outDir` option:
```sh
"outDir": "./build"
```
And for the `rootDir` option:
```sh
"rootDir": "./src"
```
To verify the new configuration, you can create a new file called app.ts under the ./src directory and place the following code:

```sh
console.log('Node.js TypeScript');
```
And then run the following command to execute the TypeScript compiler. It’ll compile all the files stored in the `src` directory:
```sh
tsc
```
If the configuration is correct, you’ll see the `app.js` generated under the `./build` directory:

To run the app.js, you navigate to the build directory and execute the following command:
```sh
node app.js
```

This is time-consuming.

Luckly, you can automate the whole process using some Node.js modules.

##### Install Node.js modules
The `nodemon` module allows you to automatically restart the application when you change the JavaScript source code.

The `concurrently` module runs multiple commands concurrently.

First, execute the `npm init` command from the root directory of the project:

```sh
npm init --yes
```
Next, install the `nodemon` and `concurrently` module:
```sh
npm install --g nodemon concurrently
```
Open `package.json` file and change the scripts option to the following:
```sh
"scripts": {
    "start:build": "tsc -w",
    "start:run": "nodemon build/app.js",
    "start": "concurrently npm:start:*"
}
```

This `"start:build": "tsc -w"` will watch for the changes in the `./src` directory and compile them automatically.

This `"start:run": "nodemon build/app.js"` will automatically run the `app.js` in the `./build` directory whenever the new file is generated.

This `"start": "concurrently npm:start:*"` runs all the commands that start with `npm:start:*`, which executes both `start:build` and `start:run` commands above.

Also change main from 
```sh
"main": "index.js"
```
to
```sh
"main": "app.js"
```

Finally, execute the following command:
```sh
npm start
```
To verify the configuration, you change some code in the `app.ts`. And you’ll see the output in the console.


#### Why typescript?

-> TypeScript adds a type system to help you avoid many problems with dynamic types in JavaScript.
-> TypeScript implements the future features of JavaScript a.k.a ES Next so that you can use them today.

```sh
let box;
console.log(typeof(box)); // undefined
box = "Hello";
console.log(typeof(box)); // string
box = 100;
console.log(typeof(box)); // number
```

#### Basic Types

The basic types are same as JavaScript.
##### Primitive types
The following illustrates the primitive types in TypeScript:

|Name | Description|
| ------ | ------ |
|string  |represents text data|
|number | represents numeric values|
|boolean |  has true and false values|
|null | has one value: null |
| undefined | has one value: undefined. It is a default value of an uninitialized variable|
|symbol | represents a unique constant value|

#### Object types
Objec types are functions, arrays, classes, etc. You can create custom objects as well.

#### Type Annotation
TypeScript uses the syntax : type after an identifier as the type annotation, where type can be any valid type.
```sh
let variableName: type;
let variableName: type = value;
const constantName: type = value;
```

```sh
let name: string = 'John';
let age: number = 25;
let active: boolean = true;
```

#### Arrays
To annotate an array type you use use a specific type followed by a square bracket : type[]
```sh
let arrayName: type[];
let names: string[] = ['John', 'Jane', 'Peter', 'David', 'Mary'];
```

#### Object Type
To specify a type for an object, you use the object type annotation.
```sh
let person: {
   name: string;
   age: number
};

person = {
   name: 'John',
   age: 25
}; // valid

OR

 let person: {
   name: string;
   age: number
} = {
   name: 'John',
   age: 25
}; // valid
```

#### Function arguments & return types
How to give types for a function declaration.
```sh
let greeting : (name: string) => string;
greeting = function (name: string) {
    return `Hi ${name}`;
};

// This will cauase error
greeting = function () {
    console.log('Hello');
};
```

#### Type Inference
Type inference describes where and how TypeScript infers types when you don't explicitly annotate them.
```sh
let counter = 0;
// The above line is equivalent to
let counter: number = 0; // implicit type infer by Typescript

function increment(counter: number) {
    return counter++;
}
// It's return type is implicitely infered by Typescript based on return
function increment(counter: number) : number {
    return counter++;
}
```

#### Common types
There are common types in typescript.
```sh
Number Type
String Type
Boolean Type
Object Type
Array Type
```

##### Typle Type
A tuple works like an array with some additional considerations:
- The number of elements in the tuple is fixed.
- The types of elements are known, and need not be the same.
```sh
let skill: [string, number];
skill = ['Programming', 5];

// Below code will throw error as order of values is important
let skill: [string, number];
skill = [5, 'Programming'];
```

##### Enum Type
An enum is a group of named constant values. Enum stands for enumerated type.
```sh
enum name {constant1, constant2, ...};
enum Month {
    Jan,
    Feb,
    Mar,
    Apr,
    May,
    Jun,
    Jul,
    Aug,
    Sep,
    Oct,
    Nov,
    Dec
};

function isItSummer(month: Month) {
    let isSummer: boolean;
    switch (month) {
        case Month.Jun:
        case Month.Jul:
        case Month.Aug:
            isSummer = true;
            break;
        default:
            isSummer = false;
            break;
    }
    return isSummer;
}

console.log(isItSummer(Month.Jun)); // true
// This also works fine
console.log(isItSummer(6)); // true

// JavaScript code generated for enum
var Month;
(function (Month) {
    Month[Month["Jan"] = 0] = "Jan";
    Month[Month["Feb"] = 1] = "Feb";
    Month[Month["Mar"] = 2] = "Mar";
    Month[Month["Apr"] = 3] = "Apr";
    Month[Month["May"] = 4] = "May";
    Month[Month["Jun"] = 5] = "Jun";
    Month[Month["Jul"] = 6] = "Jul";
    Month[Month["Aug"] = 7] = "Aug";
    Month[Month["Sep"] = 8] = "Sep";
    Month[Month["Oct"] = 9] = "Oct";
    Month[Month["Nov"] = 10] = "Nov";
    Month[Month["Dec"] = 11] = "Dec";
})(Month || (Month = {}));
```

##### Any Type
Sometimes, you may need to store a value in a variable. But you don't know its type at the time of writing the program. And the unknown value may come from a third party API or user input.

```sh
let result: any;
result = 10.123;
console.log(result.toFixed());
result.willExist(); //

In this example, the TypeScript compiler doesn't issue any warning even the willExist() method doesn't exist at compile time because the willExist() method might available at runtime.
```

##### Void Type
The void type denotes the absence of having any type at all. It is a little like the opposite of the any type.
```sh
function log(message): void {
    console.log(messsage);
}
```
##### Never Type
The never type is a type that contains no values. Because of this, you cannot assign any value to a variable with a never type.
Typically, you use the never type to represent the return type of a function that always throws an error. For example:
```sh
function raiseError(message: string): never {
    throw new Error(message);
}

// The return type of the following function is inferred to the never type:
function reject() {
   return raiseError('Rejected');
}

// If you have a function expression that contains an indefinite loop, its return type is also the never type. For example:
let loop = function forever() {
    while (true) {
        console.log('Hello');
    }
}
```

##### Union Type
Union type is useful when you run into a function that expects a parameter that is either a number or a string.
```sh
let result: number | string;
result = 10; // OK
result = 'Hi'; // also OK
result = false; // a boolean value, not OK
```

##### Type aliases
It allows you to create a new name for an existing type.
```sh
type alias = existingType;

type chars = string;
let messsage: chars; // same as string type

type alphanumeric = string | number;
let input: alphanumeric;
input = 100; // valid
input = 'Hi'; // valid
input = false; // Compiler error
```

##### String literal type
The string literal types allow you to define a type that accepts only one specified string literal.
```sh
let click: 'click';
click = 'click'; // valid
click = 'dblclick'; // compiler error

let mouseEvent: 'click' | 'dblclick' | 'mouseup' | 'mousedown';
mouseEvent = 'click'; // valid
mouseEvent = 'dblclick'; // valid
mouseEvent = 'mouseup'; // valid
mouseEvent = 'mousedown'; // valid
mouseEvent = 'mouseover'; // compiler error
```

#### CONTROL FLOW STATEMENTS
- if else
- switch case
- for
- while
- do while
- break
- continue

#### Functions
TypeScript functions are the building blocks of readable, maintainable, and reusable code.
```sh
function name(parameter: type, parameter:type,...): returnType {
   // do something
}
function add(a: number, b: number): number {
    return a + b;
}
```

##### Function Types
It decides the return type of function
```sh
let add: (a: number, b: number) => number =
function (x: number, y: number) {
    return x + y;
};

add = function (x: string, y: string): number {
    return x.concat(y).length;
};
```

##### Optional Parameters
To make a function parameter optional, you use the ? after the parameter name. For example:
```sh
function multiply(a: number, b: number, c?: number): number {
    if (typeof c !== 'undefined') {
        return a * b * c;
    }
    return a * b;
}
```

##### Default Parameters
TypeScript default parameters for functions.
```sh
function applyDiscount(price, discount = 0.05) {
    return price * (1 - discount);
}
console.log(applyDiscount(100)); // 95
```

##### Rest Parameters
A rest parameter allows you a function to accept zero or more arguments of the specified type.
- A function has only one rest parameter.
- The rest parameter appears last in the parameter list.
- The type of the rest parameter is an array type.

```sh
function getTotal(...numbers: number[]): number {
    let total = 0;
    numbers.forEach((num) => total += num);
    return total;
}

console.log(getTotal()); // 0
console.log(getTotal(10, 20)); // 30
console.log(getTotal(10, 20, 30)); // 60
```

##### Function overloadings
Function overloadings allow you to establish the relationship between the parameter types and result types of function.

Let's start with some simple functions:
```sh
function addNumbers(a: number, b: number): number {
    return a + b;
}

function addStrings(a: string, b: string): string {
    return a + b;
}
```
- The addNumbers() function returns the sum of two numbers.
- The addStrings() function returns the concatenation of two strings.

It's possible to use a union type to define a range of types for function parameters and results:
```sh
function add(a: number | string, b: number | string): number | string {
    if (typeof a === 'number' && typeof b === 'number')
        return a + b;

    if (typeof a === 'string' && typeof b === 'string')
        return a + b;
}
```
However, the union type doesn't express the relationship between the parameter types and results accurately.

To better describe the relationships between the types used by a function, TypeScript supports function overloadings. For example:
```sh
function add(a: number, b: number): number;
function add(a: string, b: string): string;
function add(a: any, b: any): any {
   return a + b;
}
```
###### Method overloading
When a function is a property of a class, it is called a method. TypeScript also supports method overloading. For example:
```sh
class Counter {
    private current: number = 0;
    count(): number;
    count(target: number): number[];
    count(target?: number): number | number[] {
        if (target) {
            let values = [];
            for (let start = this.current; start <= target; start++) {
                values.push(start);
            }
            this.current = target;
            return values;
        }
        return ++this.current;
    }
}

The count() function can return a number or an array depending on the number of argument that you pass into it:
let counter = new Counter();
console.log(counter.count()); // return a number
console.log(counter.count(20)); // return an array
```

#### TypeScript Class
JavaScript does not have a concept of class like other programming languages such as Java and C#. In ES5, you can use a constructor function and prototype inheritance to create a "class"
```sh
class Person {
    ssn: string;
    firstName: string;
    lastName: string;

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```

#### Access Modifiers
TypeScript provides three access modifiers:
- private
- protected
- public

##### Private Modifier
The private modifier limits the visibility to the same-class only. When you add the private modifier to a property or method, you can access that property or method within the same class.
```sh
class Person {
    private ssn: string;
    private firstName: string;
    private lastName: string;

    constructor(ssn: string, firstName: string, lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}

let person = new Person('153-07-3130', 'John', 'Doe');
console.log(person.ssn); // compile error
```

##### Public modifier
The public modifier allows class properties and methods to be accessible from all locations. If you don't specify any access modifier for properties and methods, they will take the public modifier by default.

```sh
class Person {
    // ...
    public getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
    // ...
}
```
##### Protected modifier
The protected modifier allows properties and methods of a class to be accessible within same class and within subclasses.
```sh
class Person {
    constructor(protected ssn: string, private firstName: string, private lastName: string) {
        this.ssn = ssn;
        this.firstName = firstName;
        this.lastName = lastName;
    }

    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
}
```

#### TypeScript readonly
TypeScript provides the readonly modifier that allows you to mark the properties of a class immutable. The assignment to a readonly property can only occur in one of two places:
- In the property declaration.
- In the constructor of the same class.

```sh
class Person {
    readonly birthDate: Date;

    constructor(birthDate: Date) {
        this.birthDate = birthDate;
    }
}

let person = new Person(new Date(1990, 12, 25));
person.birthDate = new Date(1991, 12, 25); // Compile error
```

#### TypeScript Getters and Setters
To get and set properties of a class.
For each property:
- A getter method returns the value of the property's value. A getter is also called an accessor.
- A setter method updates the property's value. A setter is also known as a mutator.

A getter method starts with the keyword get and a setter method starts with the keyword set
```sh
class Person {
    private _age: number;
    private _firstName: string;
    private _lastName: string;


    public get age() {
        return this._age;
    }

    public set age(theAge: number) {
        if (theAge <= 0 || theAge >= 200) {
            throw new Error('The age is invalid');
        }
        this._age = theAge;
    }

    public getFullName(): string {
        return `${this._firstName} ${this._lastName}`;
    }
}

let person = new Person();
person.age = 10;
```

How it works?
- First, change the access modifiers of the age, firstName, and lastName properties from public to private.
- Second, change the property age to _age.

#### TypeScript Inheritance
A class can reuse the properties and methods of another class. This is called inheritance in TypeScript.
```sh
class Person {
    constructor(private firstName: string, private lastName: string) {
        this.firstName = firstName;
        this.lastName = lastName;
    }
    getFullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
    describe(): string {
        return `This is ${this.firstName} ${this.lastName}.`;
    }
}

// Iheritance
class Employee extends Person {
    constructor(
        firstName: string,
        lastName: string,
        private jobTitle: string) {

        // call the constructor of the Person class:
        super(firstName, lastName);
    }
}

let employee = new Employee('John','Doe','Front-end Developer');
console.log(employee.getFullName());
console.log(employee.describe());
```

##### Method overriding
If you want the Employee class has its own version of the describe() method, you can define it in the Employee class like this:
Employee class ovrridig the describe method of person class.
```sh
class Employee extends Person {
    constructor(
        firstName: string,
        lastName: string,
        private jobTitle: string) {

        super(firstName, lastName);
    }

    describe(): string {
        return super.describe() + `I'm a ${this.jobTitle}.`;
    }
}
```

##### Static Methods and Properties
Unlike an instance property, a static property is shared among all instances of a class.

Static Property
```sh
class Employee {
    static headcount: number = 0;

    constructor(
        private firstName: string,
        private lastName: string,
        private jobTitle: string) {

        Employee.headcount++;
    }
}

let john = new Employee('John', 'Doe', 'Front-end Developer');
let jane = new Employee('Jane', 'Doe', 'Back-end Developer');

console.log(Employee.headcount); // 2
```

Static Method
```sh
class Employee {
    private static headcount: number = 0;

    constructor(
        private firstName: string,
        private lastName: string,
        private jobTitle: string) {

        Employee.headcount++;
    }

    public static getHeadcount() {
        return Employee.headcount;
    }
}

let john = new Employee('John', 'Doe', 'Front-end Developer');
let jane = new Employee('Jane', 'Doe', 'Back-end Developer');
console.log(Employee.getHeadcount); // 2
```

#### Abstract Classes
An abstract class is typically used to define common behaviors for derived classes to extend.
An abstract method does not contain implementation. It only defines the signature of the method without including the method body. An abstract method must be implemented in the derived class.
```sh
abstract class Employee {
    constructor(private firstName: string, private lastName: string) {
    }
    abstract getSalary(): number
    get fullName(): string {
        return `${this.firstName} ${this.lastName}`;
    }
    compensationStatement(): string {
        return `${this.fullName} makes ${this.getSalary()} a month.`;
    }
}
```
```sh
class FullTimeEmployee extends Employee {
    constructor(firstName: string, lastName: string, private salary: number) {
        super(firstName, lastName);
    }
    getSalary(): number {
        return this.salary;
    }
}
```
```sh
class Contractor extends Employee {
    constructor(firstName: string, lastName: string, private rate: number, private hours: number) {
        super(firstName, lastName);
    }
    getSalary(): number {
        return this.rate * this.hours;
    }
}
```
```sh
let john = new FullTimeEmployee('John', 'Doe', 12000);
let jane = new Contractor('Jane', 'Doe', 100, 160);

console.log(john.compensationStatement());
console.log(jane.compensationStatement());

// Output
John Doe makes 12000 a month.
Jane Doe makes 16000 a month.
```

#### TypeScript Interface
TypeScript interfaces define the contracts within your code. They also provide explicit names for type checking.
```sh
interface Person {
    firstName: string;
    lastName: string;
}

function getFullName(person: Person) {
    return `${person.firstName} ${person.lastName}`;
}

let john = {
    firstName: 'John',
    lastName: 'Doe'
};

console.log(getFullName(john));
```
Optional properties
```sh
interface Person {
    firstName: string;
    middleName?: string;
    lastName: string;
}

function getFullName(person: Person) {
    if (person.middleName) {
        return `${person.firstName} ${person.middleName} ${person.lastName}`;
    }
    return `${person.firstName} ${person.lastName}`;
}
```
Readonly properties
```sh
interface Person {
    readonly ssn: string;
    firstName: string;
    lastName: string;
}

let person: Person;
person = {
    ssn: '171-28-0926',
    firstName: 'John',
    lastName: 'Doe'
}
// Throws error
person.ssn = '171-28-0000';
```
Function types
```sh
interface StringFormat {
    (str: string, isUpper: boolean): string
}

let format: StringFormat;
format = function (str: string, isUpper: boolean) {
    return isUpper ? str.toLocaleUpperCase() : str.toLocaleLowerCase();
};
console.log(format('hi', true));
```
Class Types
```sh
interface Json {
   toJSON(): string
}

The following declares a class that implements the Json interface:
class Person implements Json {
    constructor(private firstName: string,
        private lastName: string) {
    }
    toJson(): string {
        return JSON.stringify(this);
    }
}

The following example shows how to use the Person class:
let person = new Person('John', 'Doe');
console.log(person.toJson());

<!--Output-->
{"firstName":"John","lastName":"Doe"}
```

#### Extend Interfaces in TypeScript
Suppose that you have an interface called Mailable that contains two methods called send() and queue() as follows:
```sh
interface Mailable {
    send(email: string): boolean
    queue(email: string): boolean
}
```
```sh
later(email: string, after: number): void
```
```sh
interface FutureMailable extends Mailable {
    later(email: string, after: number): boolean
}
```
To extend an interface, you use the extends keyword with the following syntax:
```sh
interface A {
    a(): void
}

interface B extends A {
    b(): void
}
```
The following shows how to implement the FutureMailable interface:
```sh
class Mail implements FutureMailable {
    later(email: string, after: number): boolean {
        console.log(`Send email to ${email} in ${after} ms.`);
        return true;
    }
    send(email: string): boolean {
        console.log(`Sent email to ${email} after ${after} ms. `);
        return true;
    }
    queue(email: string): boolean {
        console.log(`Queue an email to ${email}.`);
        return true;
    }
}
```

Interfaces extending multiple interfaces
```sh
interface C {
    c(): void
}

interface D extends B, C {
    d(): void
}
```
Interfaces extending classes
- TypeScript allows an interface to extend a class. In this case, the interface inherits the properties and methods of the class. Also, the interface can inherit the private and protected members of the class, not just the public members.
- It means that when an interface extends a class with private or protected members, the interface can only be implemented by that class or subclasses of that class from which the interface extends.

```sh
class Control {
    private state: boolean;
}

interface StatefulControl extends Control {
    enable(): void
}

class Button extends Control implements StatefulControl {
    enable() { }
}
class TextBox extends Control implements StatefulControl {
    enable() { }
}
class Label extends Control { }


// Error: cannot implement
class Chart implements StatefulControl {
    enable() { }
}
```

#### Intersection Types
An intersection type creates a new type by combining multiple existing types. The new type has all features of the existing types.
To combine types, you use the & operator as follows:
```sh
type typeAB = typeA & typeB;
```
Suppose that you have three interfaces: `BusinessPartner, Identity, and Contact`.
```sh
interface BusinessPartner {
    name: string;
    credit: number;
}

interface Identity {
    id: number;
    name: string;
}

interface Contact {
    email: string;
    phone: string;
}
```
The following defines two intersection types:
```sh
type Employee = Identity & Contact;
type Customer = BusinessPartner & Contact;
```
The Employee type contains all properties of the Identity and Contact type:
```sh
type Employee = Identity & Contact;

let e: Employee = {
    id: 100,
    name: 'John Doe',
    email: 'john.doe@example.com',
    phone: '(408)-897-5684'
};
```

#### Type Casting
JavaScript doesn't have a concept of type casting because variables have dynamic types. However, every variable in TypeScript has a type. Type castings allow you to convert a variable from one type to another.
In TypeScript, you can use the `as` keyword or `<>` operator for type castings.

The following selects the first input element by using the `querySelector()` method:
```sh
let input = document.querySelector('input[type="text"]');
```
Since the returned type of the `document.querySelector()` method is the `Element` type, the following code causes a compiler error:
```sh
console.log(input.value);
```

The reason is that the value property doesn't exist in the `Element` type. It only exists on the `HTMLInputElement` type.

To resolve this, you can use type casting that cast the `Element` to `HTMLInputElement` by using the as keyword like this:
```sh
let input = document.querySelector('input[type="text"]') as HTMLInputElement;
```
Type Casting using the `<>` operator
```sh
let input = <HTMLInputElement>document.querySelector('input[type="text"]');
console.log(input.value);
```

#### Type Assertions
Type assertions instruct the TypeScript compiler to treat a value as a specified type. It uses the `as` keyword to do so:
```sh
expression as targetType
```
A type assertion is also known as type narrowing. It allows you to narrow a type from a `union type`.
```sh
function getNetPrice(price: number, discount: number, format: boolean): number | string {
    let netPrice = price * (1 - discount);
    return format ? `$${netPrice}` : netPrice;
}
```
The following uses the `as` keyword to instruct the compiler that the value assigned to the `netPrice` is a `string`:
```sh
let netPrice = getNetPrice(100, 0.05, true) as string;
console.log(netPrice);
```
Similarly, the following uses the `as` keyword to instruct the compiler that the returned value of the `getNetPrice()` function is a `number`.
```sh
let netPrice = getNetPrice(100, 0.05, false) as number;
console.log(netPrice);
```
#### Typescript Generics
TypeScript generics allow you to write the reusable and generalized form of `functions, classes, and interfaces`.

The following `getRandomNumberElement()` function takes an array of numbers as its parameter and returns a random element from the array:
```sh
function getRandomNumberElement(items: number[]): number {
    let randomIndex = Math.floor(Math.random() * items.length);
    return items[randomIndex];
}
```
```sh
let numbers = [1, 5, 7, 4, 2, 9];
console.log(getRandomNumberElement(numbers));
```
Assuming that you need to get a random element from an array of `strings`. This time, you may come up with a new function:
```sh
function getRandomStringElement(items: string[]): string {
    let randomIndex = Math.floor(Math.random() * items.length);
    return items[randomIndex];
}
```
```sh
let colors = ['red', 'green', 'blue'];
console.log(getRandomStringElement(colors));
```
The logic of the `getRandomStringElement()` function is the same as the one in the `getRandomNumberElement()` function.

This can be solved by using `any` type like below code but there is a drawback it doesn't ensure the return type of the function.
```sh
function getRandomAnyElement(items: any[]): any {
    let randomIndex = Math.floor(Math.random() * items.length);
    return items[randomIndex];
}
```
##### TypeScript generics come to rescue
The following shows a generic function that returns the random element from an array of type `T`:
```sh
function getRandomElement<T>(items: T[]): T {
    let randomIndex = Math.floor(Math.random() * items.length);
    return items[randomIndex];
}
```
##### Calling a generic function
The following shows how to use the `getRandomElement()` with an array of `numbers`:
```sh
let numbers = [1, 5, 7, 4, 2, 9];
let randomEle = getRandomElement<number>(numbers);
console.log(randomEle);
```

##### Generic functions with multiple types
The following illustrates how to develop a generic function with two type variables `U` and `V`:
```sh
function merge<U, V>(obj1: U, obj2: V) {
    return {
        ...obj1,
        ...obj2
    };
}
```
The `merge()` function merges two objects with the type `U` and `V`. It combines the properties of the two objects into a single object.

The following illustrates how to use the `merge()` function that merges two objects:
```sh
let result = merge(
    { name: 'John' },
    { jobTitle: 'Frontend Developer' }
);

console.log(result);
```
```sh
// Output
{ name: 'John', jobTitle: 'Frontend Developer' }
```
The following are benefits of TypeScript generics:
- Leverage type checks at the compile time.
- Eliminate type castings.
- Allow you to implement generic algorithms.

#### TypeScript Generic Constraints
Consider the following example:
```sh
function merge<U, V>(obj1: U, obj2: V) {
    return {
        ...obj1,
        ...obj2
    };
}
```
The `merge()` is a generic function that merges two objects. For example:
```sh
let person = merge(
    { name: 'John' },
    { age: 25 }
);

console.log(result);
```
It wroks perfectly fine.
The `merge()` function expects two objects. However, it doesn't prevent you from passing a non-object like this:
```sh
let person = merge(
    { name: 'John' },
    25
);

console.log(person);
```
Typescript doesn't issue any error

Instead of working with all types, you may want to add a constraint to the merge() function so that it works with objects only.
In order to denote the constraint, you use the `extends` keyword. For example:
```sh
function merge<U extends object, V extends object>(obj1: U, obj2: V) {
    return {
        ...obj1,
        ...obj2
    };
}
```
The following will result in an error:
```sh
let person = merge(
    { name: 'John' },
    25
);
```
##### Using type parameters in generic constraints
The following `prop()` function accepts an object and a property name. It returns the value of the property.
Add a constraint to K to ensure that it is a key of T as follows:
```sh
function prop<T, K extends keyof T>(obj: T, key: K) {
    return obj[key];
}
```

#### TypeScript Generic Classes
The following shows a complete generic Stack class called `Stack<T>`:
```sh
class Stack<T> {
    private elements: T[] = [];

    constructor(private size: number) {
    }
    isEmpty(): boolean {
        return this.elements.length === 0;
    }
    isFull(): boolean {
        return this.elements.length === this.size;
    }
    push(element: T): void {
        if (this.elements.length === this.size) {
            throw new Error('The stack is overflow!');
        }
        this.elements.push(element);

    }
    pop(): T {
        if (this.elements.length == 0) {
            throw new Error('The stack is empty!');
        }
        return this.elements.pop();
    }
}
```
The following creates a new stack of numbers:
```sh
let numbers = new Stack<number>(5);
```
#### TypeScript Generic Interfaces
```sh
interface Collection<T> {
    add(o: T): void;
    remove(o: T): void;
}
```
And this `List<T>` generic class implements the `Collection<T>` generic interface:
```sh
class List<T> implements Collection<T>{
    private items: T[] = [];

    add(o: T): void {
        this.items.push(o);
    }
    remove(o: T): void {
        let index = this.items.indexOf(o);
        if (index > -1) {
            this.items.splice(index, 1);
        }
    }
}
```
For example, the following shows how to use the `List<T>` generic class to create a list of numbers:
```sh
let list = new List<number>();

for (let i = 0; i < 10; i++) {
    list.add(i);
}
```

### Refrence
[`Typescript Tutorial`](https://www.typescripttutorial.net/)
