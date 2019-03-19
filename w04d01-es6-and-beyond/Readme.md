# ES6 and beyond

## Learning Competencies
- ES6 introduction
- Use let and const and explain the implications of using both
- Use template strings to avoid string concatenation in your JavaScript code
- Arrow Function & use them to write shorter functions
- Explain the difference between arrow functions and the function keyword
- Destructuring and Array spread
- Imports and exports
- Dynamic Object Keys
- What is ES6 Class Syntax
- Compare and contrast the class keyword versus writing constructor functions and prototypes


## Overview

### What Wikipedia says
ECMAScript is supported in many applications, especially Web browsers, where it is implemented by JavaScript, or, in the case of Internet Explorer, JScript. Implementations sometimes include extensions to the language, or to the standard library and related application programming interfaces (API) such as the World Wide Web Consortium (W3C) specified Document Object Model (DOM). This means that applications written in one implementation may be incompatible with another, unless they are written to use only a common subset of supported features and APIs.

ES6, or ECMAScript 6, is the first significant update to the language since ES5 was initially released in 2009.
Many ES6 features are already available in modern JavaScript engines. YOu have been using most of these already in the previous exercises. Using Babel, however, gives us access to many more features, while ensuring our JavaScript runs on more platforms. React Native uses Babel to enable ES6 features and ensure cross-platform consistency, as your JavaScript will run on Android, iOS, Windows, and other platforms.

### Why use ES6
The 6th edition, officially known as ECMAScript 2015, was finalized in June 2015. This update adds significant new syntax for writing complex applications, including classes and modules, but defines them semantically in the same terms as ECMAScript 5 strict mode. Other new features include iterators and for/of loops, Python-style generators and generator expressions, arrow functions, binary data, typed arrays, collections (maps, sets and weak maps), promises, number and math enhancements, reflection, and proxies (metaprogramming for virtual objects and wrappers). Hence made the

### Story
The ECMAScript specification is a standardized specification of a scripting language developed by Brendan Eich of Netscape; initially it was named Mocha, later LiveScript, and finally JavaScript. In December 1995, Sun Microsystems and Netscape announced JavaScript in a press release. In March 1996, Netscape Navigator 2.0 was released, featuring support for JavaScript.

The 6th edition, officially known as ECMAScript 2015, was finalized in June 2015. This update adds significant new syntax for writing complex applications, including classes and modules, but defines them semantically in the same terms as ECMAScript 5 strict mode. Other new features include iterators and for/of loops, Python-style generators and generator expressions, arrow functions, binary data, typed arrays, collections (maps, sets and weak maps), promises, number and math enhancements, reflection, and proxies (metaprogramming for virtual objects and wrappers).

### Block Scoped Declarations

Instead of using var to declare local variables, we use `const` and `let`. The main difference is that `var` is scoped to a function, while `const` and `let` are scoped to a block.        
Additionally, variables declared with const can only be assigned a value once. Assigning another value to the same name will throw a compiler error. Note that if the value assigned to a `const` variable is an object or array, the object or array may still be modified. In other words, it's only the variable name that is bound permanently -- the value itself is still mutable.

```js
const a = 1
let b = 'foo'

// Not allowed!
// a = 2

// Ok!
b = 'bar'

if (true) {
  const a = 3
}
```
You'll notice that the compiled output replaces `const` and `let` with `var`.

### Template strings
ES2015 gives us string interpolation using back ticks (``) and adding our variables in a ${}. Here is an example:
```js
`Now we can do string interpolation like ${1+1}`;

var person = "Elie";

`My name is ${person}`;
```
String interpolation can make working with strings much more convenient, because it allows us to avoid having to do a lot of string concatenation:
```js
var firstName = "Matt";
var lastName = "Lane";
var title = "instructor";
var employer = "Rithm";

// ughhh, so much concatenation...
var greeting1 = "Hi, my name is " + firstName + " " + lastName + ", and I am an " + title + " at " + employer + "!";

// much better
var greeting2 = `Hi, my name is ${firstName} ${lastName}, and I am an ${title} at ${employer}!`;
```
### for of loop
Another nice addition to ES2015 is the `for of` loop which allows us to iterate through what is called an iterable.
When dealing with arrays, note the difference between a for in loop and a for of loop. The for in loop will loop over the indices of an array; the for of loop will loop over the elements of an array:
```js
let letters = ['a', 'b', 'c'];

for (let idx in letters) {
    console.log(idx);
}
// 0
// 1
// 2

for (let char of letters) {
    console.log(char); 
}
// 'a'
// 'b'
// 'c'
```


## Arrow Functions
Like all type classes, arrows can be thought of as a set of qualities that can be applied to any data type. In the Haskell programming language, arrows allow functions (represented in Haskell by an arrow symbol) to combine in a reified form. However, the actual term "arrow" may also come from the fact that some (but not all) arrows correspond to the morphisms (also known as "arrows" in category theory) of different Kleisli categories. As a relatively new concept, there is not a single, standard definition, but all formulations are logically equivalent, feature some required methods, and strictly obey certain mathematical laws.

Read more about Arrow Function [here](https://en.wikipedia.org/wiki/Arrow_(computer_science))

### Why Arrow Functions are used
Arrows may be extended to fit specific situations by defining additional operations and restrictions. Commonly used versions include arrows with choice, which allow a computation to make conditional decisions, and arrows with feedback, which allow a step to take its own outputs as inputs. Another set of arrows, known as arrows with application, are rarely used in practice because they are actually equivalent to monads.

Arrows have several benefits, mostly stemming from their ability to make program logic explicit yet concise. Besides avoiding side effects, purely functional programming creates more opportunities for static code analysis. This in turn can theoretically lead to better compiler optimizations, easier debugging, and features like syntax sugar

### Code along

There are two important differences in the behavior of these functions, compared to functions defined with function.
- The binding for the keyword this is the same outside and inside the fat arrow function. This is different than functions declared with function, which can bind this to another other object upon invocation. Maintaining the this binding is very convenient for operations like mapping: `this.items.map(x => this.doSomethingWith(x))`.

- Fat arrow functions don't have an arguments object defined. You can achieve the same thing using the spread syntax: `(...args) => doSomething(args[0], args[1])`.

The fat arrow `function` syntax can vary a bit. If the function takes exactly one parameter, the parentheses can be omitted: `x => Math.pow(x, 2)`. Any other number of arguments will need parentheses: `(x, y) => Math.pow(x, y)`. If the function body is not wrapped in curly braces, it is executed as an expression, and the return value of the function is the value of the expression. The function body can be wrapped in curly braces to make it a block, in which case you will need to explicitly return a value, if you want something returned. You will likely use the curly braces and block version more frequently, as this allows the function body to include multiple lines of code.

```js
const foo = () => 'bar'

const baz = (x) => {
  return x + 1
}

const squareSum = (...args) => {
  const squared = args.map(x => Math.pow(x, 2))
  return squared.reduce((prev, curr) => prev + curr)
}

this.items.map(x => this.doSomethingWith(x))
```
### Comparing Function Keyword and Arrow Function
```js
var obj = {
    firstName: "Elie",
    sayHi: function(){
        setTimeout(function(){
            console.log("Hi, I am " + this.firstName);
        },1000)
    }
}
```
If you call `obj.sayHi()` in this example, you'll see that "Hi, I'm undefined" gets logged to the console one second later. This is because the callback to setTimeout loses the context of this, as it isn't being called as a method on `obj`.

When using an arrow function for this callback, however, the arrow function keeps its value from the enclosing context: in this case, it will refer to the `obj` object, and the `console.log` will work as expected:
```js
var objES2015 = {
    firstName: "Elie",
    sayHi: function(){
        setTimeout(() => {
            console.log(`Hi, I am ${this.firstName}`);
        },1000)
    }
}
```


## Classes
In object-oriented programming, a **class** is an extensible program-code-template for creating objects, providing initial values for state (member variables) and implementations of behavior (member functions or methods). In many languages, the class name is used as the name for the class (the template itself), the name for the default constructor of the class (a subroutine that creates objects), and as the type of objects generated by instantiating the class; these distinct concepts are easily conflated.

Whereas the **syntax** is the set of rules, principles, and processes that govern the structure of sentences in a given language, specifically word order and punctuation. It is also used to refer to the study of such principles and processes. The goal of many syntacticians is to discover the syntactic rules common to all languages.

### Why they both are use
ES6 Classes formalize the common JavaScript pattern of simulating class-like inheritance hierarchies using functions and prototypes. They are effectively simple sugaring over prototype-based Object oriented programming, offering a convenient declarative form for class patterns which encourage interoperability.


### Code Along
Here is what an ES2015 Syntax Implementation looks like:
```js
class Person {
    constructor(firstName, lastName){
        this.firstName = firstName;
        this.lastName = lastName;
    }
    sayHi(){
        return `${this.firstName} ${this.lastName} says hello!`;
    }
    static isPerson(person){
        return person.constructor === Person;
    }
}
```
The function called constructor MUST be named that way (since that is what is run when the new keyword is used). If you just try to run `Person() `you will get a TypeError with the message that "Class constructor Person cannot be invoked without `new`".

If we want to add functions directly on the "class" (which is really a function), we use the word `static`.

### Inheritance
The class gives us simple inheritance with the keyword extends. In classes that inherit from parents, we have access to a function super(). Within an inherited function in that child class, super will invoke the parent class's version of that function
```js
class Cat extends Animal {
  printName() {
    super.printName()
    console.log(`My name is ${this.name}`)
  }
}
```


## Other ES6 Features
There are a ton of features that have been introduced in ES6. We have covered the most major ones here. Explore what all ES6 has to offer and how and why these features are extremely useful fro developing modern software with JavaScript.

**Spread syntax** allows an iterable such as an array expression to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.

In ES5, object literal keys are always interpreted as a string. ES6 allows us to use computed values as keys in object literals, using square bracket syntax: [myKey].


## Exploration
- [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes), [ES6 Classes](https://www.tutorialspoint.com/es6/es6_classes.htm)
- [Static Methods](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)
- [ES6 Syntax](https://www.tutorialspoint.com/es6/es6_syntax.htm)
