# Property accessors  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/objects/property-accessors?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects%2Fproperty-accessors](https://web.dev/learn/javascript/objects/property-accessors?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fobjects%2Fproperty-accessors)  
**Last Updated:** 2025-05-23T01:12:35.169Z  
**Extracted:** 2025-05-31 16:58:10

---

# Property accessors  |  web.dev

Property accessors

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

There are two ways of setting, altering, and accessing the properties of an object: _dot notation_ and _bracket notation_.

## Dot notation

As seen in some previous examples, dot notation uses a period (`.`) between an object and the property key being accessed:

```
const myObj = {
    "myProp": "String value."
};

myObj.myProp;
> "String value."
```

You can use dot notation to access, change, or create new properties using [assignment operators](https://web.dev/learn/javascript/data-types/variable#declaration):

```
const myObj = {};

myObj.myProp = "String value.";

myObj;
> Object { myProp: "String value." }
```

Chaining property keys using dot notation lets you access the properties of objects that are themselves properties of an object:

```
const myObj = {
    "myProp": {
            "childProp" : true
    }
};

myObj.myProp.childProp;
> true;
```

However, using this syntax when a key specified in the chain might not be defined can cause errors. In the following example, `myMissingProp` isn't a property of the `myObj` object, so trying to access `myObj.myMissingProp` results in `undefined`. Trying to then access a property on `undefined`, as if it were an object, causes an error:

```
const myObj = {
    "myProp": {
            "childProp" : true
    }
};

> myObj.myMissingProp
> undefined

myObj.myMissingProp.childProp;
> Uncaught TypeError: myObj.myMissingProp is undefined
```

To address this issue, ES2020 introduced an "optional chaining operator" (`?.`) to safely access nested properties of objects.

```
const myObj = {
    "myProp": {
            "childProp" : true
    }
};

myObj.myMissingProp?.childProp;
> undefined
```

Keys accessed using dot notation aren't enclosed in quotation marks like string literals are. This means you can use dot notation to access only property keys that are valid [identifiers](https://web.dev/learn/javascript/data-types/variable):

```
const myObj = {
    "1": true,
    "key with spaces": true
};

myObj.1;
> Uncaught SyntaxError: unexpected token: numeric literal

myObj.key with spaces;
> Uncaught SyntaxError: unexpected token: keyword 'with'
```

Because of this, it's best practice to follow [identifier rules](https://web.dev/learn/javascript/data-types/variable) when specifying property keys whenever possible. If this isn't possible for a given key, an alternate _bracket notation_ syntax lets you set and access string-based object keys that don't follow identifier rules.

## Bracket notation

Bracket notation uses a set of brackets (`[]`) containing a value that evaluates a string (or a [Symbol](https://web.dev/learn/javascript/data-types/symbol)) representing the property key.

```
const myObj = {
    "myProp": "String value."
};

myObj["myProp"];
> "String value."
```

This syntax is considerably more permissive, and potentially permissive enough to be confusing, because the value in brackets is evaluated as a string literal regardless of its data type. For example, here the boolean value `false` and the number value `10` are used to access properties associated with the string literal keys `"false"` and `"10"` :

```
const myObj = {
    "false": 25,
    "10" : true,
    "key with spaces": true
};

myObj[false];
> 25

myObj[10];
> true

myObj["key with spaces"];
> true
```

The strength of this syntax is in its flexibility, allowing the use of dynamically-created strings to access properties. The following example uses a random number to select one of an object's three properties:

```
const colors = {
    "color1" : "red",
    "color2" : "blue",
    "color3" : "green"
};
const randomNumber = Math.ceil( Math.random() * 3 );

colors[ "color" + randomNumber ];
> "blue"
```

As with dot notation, you can use bracket notation to both access and create new properties, using [assignment operators](https://web.dev/learn/javascript/data-types/variable#declaration):

```
const myObj = {};

myObj[ "myProp" ] = "String value.";

myObj;
> Object { myProp: "String value." }
```

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
