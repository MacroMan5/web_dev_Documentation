# Prototypal inheritance  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/objects/prototypal-inheritance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects%2Fprototypal-inheritance](https://web.dev/learn/javascript/objects/prototypal-inheritance?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects%2Fprototypal-inheritance)  
**Last Updated:** 2025-05-23T01:12:41.341Z  
**Extracted:** 2025-05-31 16:58:10

---

# Prototypal inheritance  |  web.dev

Prototypal inheritance

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Like [other data types](https://web.dev/learn/javascript/appendix#prototyal-inheritance), an object inherits properties and methods from a built-in `Object` prototype, meaning the resulting object contains both the properties you've defined and a prototype property containing the methods inherited from the prototype:

```
let myObject = {
    'booleanValue' : true
};

myObject;
> Object { booleanValue: true }
    booleanValue: true
    [[prototype]]: Object { … }
            __defineGetter__: function __defineGetter__()
            __defineSetter__: function __defineSetter__()
            __lookupGetter__: function __lookupGetter__()
            __lookupSetter__: function __lookupSetter__()
            __proto__: …
                constructor: function Object()
                hasOwnProperty: function hasOwnProperty()
                isPrototypeOf: function isPrototypeOf()
                propertyIsEnumerable: function propertyIsEnumerable()
                toLocaleString: function toLocaleString()
                toString: function toString()
                valueOf: function valueOf()
                <get __proto__()>: function __proto__()
                <set __proto__()>: function __proto__()
```

Prototype properties aren't intended to be accessed directly by property key. As you might notice in the previous example, this is implied by the `[[prototype]]` or `<prototype>` notation used in browsers' developer consoles and sources of documentation for the prototype's property key:

```
// Chrome:
let emptyObject = {};

emptyObject;
> {}
  [[prototype]]: Object
```
```
// Firefox:
let emptyObject = {};

emptyObject;
> Object {  }
  <prototype>: Object { … }
```

Though all common browsers use `__proto__` as a de facto standard, this isn't formally standardized and should be avoided in production code.

```
let emptyObject = {};

emptyObject.__proto__;
> Object { … }
    __defineGetter__: function __defineGetter__()
    __defineSetter__: function __defineSetter__()
    __lookupGetter__: function __lookupGetter__()
    __lookupSetter__: function __lookupSetter__()
    __proto__:
        constructor: function Object()
        hasOwnProperty: function hasOwnProperty()
        isPrototypeOf: function isPrototypeOf()
        propertyIsEnumerable: function propertyIsEnumerable()
        toLocaleString: function toLocaleString()
        toString: function toString()
        valueOf: function valueOf()
        <get __proto__()>: function __proto__()
        <set __proto__()>: function __proto__()
```

Instead, you can directly access and modify the `[[Prototype]]` of an object using the built-in `Object.getPrototypeOf()` and `Object.setPrototypeOf()` methods:

```
let myObj = { "value" : 5 };
let protoParent = { "protoValue" : true };

myObj;
Object { value: 5 }
    value: 5
    <prototype>: Object { … }

Object.getPrototypeOf( myObj );
> Object { … }
    __defineGetter__: function __defineGetter__()
    __defineSetter__: function __defineSetter__()
    __lookupGetter__: function __lookupGetter__()
    __lookupSetter__: function __lookupSetter__()
    __proto__:
    constructor: function Object()
    hasOwnProperty: function hasOwnProperty()
    isPrototypeOf: function isPrototypeOf()
    propertyIsEnumerable: function propertyIsEnumerable()
    toLocaleString: function toLocaleString()
    toString: function toString()
    valueOf: function valueOf()
    <get __proto__()>: function __proto__()
    <set __proto__()>: function __proto__()

Object.setPrototypeOf( myObj, protoParent );
> Object { value: 5 }
    value: 5
    <prototype>: Object { protoValue: true }
```

To differentiate between inherited properties and author-defined properties, the latter is typically called the object's "own properties."

The built-in `Object.hasOwn()` method returns `true` if the specified property is a direct property of the object, and `false` if the property is inherited or doesn't exist. Whenever possible, use [`Object.hasOwn()`](https://caniuse.com/mdn-javascript_builtins_object_hasown) instead of the inherited `hasOwnProperty()`method, which doesn't support [`Object.create()`](https://web.dev/learn/javascript/objects/property-descriptors).

```
let myObject = {
    'myValue' : 100
};

Object.hasOwn( myObject, 'myValue' );
> true

myObject.__proto__; // The Object prototype inherited by `myObject` is present:
> Object { … }

Object.hasOwn( myObject, '__proto__' ); // The Object prototype inherited by `myObject` is not an "own property:"
> false
```

## Check your understanding

Why should you avoid using `__proto__`?

It isn't supported by many browsers.

It will confuse future maintainers of your code.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
