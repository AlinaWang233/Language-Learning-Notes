# JavaScript

## Language
### Origin
JavaScript borrows most of its syntax from Java, C, and C++, but it has also been influenced by Awk, Perl, and Python.
- case sensitive
- unicode

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
- let: define a block-scoped, local variable, optionally initializing to a value
- const: define a block-scoped, read-only named constant
- 
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

### Events
For interactivity, the website needs event handler to constantly listen for activity

