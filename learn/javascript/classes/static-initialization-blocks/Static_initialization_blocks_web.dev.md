# Static initialization blocks  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/classes/static-initialization-blocks?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fclasses%2Fstatic-initialization-blocks](https://web.dev/learn/javascript/classes/static-initialization-blocks?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fclasses%2Fstatic-initialization-blocks)  
**Last Updated:** 2025-05-23T01:11:07.376Z  
**Extracted:** 2025-05-31 16:58:10

---

# Static initialization blocks | web.dev

Static initialization blocks

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

Static initialization blocks are a very new JavaScript feature, standardized in ECMAScript 2022 and only supported in [modern browsers](https://caniuse.com/mdn-javascript_classes_static_initialization_blocks). Static initialization blocks let you set the value of static fields dynamically, using logic that spans multiple statements.

To create a static initialization block, use the `static` keyword followed by a [block statement](https://web.dev/learn/javascript/introduction#block-statements) in curly brackets (`{}`):

```
class MyClass {
  static {}
}
```

This pattern lets you initialize or alter static fields declared in the body of the class:

```
class MyClass {
  static firstProperty = 'First property.';
  static secondProperty;
  static {
    this.secondProperty = 'Second property.';
  }
}

MyClass.secondProperty;
"Second property."
```

These statements are evaluated at the time a class is first _initialized_, that is, when the JavaScript engine first evaluates it, not when an instance of a class is created, as with `constructor()`:

```
class MyClass {
    static {
        console.log( "Static initialization block." );
    }
    constructor() {
        console.log( "Constructor." );
    }
}
> "Static initialization block."

const myClassInstance = new MyClass();
> "Constructor."
```

A class can contain multiple static initialization blocks, and those blocks are evaluated in the order they're declared, alongside any other static fields and methods. This means that only the fields declared before a static initialization block are available in that block:

```
class MyClass {
  static myNewField;
  static {
    this.myNewField = this.myField;
  }
  static myField = "My value.";
};

MyClass.myNewField;
> undefined

class MyCorrectedClass {
  static myNewField;
  static myField = "My value.";
  static {
    this.myNewField = this.myField;
  }
};

MyCorrectedClass.myNewField;
> "My value."
```

## Check your understanding

Which of the following statements are true?

A class can only contain one static initialization block.

Static initialization blocks are evaluated when the class is first initialized.

Fields declared after a static initialization block are available inside the block.

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
