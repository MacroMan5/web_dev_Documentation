# Function expressions  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/functions/function-expressions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Ffunction-expressions](https://web.dev/learn/javascript/functions/function-expressions?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Ffunctions%2Ffunction-expressions)  
**Last Updated:** 2025-05-23T01:12:04.747Z  
**Extracted:** 2025-05-31 16:58:10

---

# Function expressions  |  web.dev

Function [expressions](https://web.dev/learn/javascript/introduction#expressions) are functions created where an expression is expected. You'll frequently encounter function expressions as values assigned to a variable. Although a function declaration always requires a name, you can use function expressions to create anonymous functions by omitting the identifier and following the `function` keyword with a pair of parentheses containing optional parameters:

```
const myVariable = function() { };
```

You can then [call](https://web.dev/learn/javascript/functions#function-calling) those function expressions using the variable's identifier:

```
const myVariable = function() {
    console.log( "This is my function." );
};

myVariable();
> "This is my function."
```

You can also use function expressions to create named functions using a syntax similar to function declarations:

```
const myVariable = function myFunction() {
    console.log( "This is my function." );
};

myVariable();
> "This is my function."
```

However, unlike function declarations, a named function expression can be accessed by function name only within the function itself:

```
const myVariable = function myFunction() {
  console.log( `I'm a ${ typeof myFunction }.`);
};

typeof myFunction;
> "undefined"

typeof myVariable;
> "function"

myVariable();
> "I'm a function."
```

Names associated with function expressions are primarily useful for debugging. A named function expression can also call itself recursively, though this isn't a very common use case in modern development:

```
const myVariable = function myFunction() {
    console.log( "One second elapsed." );
    setTimeout( myFunction, 1000 );
};

setTimeout( myVariable, 1000 );
> "One second elapsed."
> "One second elapsed."
> "One second elapsed."
…
```

### Arrow function expressions

Arrow function expressions (often called "arrow functions" or, rarely, "lambda functions") were introduced in ES6 to provide a concise syntax for creating anonymous function expressions with some unique behaviors.

You can create an arrow function wherever an expression is expected, for example, as a value assigned to a variable. In its most common form, an arrow function is made up of a pair of matched parentheses containing zero or more parameters, an arrow made up of a single equals sign and greater-than character (`=>`), and a pair of matched curly braces containing the function body:

```
const myFunction = () => {};
```

Under certain conditions, you can make the syntax even more compact. If you're only using one parameter, you can leave out the starting parentheses:

```
const myFunction = myParameter => {};
```

When you want the function body to [return the value of a single expression](https://web.dev/learn/javascript/functions/return), neither enclosing the function body in curly braces nor [the `return` keyword](https://web.dev/learn/javascript/functions/return) are required:

```
const myFunction = () => 2 + 2

myFunction()
> 4
```

Arrow functions are unique in that they don't have their own context for [`arguments`](https://web.dev/learn/javascript/functions#function-calling) or [`this`](https://web.dev/learn/javascript/functions/this) values. Instead, they inherit both values from the arrow function's [_lexically enclosing environment_](https://262.ecma-international.org/6.0/#sec-arrow-function-definitions-runtime-semantics-evaluation), the nearest enclosing function that does provide those contexts.

```
function myParentFunction() {
    this.myProperty = true;
    let myFunction = () => {
            console.log( this );
    }
    myFunction();
};

let myInstance = new myParentFunction();
> Object { myProperty: true }
```

### Call arrow functions

Arrow functions don't bind arguments in the same way as [other types of function](https://web.dev/learn/javascript/functions#function-calling). An `arguments` object in the body of an arrow function inherits its value from that arrow function's closest [lexically enclosing environment](https://262.ecma-international.org/6.0/#sec-arrow-function-definitions-runtime-semantics-evaluation):

```
function myFunction() {
    let myArrowFunction = () => {
            console.log( arguments[ 0 ] );
    }
    myArrowFunction( true );
};

myFunction( false );
> false
```

In this example, an outer function called with the argument `false` calls an inner arrow function with the argument `true`. Because the `arguments` object inside the arrow function resolves to the binding in the outer function, the inner function logs the outer function's `false`.

If there's no `arguments` object to inherit from the parent context, the arrow function's `arguments` object aren't defined, and trying to access it causes an error:

```
let myArrowFunction = () => {
    console.log(arguments);
};
myArrowFunction( true );
> Uncaught ReferenceError: arguments is not defined
```

### Immediately Invoked Function Expressions (IIFE)

An Immediately Invoked Function Expression (IIFE), also sometimes called a "self-executing anonymous function," is a function expression that is called immediately when it's defined. An IIFE uses a function expression created by enclosing the function in a [grouping operator](https://web.dev/learn/javascript/introduction#expressions). A second matched pair of parentheses then calls the function, either immediately following the function definition itself or immediately following the grouping operator. If you use a standard function, there's no practical difference between the two approaches:

```
(function() {
    console.log( "IIFE.")
    }
)();
> "IIFE."

(function() {
    console.log( "IIFE.")
    }
());
> "IIFE."
```

The first example calls the grouped function expression. The second example calls a function declaration inside the grouping operators, and the end result is then evaluated as a grouped expression. The result is the same in either case.

However, there is a difference when your IIFE is an arrow function. In this case, the parentheses used to call the function must be outside the grouping operators, because an arrow function on its own isn't an expression, but it must be created in a context where an expression is expected. Trying to call the arrow function from inside the scope of the grouping operators would mean calling an arrow function that hasn't yet been created in the context of an expression:

```
( () => {
    console.log( "IIFE." );
}() );
> Uncaught SyntaxError: missing ) in parenthetical
```

Because the grouping operators expect an expression, the arrow function within them is defined, letting the parentheses that follow them call the grouped expression:

```
( () => {
    console.log( "IIFE." );
} )();
> "IIFE."
```

Legacy applications, frequently used IIFEs to manage scope, specifically to avoid polluting the [global scope](https://web.dev/learn/javascript/data-types/variable#global-scope) with [function-scoped variables](https://web.dev/learn/javascript/data-types/variable#function-scope) and [function declarations](https://web.dev/learn/javascript/functions#declarations). Before the introduction of [block scoping](https://web.dev/learn/javascript/data-types/variable#block-scope) in ES6, it was common practice to wrap an entire script in an IIFE to prevent accidental pollution of the global scope.

## Check your understanding

Can you call a named function expression by name outside the function?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
