# Objects  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/objects?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects](https://web.dev/learn/javascript/objects?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects)  
**Last Updated:** 2025-05-23T01:12:33.766Z  
**Extracted:** 2025-05-31 16:58:10

---

# Objects  |  web.dev

Objects

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Objects are a discrete data type in the same way that each [primitive](https://web.dev/learn/javascript/data-types) is a data type, with one critical difference: unlike primitives, objects are _mutable_. An object can contain data associated with identifiers, like a variable, but it keeps its `object` data type no matter what data it contains.

Aside from primitives, all JavaScript values are objects, though because even primitive literals exhibit object-like behavior due to [prototypal inheritance](https://web.dev/learn/javascript/objects/prototypal-inheritance), it's often said that JavaScript is effectively made up of objects.

An object literal is a pair of curly braces surrounding zero or more key-value pairs called "properties," which can contain any JavaScript value.

```
{
    "myProperty" : true
}
```

Property _keys_ can be any [symbol](https://web.dev/learn/javascript/data-types/symbol) or [string](https://web.dev/learn/javascript/data-types/string). As when assigning an identifier to a variable, the strings used as property keys should be predictable and descriptive:

```
let carAttributes = {
    "color" : "red"
};

carAttributes
> Object { color: "red" }
```

Property keys require a single (`'`) or double quoted (`"`) string literal, not a [template literal](https://web.dev/learn/javascript/data-types/string#template-literals):

```
let carAttributes = {
    `keyString` : false
};
> Uncaught SyntaxError: expected property name, got template literal
```

Property values can be any data type. The properties of an object can themselves contain objects with their own properties:

```
let myObject = {
    'key' : {
        'subkey' : true,
        'othersubkey' : false
    }
};

myObject;
> Object { key: Object { subkey: true, othersubkey: false } }
```

When the value of a property is a function, that property is called a "method."

```
const myObject = {
    "myProperty" : true,
    myMethod() {
        console.log( "This is a method." );
    }
}

myObject.myProperty;
> true

myObject.myMethod();
> "This is a method."
```

You can also create an object using the `new` keyword:

```
let myObject = new Object();
```

In the previous examples, the newly-created object literals have been assigned to variables. This isn't required, because like any other data type, you can use an object without an identifier anywhere an object is expected. However, an object literal requires parentheses in any context where it could be confused for a block statement, given that the two share curly brace syntax (`{}`). Initializing a variable never requires this.

```
{ "value" : 2 }
> Uncaught SyntaxError: unexpected token: ':'

({ "value" : 2 })
> Object { value: 2 }

let valObj = { "value" : 2 };

valObj;
> Object { value: 2 }
```

Unlike primitives, there's no meaningful difference in the results of creating an object using `new Object()` and creating an object literal, because the result in either case will be an object with properties inherited from the `Object` prototype. However, there is one practical difference between the two syntaxes.

The `new` keyword must define an empty object that is filled with data later:

```
let myObject = new Object();

myObject.booleanValue = true;
myObject.stringValue = "My string.";
```

An object literal can be populated with data when it's created:

```
let myObject = {
    'booleanValue' : true,
    'stringValue' : "My string."
};
```

Though it has little practical use, `new Object()` can be used to turn primitive data values into Objects of their respective type, like those returned by using the `new` keyword along with their [constructor](https://web.dev/learn/javascript/functions/new) function. For example, the following is functionally equivalent to `new Number( 10 )`:

```
let myObject = new Object( 10 );

myObject;
> Number { 10 }
```

`null` and `undefined` values result in an empty object, functionally identical to invoking `new Object()` without supplying an argument.

Passing an object literal to `new Object()` as an argument passes the object literal without changing it:

```
let myObject = new Object( { myValue : 10 } );

myObject;
> Object { myValue: 10 }
```

As with using constructors for primitive values, using constructors for objects rarely has any benefits over using object literal notation. Even when creating empty objects to be populated with values later, developers tend to favor object literal notation for the sake of simplicity.

## Check your understanding

What kinds of notation can you use to set an object's properties?

Which of the following is the correct syntax for getting the value of `myProp`

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
