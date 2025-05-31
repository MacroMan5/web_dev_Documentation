# Symbol  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/data-types/symbol?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fsymbol](https://web.dev/learn/javascript/data-types/symbol?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fsymbol)  
**Last Updated:** 2025-05-23T01:11:55.248Z  
**Extracted:** 2025-05-31 16:58:10

---

# Symbol  |  web.dev

Symbol

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

A symbol primitive represents a unique value that never collides with any other value, including the value of other symbol primitives. Two string primitives made up of identical characters evaluate as strictly equal:

```
String() === String()
> true

String( "My string." ) === String( "My string." );
> true
```

However, no two symbols created using the `Symbol()` function can ever be strictly equal:

```
Symbol() === Symbol()
> false
```

This trait lets you use symbols as unique property keys in an object, preventing collisions with keys any other code might add to that object.

```
const mySymbol = Symbol( "Desc" );

const myObject = {};
myObject[mySymbol] = "propSymbol";

myObject
> Object { Symbol("Desc"): "propSymbol" }
```

There are three types of symbols:

*   Symbols created with `Symbol()`
*   Shared symbols that are set and retrieved from a global Symbol registry using `Symbol.for()`
*   "Well-known symbols" defined as static properties on the Symbol object. These symbols contain internal methods that can't be accidentally overwritten.

`Symbol()` accepts a description (or "symbol name") as an optional argument. These descriptions are human-readable labels for debugging purposes, and they don't affect the uniqueness of the result. Any call to `Symbol` returns a completely unique symbol primitive, even if multiple calls have identical descriptions:

```
Symbol( "My symbol." ) === Symbol( "My symbol." );
> false
```

As with other primitive data types, symbols inherit methods and properties from their [prototype](https://web.dev/learn/javascript/appendix#prototypal-inheritance). For example, you can access a description as an inherited property of the created symbol:

```
let mySymbol = Symbol( "My symbol." );

mySymbol.description
> "My symbol."
```

But you can't create a symbol using the `new` keyword:

```
let mySymbol = new Symbol();

> Uncaught TypeError: Symbol is not a constructor
```

Symbols aren't enumerable, meaning that symbolic properties aren't available when using standard methods to iterate over them. The `getOwnPropertySymbols()` method gives access to an object's symbol properties.

The `Symbol.for()` method tries to look up any existing symbols in a runtime-wide global symbol registry with a given string as the key, and returns the matching symbol if one is found. If it doesn't find one, it creates a symbol with the specified key and adds it to the global registry:

```
let sharedSymbol = Symbol.for( "My key." );

sharedSymbol === Symbol.for( "My key." )
> true
```

These keys share no functional overlap with the descriptions assigned to author-created `Symbol` primitives. To access a symbol in the symbol registry, you must first create it using `for()`:

```
Symbol( "String" ) === Symbol( "String" );
> false

Symbol( "String" ) === Symbol.for( "String" );
> false

Symbol.for( "String" ) === Symbol.for( "String" );
> true
```

To retrieve the key for any symbol from the symbol registry, use `Symbol.keyFor()`:

```
let mySymbol = Symbol.for( "Key." );

Symbol.keyFor( mySymbol ) ;
> "Key."
```

## "Well-known" symbols

_Well-known symbols_ are static properties of the `Symbol` object, each of which is a symbol itself. Well-known symbols provide unique property keys for accessing and modifying JavaScript's built-in methods, while preventing core behavior from being unintentionally overwritten.

```
Symbol;
> function Symbol()
    asyncIterator: Symbol(Symbol.asyncIterator)
    for: function for()
    hasInstance: Symbol("Symbol.hasInstance")
    isConcatSpreadable: Symbol("Symbol.isConcatSpreadable")
    iterator: Symbol(Symbol.iterator)
    keyFor: function keyFor()
    length: 0
    match: Symbol("Symbol.match")
    matchAll: Symbol("Symbol.matchAll")
    name: "Symbol"
    prototype: Object { … }
    replace: Symbol("Symbol.replace")
    search: Symbol("Symbol.search")
    species: Symbol("Symbol.species")
    split: Symbol("Symbol.split")
    toPrimitive: Symbol("Symbol.toPrimitive")
    toStringTag: Symbol("Symbol.toStringTag")
    unscopables: Symbol("Symbol.unscopables")
    <prototype>: function ()
```

Because symbols are a feature specific to ES6, these symbolic values are intended to be used as "extension points" for developers modifying JavaScript's behavior without introducing backwards-compatibility issues.

Well-known symbol values are often stylized with a [`@@` prefix or wrapped in `%`](https://github.com/tc39/ecma262/pull/1314) to differentiate their keys from their mutable prototypes. For example, `@@match` (or `%match%`) is a reference to the immutable `Symbol.match`, not `String.prototype.match`.

## Check your understanding

Can you use `new` to create a symbol?

Which of the following describe \`well-known\` symbols?

Unique property keys for accessing and modifying JavaScript's built-in methods

Symbols that you use frequently

Static properties of the \`Symbol\` object

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
