# BigInt  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/data-types/bigint?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fbigint](https://web.dev/learn/javascript/data-types/bigint?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fbigint)  
**Last Updated:** 2025-05-23T01:11:49.245Z  
**Extracted:** 2025-05-31 16:58:10

---

# BigInt  |  web.dev

BigInt

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

BigInt primitives are a [relatively new addition](https://caniuse.com/bigint) to JavaScript, allowing mathematical operations on numbers outside the range allowed by `Number`. To create a BigInt, append `n` to the end of a number literal, or pass an integer or numeric string value to the `BigInt()` function.

```
const myNumber = 9999999999999999;
const myBigInt = 9999999999999999n;

typeof myNumber;
> "number"

typeof myBigInt;
> "bigint"

myNumber;
> 10000000000000000

myBigInt;
> 9999999999999999n
```

In this example, `9999999999999999` is outside the range of digits that can be safely represented by `Number`, causing a rounding error.

BigInt values don't inherit the methods and properties by the `Number` object provides, and they can't be used with the methods JavaScript's built-in `Math` object provides. Most importantly, you can't mix BigInt and Number primitives in standard arithmetic operations:

```
9999999999999999n + 5
> Uncaught TypeError: can't convert BigInt to number
```

To do arithmetic with BigInts, you must define both operands as BigInt values:

```
console.log( 9999999999999999 + 10 );  // Off by one
> 10000000000000010

console.log( 9999999999999999n + 10n );
> 10000000000000009n
```

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
