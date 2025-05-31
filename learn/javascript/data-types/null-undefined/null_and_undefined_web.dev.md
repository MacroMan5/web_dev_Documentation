# null and undefined  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/data-types/null-undefined?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fnull-undefined](https://web.dev/learn/javascript/data-types/null-undefined?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fdata-types%2Fnull-undefined)  
**Last Updated:** 2025-05-23T01:11:41.460Z  
**Extracted:** 2025-05-31 16:58:10

---

# null and undefined | web.dev

null and undefined

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

JavaScript has multiple ways of indicating the absence of a value. This page describes the two most common ways: the `null` and `undefined` data types.

The `null` keyword represents an intentionally defined absence of value. `null` is a primitive, although the `typeof` operator returns that `null` is an object. This is an [error](https://2ality.com/2013/10/typeof-null.html) that has carried over from the first version of JavaScript and been left intentionally unaddressed to avoid breaking expected behavior across the web.

```
typeof null
> object
```

You might define a [variable](https://web.dev/learn/javascript/data-types/variable) as `null` with the expectation that it reflects either a value assigned to it at some point in a script or an explicitly absent value. You can also assign the `null` value to an existing reference to clear a previous value.

## `undefined`

`undefined` is a primitive value assigned to [variables](https://web.dev/learn/javascript/data-types/variable) that have just been declared, or to the resulting value of an operation that doesn't return a meaningful value. For example, this can happen when you declare a function in a browser's developer console:

```
function myFunction() {}
> undefined
```

A function explicitly returns `undefined` when its [`return` statement](https://web.dev/learn/javascript/functions/return) returns no value.

```
(function() {
    return;
}());
> undefined
```

## Comparison of `null` and `undefined`

Although `undefined` and `null` have some functional overlap, they have different purposes. In the strictest sense, `null` represents a value intentionally defined as "blank," and `undefined` represents a lack of any assigned value.

`null` and `undefined` are [loosely equal, but not strictly equal](https://web.dev/learn/javascript/comparison#type-coercion-equality). The loose equality operator coerces operands of different types to boolean values, making `null` and `undefined` both `false`. The strict equality operator considers operands of different data types to be unequal.

```
null == undefined
> true

null === undefined
> false
```

Unlike the reserved keyword `null`, `undefined` is a property of the [global object](https://web.dev/learn/javascript/data-types/variable#global-scope). This was a design decision made early in JavaScript's development, and it let legacy browsers overwrite `undefined` completely. In modern browsers, it's still possible to use `undefined` as an identifier in non-global scopes, overriding its value within the scope of that declaration. **Never** use `undefined` as an identifier. It can cause unexpected behaviors and is likely to confuse future maintainers of your codebase.

## Check your understanding

What does `typeof null` return?

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
