# Extend classes  |  web.dev

**Source URL:** [https://web.dev/learn/javascript/classes/extends?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fclasses%2Fextends](https://web.dev/learn/javascript/classes/extends?continue=https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%23article-https%3A%2F%2Fweb.dev%2Flearn%2Fjavascript%2Fclasses%2Fextends)  
**Last Updated:** 2025-05-23T01:13:01.172Z  
**Extracted:** 2025-05-31 16:58:10

---

# Extend classes  |  web.dev

Extend classes

bookmark\_border Stay organized with collections Save and categorize content based on your preferences. bookmark\_border Stay organized with collections Save and categorize content based on your preferences.

The `extends` keyword is used in class declarations or expressions to create a class that acts as a subclass of another, with the parent class (sometimes called the "base class") serving as the prototype of the child class (sometimes called the "subclass" or "derived class").

```
class ParentClass {}
class ChildClass extends ParentClass {}

Object.getPrototypeOf( ChildClass );
> class ParentClass {}
```

These subclasses inherit the properties and methods of the parent class. This lets you extend the core functionality of a class to serve more specific purposes without overloading the parent class to suit every possible use case, or reimplementing code that serves a similar purpose.

Child classes can provide their own implementations of the methods inherited from a parent class:

```
class MyClass {
  constructor( myPassedValue ) {
    this.instanceProp = myPassedValue;
  }
  classMethod() {
    console.log( `The value was '${ this.instanceProp }.'`)
  }
}
class ChildClass extends MyClass {
  classMethod() {
    console.log( `The value was '${ this.instanceProp },' and its type was '${ typeof this.instanceProp }.'`)
  }
}

const myParentClassInstance = new MyClass( "My string." );
const mySubclassInstance = new ChildClass( 100 );

myParentClassInstance.classMethod();
> "The value type was 'string.'"

mySubclassInstance.classMethod();
> "The value was '100,' and its type was 'number.'"
```

You can also call methods defined on the parent class in the context of the child class using `super`:

```
class MyClass {
  constructor( myPassedValue ) {
    this.instanceProp = myPassedValue;
  }
  classMethod() {
    console.log( `The value was '${ this.instanceProp }.'`)
  }
}

class ChildClass extends MyClass {
  subclassMethod() {
    super.classMethod();
    console.log( `The value type was '${ typeof this.instanceProp }.'`)
  }
}
const mySubclassInstance = new ChildClass( 100 );

mySubclassInstance.subclassMethod();
> The value was '100.'
> The value type was 'number.'
```

As seen in the previous examples, when the `constructor()` method is omitted in the context of a child class, JavaScript's implicit constructor calls the parent constructor along with the same set of arguments. However, if there's a constructor in the subclass, it must first call `super()` along with any necessary arguments before referencing `this`.

```
class MyClass {
  constructor( myPassedValue ) {
    this.instanceProp = myPassedValue;
  }
  classMethod() {
    console.log( `The value was '${ this.instanceProp }.'`)
  }
}

class ChildClass extends MyClass {
    constructor( myPassedValue ) {
        super( myPassedValue );
        this.modifiedProp = myPassedValue + 50;
    }\
    subclassMethod() {
        super.classMethod();
        console.log( `The value type was '${ typeof this.instanceProp }.'`)
    }
}
const mySubclassInstance = new ChildClass( 100 );

mySubclassInstance;
> MyClass { instanceProp: 100, modifiedProp: 150 }
```

Getters and setters are special methods used exclusively to retrieve and define values, respectively. Methods defined using the `get` and `set` keywords lets you create methods that can be interacted with as if they were static properties.

```
class MyClass {
    constructor( originalValue ) {
        this.totalValue = 0;
    }
    set doubleThisValue( newValue ) {
        this.totalValue = newValue * 2;
    }
    get currentValue() {
        console.log( `The current value is: ${ this.totalValue }` );
    }
}
const myClassInstance = new MyClass();

myClassInstance;
> MyClass { totalValue: 0 }

myClassInstance.doubleThisValue = 20;

myClassInstance.currentValue;
> The current value is: 40
```

`get` and `set` properties are defined on the prototype property of the class, and are therefore available to all instances of the class.

## Check your understanding

Select the true statements about classes created with the `extends` keyword.

It inherits the properties and methods of its parent class.

It acts as the child of the class it extends.

It acts as the parent of the class it extends.

`It can't overwrite methods from a parent class.`

---

*This documentation was extracted from the database for URLs containing 'web.dev'*
