# JavaScript
- Client-side: supply objects to control a browser and its Document Object Model (DOM)

ex. HTML and the interactive features on it

- Server-side: supply objects relevant to running JavaScript on a server

ex. Node.js and its communication with the database


## Language
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
- Strict equality: (**===**) same value & data type 
- Not equal: (**!==**)
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
Anonymous Function:
because it gets no name
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
- Properties should be seperated by a comma **,**
- Single-word properties doesn't need double quotation, otherwise yes.
- Access or edit properties by **.name** if single word or **["name"]** if multiple
  - can also access nested array
- Delete by **delete myDog.name** or **delete myDog["name"]**

### Events
For interactivity, the website needs event handler to constantly listen for activity in the browser and run code in response.



