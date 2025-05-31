# The return keyword  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/functions/return?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Freturn](https://web.dev/learn/javascript/functions/return?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Freturn)  
**Last Updated:** 2025-05-23T01:12:20.144Z  
**Extracted:** 2025-05-31 16:58:10

---

# The return keyword | web.dev

The return keyword

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Use `return` to specify the value that the function should produce as a final result. When the interpreter reaches a `return` statement, the function that contains that statement immediately ends, and the specified value is returned to the context where the function was called:

```
const myFunction = function() {
   return 2 + 2;
}

myFunction();
> 4
```

A function that returns a value can be effectively treated as the data it contains, similar to a variable:

```
const myFunction = function() {
   return 2 + 2;
}

myFunction() + myFunction();
> 8
```

A `return` statement without an expression ends the function and returns `undefined`:

```
const myFunction = function() {
   return;
}

myFunction();
> undefined
```

Because the `return` keyword signals the end of a function, any code that follows an encountered `return` isn't executed:

```
const myFunction = function() {
   return true;
   console.log( "This is a string." );
}

myFunction();
> true
```

Additionally, code following an encountered `return` statement might result in a warning (but not an error) in some browsers' development consoles:

```
const myFunction = function() {
   return true;
   console.log( "This is a string." );
}
> unreachable code after return statement

myFunction();
> true
```

Again, this only applies to a `return` statement encountered during the execution of the function, not any code that follows a `return` statement sequentially:

```
const myFunction = function( myParameter ) {
   if( myParameter === undefined ) {
    return "This is the result.";
   }
   return "This is the alternate result.";
}

myFunction();
> "This is the result."

myFunction( true );
> "This is the alternate result."
```

"Short circuiting" a function using an early `return` can allow for more concise code than a single `return` statement at the end of a function. For example, the following function determines whether a passed value is a string containing five or more characters. If the passed value isn't a string literal, the code that counts the characters is unnecessary, and the function can return a `false` result immediately:

```
function myFunction( myString ) {
   if( typeof myString !== "string" ) {
    return false;
   }
   if( myString.length >= 5 ) {
    return true;
   } else {
    return false;
   }
}

myFunction( 100 );
> false

myFunction( "St" );
> false

myFunction( "String." );
> true
```

[Arrow function expressions](https://web.dev/learn/javascript/functions/function-expressions#arrow-functions) are unique in that the `return` keyword is implied when an arrow function body contains a single expression and no block syntax:

```
const myFunction = () => 2 + 2;

myFunction();
> 4
```

If you use block syntax to define the arrow function body, an explicit `return` is required, even if the function body only contains a single expression:

```
const myFunction = () => { 2 + 2 };

myFunction();
> undefined
```
```
const myFunction = () => { return 2 + 2 };

myFunction();
> 4
```

## Check your understanding

What is `return` used for?

Returning the code to the start of the function.

Specifying the final result of a function.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
