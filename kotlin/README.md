# Kotlin Learning Module
**This is me putting http://kotlinlang.org/docs/reference in my own words for my learning purposes. I take no credit for the information on this page**
#Basic Types
* Long: tagged with `L` at the end, `123L`
* Hex: prefixed with `0x` and represented using capital letters, `0x0F`
* Binary: prefixed with `0b`, `0b01101`
* Floats: postfixed with `f`, `234.124f`

Numbers can be interpolated with underscores for increased readability that leave no effect, `1_234_567` == `1234567`

Primitive datatypes behave as JVM variables, however nullable primitive types, `Int?`, and generics are not considered primitive datatypes.
`==` checks for value equality
`===` checks for reference equality

#Classes
Instantiation does not require the `new` keyword.

## Constructors

#### Primary Constructors
Goes in the method signature, either with the constructor keyword
```aidl
class Person contructor(name: String, age: Int) {}
```
or with the constructor keyword omitted
```aidl
class Person(name: String, age: Int) {}
```

To adjust visibility of the primary constructor, the `@inject` annotation, and the `constructor` keyword must be used
```aidl
class Person public @Inject constructor (name: String, age: String)
```

There can be no code in the constructor.
The initialization block, keyword `init`, is used to execute any code that would be executed in the constructor.
Properties are directly set using the constructor parameters inside the class

```
class Person(name: String, age: Int) {
    init() {
        if (name.isProfanity()) {
            throw ProfanityException()
        }
    }
    
    val name = name
    val age = age
}
```
or properties are set inside the constructor itself
```aidl
class Person(val name: String, age: Int) {
    init() {
        if (name.isProfanity()) {
            throw ProfanityException()
        }
    }
}
```

#### Secondary Constructors
Secondary constructors are declared inside the class with the keyword `constructor`.
If the class has a primary constructor, all secondary constructors must delegate to that primary constructor;
either through other secondary constructors, or directly using the `this` keyword.
```aidl
class person(val name: String) {
    constructor(name: String, parent: Person) : this(name) {
        parent.children.add(this)
    }
}
```

> NOTE
>
> The init block is always run before the secondary constructor.

## Inheritance
Any is the default superclass for a class with no subtypes.

#### Raw Strings
Strings surrounded by """ do not need escape characters.

#### Default Parameters
This is used when you want a function to have default parameters when omitting some arguments in the function call.
This can be very useful where a long chain of Java overloading constructors would usually be implemented.

```
fun testFunction: String (necessaryArg: String, optionalArg: String = "This is the default value") {
    // do something
}
```

#### Apply
Useful when you want to initialize an object and set some fields within that object.

```
val myObject = MyObject()
myObject.arg1 = "arg1"
myObject.arg2 = "arg2"

---Is equivalent to---

val myObject = MyObject().apply {
    arg1 = "arg1"
    arg2 = "arg2"
}
```