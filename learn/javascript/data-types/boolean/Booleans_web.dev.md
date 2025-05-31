# Booleans  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/data-types/boolean?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fboolean](https://web.dev/learn/javascript/data-types/boolean?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fboolean)  
**Last Updated:** 2025-05-23T01:11:40.264Z  
**Extracted:** 2025-05-31 16:58:10

---

# Booleans  |  web.dev

Booleans

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

The boolean primitive is a logical data type with only two values: `true` and `false`.

## Boolean object

All values in JavaScript are implicitly `true` or `false`. The `Boolean` object can be used to [coerce](https://web.dev/learn/javascript/introduction#weak-typing) a value to a `true` or `false` boolean, based on the implicit true or false state of that value:

```
Boolean( "A string literal" );
> true
```

Values that result in `false` include `0`, `null`, `undefined`, `NaN`, an empty string (`""`), an omitted value, and a `false` boolean. All other values result in `true`.

```
Boolean( NaN );
> false

Boolean( -0 );
> false

Boolean( 5 );
> true

Boolean( "false" ); // the value `"false"` is a string, and therefore implicitly true.
> true
```

Avoid using the `Boolean` object as a constructor. It creates an _object_ containing a boolean value, not the boolean primitive you might expect:

```
const falseBoolean = Boolean( 0 );
const falseObject = new Boolean( 0 );

console.log( falseBoolean  );
> false

console.log( falseObject  );
> Boolean { false }

falseObject.valueOf();
> false
```

Because all objects are inherently [truthy](https://web.dev/learn/javascript/comparison#truthy-falsy), the resulting boolean object always loosely evaluates to true, even if it contains a `false` value:

```
const falseBoolean = Boolean( 0 );
const falseObject = new Boolean( 0 );

console.log( falseBoolean == true );
> false

console.log( falseObject == true );
> false

console.log( !!falseObject );
> true
```

## Check your understanding

Which of the following returns `false`?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
