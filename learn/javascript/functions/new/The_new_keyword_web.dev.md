# The new keyword  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/functions/new?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Fnew](https://web.dev/learn/javascript/functions/new?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Fnew)  
**Last Updated:** 2025-05-23T01:12:13.546Z  
**Extracted:** 2025-05-31 16:58:10

---

# The new keyword | web.dev

The new keyword

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Calling a function with `new` creates a new object using the called function as the "constructor" for that object:

```
function MyFunction() {}
const myObject = new MyFunction();

typeof myObject;
> "object"`
```

This lets a "constructor function" provide a template for the creation of objects that follow the same structural pattern:

```
function MyFunction() {
  this.myProperty = true;
}
const myObject = new MyFunction();

myObject.myProperty;
> true
```

The value of [`this`](https://web.dev/learn/javascript/functions/this) within a constructor function refers to the object being created, letting the object be populated with properties and methods at the time of creation. This allows for the creation of objects that contain data values and any methods needed to act on that data as a single portable unit, a concept called "encapsulation":

```
function MyFunction( myArgument ) {
    this.myValue = myArgument;
    this.doubleMyValue = () => myArgument * 2;
}
const myObject = new MyFunction( 10 );

myObject.myValue;
> 10

myObject.doubleMyValue();
> 20
```

[`this`](https://web.dev/learn/javascript/functions/this) refers to the current execution context of a function, meaning that a constructor function follows the same rules for the value of `this` as any other function. For example, a function intended as a constructor uses [global binding](https://web.dev/learn/javascript/functions/this#global-binding) for the value of `this` when invoked independently:

```
function MyFunction() {
    console.log( this  );
}
const myObject = new MyFunction();
> MyFunction { }

MyFunction(); // Global `this` binding outside of strict mode is `globalThis`
> Window { … }

(function() {
    "use strict";
    function MyFunction() {
            console.log( this );
    }
    MyFunction();  // Global `this` binding inside of strict mode is `undefined`
}());
> undefined
```

It's conventional to capitalize the first character of a constructor function's identifier, following the naming pattern established by JavaScript's built-in factory functions. Though you may sometimes see the terms used interchangeably, constructor functions—functions intended to act on a newly-constructed object when invoked with the `new` keyword—differ from "factory functions," which _explicitly_ [`return`](https://web.dev/learn/javascript/functions/return) an object when invoked normally:

```
function myFunction( myArgument = false ) {
  return { "myProperty" : myArgument };
}
const myObject = myFunction( true );

myObject;
> Object { myProperty: true }
```

Though the underlying principles are the same, the use cases for custom constructor functions are better served by the more fully-featured [Class](https://web.dev/learn/javascript/classes) syntax introduced in ES6.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
