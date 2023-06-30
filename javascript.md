# JavaScript
- Client-side: supply objects to control a browser and its Document Object Model (DOM)

ex. HTML and the interactive features on it

- Server-side: supply objects relevant to running JavaScript on a server

ex. Node.js and its communication with the database


## Basic Syntax
### Origin
JavaScript borrows most of its syntax from Java, C, and C++, but it has also been influenced by Awk, Perl, and Python.
- case sensitive
- unicode
### Difference from Java
- do not have static typing and strong type checking
- runtime system vs. Java's compile time system
- prototype-based(dynamic inheritance) object model vs. Java's class-based object model 
- support functions without explicit declaration 

### Variable 
#### Identifiers (name of the variable)
- start with a letter, underscore(_), or dollar sign($)
#### Type
- String: let myVariable = 'Bob'/"Bob"
- Number
- Boolean
- Array
- Object:  let myVariable = document.querySelector('h1');

### Declaration
- var: define a (context-dependent local/global) variable, optionally initializing to a value 
  - (context-dependent local/global) 
  - initializer optional
- let: define a block-scoped, local variable, optionally initializing to a value
  - block-scoped, local
  - initializer optional
- const: define a block-scoped, read-only named constant
  - block-scoped, read-only
  - initializer required

`const { bar } = foo` = `var bar = foo(bar)`
In var and let declarations, the initializer is optional, (`value = undefined`), while it's a grammartical mistake for const.
### Operators
- Arithmetic: (+-*/)
- Assignment (=)/ Not(!)
- Strict equality: (`===`) same value & data type 
- Not equal: (`!==`)
- 
### Comments
same as Java / C;
```JavaScript
/*
This is a comment
*/

// Inline Comment

```

### Conditionals
Same as Java
### Functions


### Array
Most is similar to Java.

To manipulate the elements of the array:
- push: add the last element
- pop: remove the last element
- shift: remove the first element 
- unshift: add the first element

### JavaScript Object
Initialize JS object like below:
```JavaScript
const myDog = {
  name: dog,
  legs: 2,
  tail: 1,
  "its friends": []
}
```
- Properties should be seperated by a comma `,`
- Single-word properties doesn't need double quotation, otherwise yes.
- Access the known properties by `.name`  if single word & exact literal or `["name"]` if multiple or in a variable
  - - can also access nested array
- Add properties by `object.newProperty = something`
- Delete by `delete myDog.name` or `delete myDog["name"]`
- Check if a property exists using `.hasOwnProperty()`
### Events
For interactivity, the website needs event handler to constantly listen for activity in the browser and run code in response.

## ES6

### Variable Declaration (Scope Comparison)
- var:
  - (context-dependent local/**global**) 
  - initializer optional
- let: 
  - **block-scoped**, local
  - initializer optional
- const: 
  - block-scoped, **read-only**
  - initializer required
  - but can mutate elements using index within `const array`
  - use `const` first and change to `let` later if needed to mutate value

### Prevent Object Mutation
`Object.freeze(obj)` so that we can't add, edit, or delete property of `obj`

### Anonymous Function:
because it gets no name
- DO NOT USE `var`, use `const`
```JavaScript
function(){
    something;
};
```
Alternative: (a bit like lamda?)
```JavaScript
()=>{
    something;
}
```
With a certain number of parameters & Default value:
```JavaScript
const func = (par = "default value") =>{
    something;
}
```

With a varaible number of parameters:
```JavaScript
const func = (...args) =>{
    for(let i = 0; i < args.length; i++){
      something;
    }
}
```

### Spread Operator
```JavaScript
var arr = [6, 89, 3, 45];
```
Below two will return same result: `89`
```JavaScript
var maximus = Math.max.apply(null, arr);// Math.max only apply to comma-seperated objects, but not array
const maximus = Math.max(...arr);
```

`...arr`will spread the array, but only work in-place.
``` JavaScript 
const spreaded = [...arr];  // works
const spreaded = ...arr; // won't work
```

### Destructuring Assignment 
To Extract Values from Objects:

`const { prop1, prop2 } = obj` will extract values according to the property name from `obj`

To Assign Variables from Objects:

`const {prop1 : var1, prop2 : var2} = obj` will assign property values of `obj` to variables named `var`

- from nested objects:

`const { outerProp: {prop1 : var1, prop2 : var2}} = obj`

- from array:
```JavaScript
const [a, b,,, c] = [1, 2, 3, 4, 5, 6];
const [a, b,...d] = [1, 2, 3, 4, 5, 6];

a = 1, b = 2, c = 5;
d = [3, 4, 5, 6];
```
To Pass an Object as a Function's Parameters
```JavaScript
// const half = (stats) => (stats.max + stats.min) / 2.0; 

const half = ({max, min}) => {
  return (max + min) / 2.0;
}
```

### Template Literals
String could be used as a template. (Text wrapped by \`\` and variable wrapped by `${}`)
```JavaScript
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;
```

### Concise Declarations
Object Literal: 
`const getMousePosition = (x, y) => ({ x, y });`

Function:
Replace `:function() ` with only param`()`
```JavaScript
const person = {
  name: "Taylor",
  sayHello: function() {
    return `Hello! My name is ${this.name}.`;
  }
};
// is the same as below
const person = {
  name: "Taylor",
  sayHello() {
    return `Hello! My name is ${this.name}.`;
  }
};
```
### Class in JavaScript

```JavaScript
class Book {
  constructor(author) {
    this._author = author;
  }
  // getter
  get writer() {
    return this._author;
  }
  // setter
  set writer(updatedAuthor) {
    this._author = updatedAuthor;
  }
}
```
### Connect it to HTML
Add a line to HTML:
```HTML
<script type="module" src="index.js"></script>
```

Export:
- Typical: 
```JavaScript
export const add = (x, y) => {
  return x + y;
}
//is the same as 

const add = (x, y) => {
  return x + y;
}

export { add, subtract };
```
- Default export
Use `export default` if only one value is being exported from a file or to create a fallback value for a file or module. Should not use  with `let var const`.

Import:
- typical
```JavaScript
import { add, subtract } from './math_functions.js';
```
- import a default export
```JavaScript
import add from "./math_functions.js"; // variable name without {}
```

### Promise
Promise to do something usually asynchronously, usually have two states `resolve` and `reject`
Use `then` could continue to act if promise is `resolved` and use `catch` to catch `error` during `reject`.
```JavaScript
const makeServerRequest = new Promise((resolve, reject) => {
  
  let responseFromServer;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => {
  console.log(result);
});

makeServerRequest.catch(error => {
  console.log(error);
});
```