## Kotlin Constructors
Constructors is a special member function that is called when an object is instantiated (Created). However, how they work in Kotlin is slightly different. 

In Kotlin, there are two constructors:
 - Primary constructor - concise way to initialize a class
 - Secondary constructor - allows you to put additional initialization
   logic
### Primary Constructor
The primary constructor is part of the class header.

    class Person(val firstName: String, var age: Int) {
        // class body
    }
Here the block of code surrounded by parentheses is the primary constructor. 

> The primary constructor has a constrained syntax, and cannot contain
> any code. So in that case we are using the **initializer block/init
> block** for the  initilization of  code (not only code to initialize
> properties).
### Secondary Constructor
A class can also contain one or more secondary constructors. They are created using `constructor` keyword.

Secondary constructors are not that common in Kotlin. The most common use of secondary constructor comes up when you need to extend a class that provides multiple constructors that initialize the class in different ways.

    class Log {
        constructor(data: String) {
            // some code
        }
        constructor(data: String, numberOfData: Int) {
            // some code
        }
    }
Here, the `Log` class has two secondary constructors, but no primary constructor.

    class AuthLog: Log {
        constructor(data: String): super(data) {
            // code
        }
        constructor(data: String, numberOfData: Int): super(data, numberOfData) {
            // code
        }
    }
Here, constructors of the derived class `AuthLog` calls the corresponding constructor of the base class `Log`. For that, `super()` is used.

    class AuthLog: Log {
        constructor(_data: String): this("From AuthLog -> " + _data, 10) {
        }    
        constructor(_data: String, _numberOfData: Int): super(_data, _numberOfData) {
        }
    }
Here one constructor called from another constructor of the same class using  `this()`


## Sealed Classes
Sealed classes are used for representing restricted class hierarchies, when a value can have one of the types from a limited set, but cannot have any other type.They are, in a sense, an extension of enum classes: the set of values for an enum type is also restricted, but each enum constant exists only as a single instance, whereas a subclass of a sealed class can have multiple instances which can contain state. To declare a sealed class, you put the sealed modifier before the name of the class. A sealed class can have subclasses, but all of them must be declared in the same file as the sealed class itself. A sealed class is abstract by itself, it cannot be instantiated directly and can have abstract members.
