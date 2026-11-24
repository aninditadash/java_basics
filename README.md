# Introduction to Java

Java is a high-level, object-oriented programming language used to build web apps, mobile applications, and enterprise software systems. It is platform-independent, which means we can write code once and run it anywhere using the Java Virtual Machine (JVM) (**Write Once, Run Anywhere**). Widely used programming language and platform. A platform is an environment where we can develop and run programs written in any programming language. 

## **Datatypes in Java**

Java is statically typed where variable types are known at compile time, which allows compilers to catch type-related errors early on, potentially preventing runtime crashes and improving code reliability.

**Primitive Data Types:** Stores only single values, have fixed size and are stored in stack memory. Eight primitive data types:

- Integer Types: `byte`: 1 byte (8 bits), `short`: 2 bytes (16 bits), `int`: 4 bytes (32 bits) (default), `long`: 8 bytes (64 bits).
- Floating-Point Types: `float`: 4 bytes (32 bits) - Single-precision, `double`: 8 bytes (64 bits) - Double-precision (default). _Precision refers to the format and amount of space occupied by the relevant type._ Should not be used for precise and accurate calculations. (use BigDecimal)
- Character Type: `char` - single 16-bit Unicode character with the size of 2 bytes (16 bits). Unicode range (0 to 65535).
- Boolean Type: `boolean` - typically 1 byte (actual size can vary depending on JVM). Stores true or false.

**Why Java char size is 2 bytes:** Unlike languages such as C/C++ that use the _ASCII character set_ (7-bit code), Java uses the _Unicode character set to support internationalization_. Unicode requires more than 8 bits to represent a wide range of characters from different languages. As a result, Java uses char size of 2 bytes to represent any Unicode character.

**Overflow and Underflow in Java:** Refers to runtime conditions which occur when result of an arithmetic operation falls outside the permissible boundaries of a primitive data type. Java does not throw exceptions or crash when this happens to primitive numbers since it performs _integer-wraparound_. For Integers, when you exceed the upper limit, the value wraps around to the lowest negative number and vice versa. Floating-point numbers do not wrap around, if value becomes too large (positive or negative), it converts to Infinity or -Infinity and when a number gets too low, it rounds down to 0.0.

**Type casting in Java:** Process of converting a value from one datatype into another. Primitive Casting (for numeric and character types) and Reference/Object Casting (for classes that share an inheritance relationship).

Primitive Type Casting: `byte -> short -> char -> int -> long -> float -> double`. Widening (Implicit casting): Smaller to larger size performed by compiler and no data (int -> double). Narrowing (Explicit casting): Larger to smaller size, done by adding datatype in paranthesis and risk of data loss (double -> int).

Reference (Object) Casting: Allows an object to be an instance of either a parent class (superclass) or a child class (subclass) only if the two classes are connected by inheritance (using `extends` or `implements`). Upcasting (Implicit): Converting a subclass reference to a superclass reference, happens automatically because a child class "is-a" version of the parent. Downcasting (Explicit): Converting a superclass reference back into a subclass reference, done manually. However if the object is not actually an instance of that subclass at runtime, Java throws a `ClassCastException` (always check an object's actual type using the `instanceof` operator before downcasting).

**In Java, a `char` variable can be assigned a value in several ways:** 

- Using a character literal.
- Using an integer literal representing a _Unicode_ value: char takes 2 bytes (16-bit UTF encoding ), while int takes 4 bytes (32-bit). Here, we need to typecast the int to get converted to a char. Every character has its own unique code called a Unicode value, which is represented by a numeric value. Here, we convert the numerical value to its equivalent ASCII representation.
- Using a Unicode escape sequence: we can directly specify the Unicode value using a `\u` escape sequence followed by four hexadecimal digits.

```java
char myChar1 = 'A';
char myChar2 = 65; // 65 is the Unicode value for 'A'
char myChar3 = '\u0041'; // \u0041 is the Unicode escape sequence for 'A'
```

In Java, the **`L` (or l) suffix is required when assigning a literal integer value that exceeds the range of an int to a long variable**. When trying to assign an integer literal larger than Integer.MAX_VALUE to a long variable without the L suffix, the compiler will interpret that literal as an int. Since the value exceeds the int range, it will result in a compile-time error because of an integer overflow.

```java
// 2147483647 -> Integer.MAX_VALUE
long longIntegerNum = 2147483648; // Error: The literal 2147483648 of type int is out of range 
long longIntegerNumL = 2147483648L; // Works fine
```

**Wrapper classes in Java:** provides an object representation for each of the eight primitive data types. These classes are part of the `java.lang` package and allow primitive values to be used in object-only contexts like Java Collections/Serialization (which allow only object data) and provide feature of `autoboxing` (primitive to object) - Java compiler automatically converts a primitive type into its corresponding wrapper class object when assigned directly and `unboxing` (object to primitive) - Java compiler automatically extracts the primitive value from a wrapper object when assigned to a primitive variable. These wrapper classes also include helpful methods like `parseInt()`, `compareTo()`, `equals()`, `toString()`, etc.

---

**Non-Primitive (Reference) Data Types:** These data types do not directly store values but instead store references (memory addresses) to objects. Objects are stored on the heap memory and references to these objects (local variables referencing these objects) are stored in stack memory. 

**`null` in Java:** `null` is a reserved keyword that denotes a variable or attribute that has a type but doesn't reference any object. Essentially, `null` signifies the absence of an instance/object associated with that variable or field.

**Strings in Java:** String is an object that represents a sequence of characters, every character is stored in 16 bits, i.e., using UTF 16-bit encoding. Two ways to create a string: using string literal and using new keyword. Strings are immutable meaning their values cannot be changed once they are created, so updating the string does not modify the original one, it creates a new string object instead.

```java
String str1 = "Hello";
String str2 = new String("Hello");
```
Java checks the String Constant Pool (a special memory region inside the heap). If the string "Hello" already exists, str1 reuses the existing instance. If it does not exist, Java creates a new one in the pool. Using new keyword forces Java to bypass the pool check and always create a brand-new object in the normal heap memory, even if "Hello" already exists in the pool. So, here _string interning_ allows JVM to reuse existing string objects.

Strings are frequently used to store sensitive data like passwords, usernames, and file paths, so immutability ensures that once these values are set, they cannot be accidentally or maliciously altered by other parts of the program, enhancing security.

In a multi-threaded environment, mutable objects can lead to race conditions and data corruption if multiple threads try to modify them concurrently without proper synchronization. Since String objects are immutable, they are inherently thread-safe and can be shared across threads without requiring explicit synchronization mechanisms. When a thread tries to "update" the value of a string, the thread does not actually modify the original object; instead, it creates an entirely new String object in memory, and other threads looking at it will see no change at all. Mutable Alternatives are StringBuilder and StringBuffer. StringBuilder used for single-threaded tasks because it is faster and not synchronized. StringBuffer is safe for multi-threaded applications because its methods are synchronized.

`==` is used to compare object references, while `.equals()` is used to compare the content of the strings. `isEmpty()` checks if a string contains no characters at all. It returns true only if the string's length is zero. But if the string contains whitespace characters (spaces, tabs, newlines, etc.), it will return false. `isBlank()` method provides a more comprehensive check for "blankness." It returns true if the string is either empty (has a length of zero) or consists of only whitespace characters.

## **OOP(Object Oriented Programming) in Java**

Object-Oriented Programming (OOPs) is a programming approach that organizes code into classes and objects and makes it more structured and easy to manage. The core idea of OOPs is to bind data and the functions that operate on it, preventing unauthorized access from other parts of the code. A class is a blueprint that defines properties and behaviors of an entity, while an object is an instance of that class representing the real-world entity. In Java, the `Object` class (`java.lang.Object`), is the root of the entire class hierarchy . 

**Instance Variables:** non-static and are declared in a class outside of any method, constructor, or block. Scope is throughout the class except static contexts. Its lifetime lasts as long as the object stays in memory - these variables are created when the object is created and destroyed when the object is destroyed. Default value is assigned when not initialized (e.g. String/Wrapper classes - null, float - 0.0f, etc). Can be initialised through constructors/instance blocks.

**Static Variables:** class variables declared using static keyword and only one copy of static variable is available for a class. Its lifetime is same as that of the class, its scope is restricted by the access modifier used. When accessing a static variable through an object, compiler will show a warning message, but will replace the object name with the class name automatically. Static variables cannot be declared locally inside an instance method. Static blocks can be used to initialize static variables.

Static variables and static and instance methods are stored in `Method Area`/`Class Area` where as objects are stored in the heap memory. This part of JVM memory is shared across all threads. When a Java program is executed, JVM loads the class into memory and static variables of this class are initialized in the Method area. These variables remain in memory until the program terminates.

**Static/Non-static Methods:** are commonly used for utility functions that perform a specific operation, also can be used for Factory methods that create instances of a class, or methods that perform a global operation that affect all instances of a class. _How to access instance variables/methods from a static method:_ create an instance of the class and call the method/access the variable through the instance. Instance methods can however access the static variables/methods directly without any issues.

**Scope vs Lifetime:** scope defines where in the code a variable can be accessed, while lifetime defines how long that variable exists in memory during program execution. 

**Method Signature and Method Overloading:** In Java, a method signature is uniquely defined by the method's name and its parameter list (specifically the number, data types, and exact order of the parameters). Return Type, access modifiers, parameter names and thrown exceptions are not part of the method signature. Java compiler enforces that every method within a class must have a unique method signature - this forms the basis for `Method Overloading` - creating multiple methods with the same name but different parameters.

- **Compile-time vs. Runtime:** Overloading is 100% static (compile-time) using declared types.
- **Three-Phase Resolution:** Strict (widening) → Loose (boxing) → Varargs.
- **Specificity Rule:** Subtypes beat supertypes; sibling types cause ambiguity errors.
- **Bytecode Erasure:** Generic parameters erase to raw types, causing signature collisions at the JVM level.

```java
void display(int a)          // Signature: display(int)
void display(String b)       // Signature: display(String) -> Valid (different type)
void display(int a, float b) // Signature: display(int, float) -> Valid (different count)
void display(float b, int a) // Signature: display(float, int) -> Valid (different order)
```

- **The null Literal & Most Specific Type Resolution:** Passing null to overloaded methods with unrelated or sibling reference types results in compile-time error. For below example, compiler looks for the most specific `process()` method to be invoked. Since, `Integer` and `String` are both subtypes of `Object` but are not subtypes of each other, then the compiler cannot choose a winner and hence gives error. Now, if we remove the `Integer` method, then `process()` will call the string representation.

```java
public class NullTrap {
    static void process(Object o) { System.out.println("Object"); }
    static void process(String s) { System.out.println("String"); }
    static void process(Integer i) { System.out.println("Integer"); }

    public static void main(String[] args) {
        process(null); // What happens?
    }
}
```

- **Widening vs. Autoboxing vs. Varargs (The 3-Phase Rule):** Calling an overloaded method with a primitive literal when exact matches do not exist. Below example prints Widening. To preserve backward compatibility, compiler resolves overloaded methods in three strict phases: Phase 1 (Strict Invocation): Widening primitive conversions (int → long), without boxing or unboxing. Phase 2 (Loose Invocation): Autoboxing/unboxing (int → Integer), followed by widening reference conversions (Integer → Number → Object). Phase 3 (Variable Arity): Varargs (int...).

```java
public class PrecedenceTrap {
    static void handle(Integer i) { System.out.println("Autoboxing"); }
    static void handle(long l)    { System.out.println("Widening"); }
    static void handle(int... v)  { System.out.println("Varargs"); }

    public static void main(String[] args) {
        handle(5); // Output?
   }
}
```
- However, for above example, compile-time error will come if `static void handle(Long l)` is the sole method available for `handle(5)`: compiler tries all three resolution phases on `handle(Long)` and fails every single one: Phase 1 (Widening only): fails because Long is a reference type, not a primitive. Phase 2 (Boxing + Reference Widening): Boxes 5 (int) into Integer. It then tries to widen Integer to Long, which fails because Integer and Long are sibling classes under Number (not parent-child). Phase 3 (Varargs): Fails because Long is not a varargs parameter.

- **Type Erasure Collisions in Generics:** Overloading methods that differ only by generic type arguments. Result is compile-time error (both methods have same erasure). After type erasure, both methods have the exact same bytecode descriptor. Even though the source code signatures look distinct, the JVM cannot differentiate them at runtime.

```java
public class ErasureTrap {
    public void sort(List<String> list) { }
    public void sort(List<Integer> list) { } // Compile error?
}
```

- **Primitive char Widening vs. Byte/Short:** Passing a char literal to overloaded numeric methods. Prints `int`. `char` is an unsigned 16-bit integer (0 to 65,535), whereas `short` is a signed 16-bit integer (-32,768 to 32,767). Because `short` cannot represent all `char` values, `char` does not widen to `short` — it widens directly to `int`. Now, `byte` is misleading here and has no purpose.

```java
public class CharTrap {
    static void test(byte b)  { System.out.println("byte"); }
    static void test(short s) { System.out.println("short"); }
    static void test(int i)   { System.out.println("int"); }

    public static void main(String[] args) {
        test('a'); // Output?
    }
}
```

**`main` method in Java:** `main()` has `public` and `static` modifiers and acts as the entry point of the application. `public` modifier facilitates access to this method to the JVM. Creating and managing objects is one of JVM's primary functions. Declaring it as `static` lets JVM invoke it directly using `ClassName.main()` without needing to instantiate the class first.

---

**Components of Java classes and objects:**  _Access Modifiers_ are used to control the visibility of the variables, methods and classes within a class or package. A class can only _extend/inherit_ another class using `extends` keyword. A class can _implement_ a list of interfaces using `implements` keyword. _Fields_ are variables defined within a class that hold the data/object state. _Constructor_ is a special method in a class with name same as class name and is automatically invoked by JVM when an object is created. _Objects_ are instances of a class that have their state represented by attributes, behaviour represented by the methods and identity represented by its name which enables it to interact with other objects. We can't create objects of an abstract class or an interface. `new` operator/bytecode instruction instantiates a class by allocating memory for a new object and returning a reference to that memory. It also invokes the constructor method. We also have _instance initializers_ and _static intializers_.

**Constructors in Java:** They help in object creation and are invoked by JVM when an object is created. Purpose is to initialize the object's state by assigning values to the declared properties. Access level of the default constructor (generated by Java Compiler) will be same as the access level of the class and if we don't explicitly provide any constructor, compiler will add a default, no-argument constructor. A constructor in Java can not be abstract, final, static, or Synchronized. Access modifiers can be used in constructor declaration to control its access. Types of constructors: 
_Default Constructor:_ automatically created by Java compiler if no other constructor is defined, its not created if a parameterised/no-arg constructor is defined. _Parameterized Constructor:_ A constructor with parameters. _Copy Constructor:_ used to create objects in other ways e.g., create a new object from an existing one, so we can pass another object to this constructor which will copy the data from the passed object to the newly created object.

**Constructor Chaining:** `this` keyword is used in constructor chaining where we invoke one constructor from another. We must follow 3 rules when calling one constructor from another: the call to another constructor must be the first line in the constructor, a constructor cannot call itself, same constructor cannot be called more than once. To chain a superclass constructor we have to use `super` instead of `this`. `this` or `super` expression should always be the first statement.

**Instance Initialization Block (IIB):** a nameless { ... } block inside a class — to run instance setup code every time an object is created, before the constructor body executes. Primary purpose is to intialize instance variables of an object. Multiple initialisation blocks executed in order as defined in the class definition. Cannot have a return statement.

**Static Initialization Block:** block of code that is associated with a class rather than with instances and executed when the class is loaded by JVM for the first time (executed only once). Primary purpose is to intialize static variables of a class. Defined as a nameless block with static { ... } keyword. Useful when we need to perform one-time intialization for static variables or when the initialization logic is complex and cannot be accomodated within a single line. Multiple static blocks executed in order as defined in the class definition. The java command tries to load the definition of class before it executes `main()`, at this time when class is initialized, its static initializer will be executed, hence static initializer code is executed before `main()` is called. 

__Anonymous Objects in Java:__ are objects that are instantiated without storing their reference in a variable. They are used for one-time operations (e.g., method calls) and are discarded immediately after use.

- No reference variable: Cannot reuse the object.
- Created & used instantly: Saves memory for short-lived tasks.
- Common in event handling (e.g., button clicks).


### **Access Modifiers**

Access modifiers in Java are used to enforce the level of accessibility or visibility of the variables, classes, and methods within a class or package. There are different types of access modifiers that are used to define the accessibility in different ways.

- __public Access Modifier:__ provides the highest access among all the modifiers. We can access it anywhere in the package. The public modifier allows to use the variable, methods and class to access in the same package.
- __protected Access Modifier:__ allows the class, method and variable to be accessible within the same package and subclasses.
- __private Access Modifier:__ used with method, class and variable and it can be only accessible in the class where it is defined.
- __default Access Modifier:__ When the modifier is not defined (variable, method or class) then it is specified as default method or package private, having accessibility within the same package.

The following rules for inherited methods are enforced −

- Methods declared public in a superclass also must be public in all subclasses.
- Methods declared protected in a superclass must either be protected or public in subclasses; they cannot be private.
- Methods declared private are not inherited at all, so there is no rule for them.

<img src="https://usemynotes.com/wp-content/uploads/2021/02/what-are-access-specifiers-in-java.jpg" width=700 />

### **Method Modifiers**

In addition to access modifiers, methods have other modifiers.

- __abstract:__ When you declare a method abstract, a method body is always omitted. An abstract method can only be declared on an abstract class or an interface.
- __static:__ Sometimes called a class method, rather than an instance method, because it's called directly on the Class instance.
- __final:__ A method that is final cannot be overridden by subclasses.
- __default:__ Only applicable to an interface.
- __synchronized:__ This modifier manages how multiple threads will access the code in this method.

## **Encapsulation**

Defined as the wrapping up of data and functionality under a single unit. It is the mechanism of bundling attributes (fields) and behaviour (methods) together within a single object (Class). It involves the practice of hiding certain fields and methods from public access using access modifiers like `private`, `protected`, etc. It also restricts direct access to an object's internal state, allowing interaction only through defined `public` methods (getters and setters).

- __Data Hiding:__ The internal data of an object is hidden from the outside world, preventing direct access.
- __Data Integrity:__ Only validated or safe values can be assigned to an object’s attributes via setter methods.
- __Reusability:__ Encapsulated code is more flexible and reusable for future modifications or requirements.
- __Security:__ Sensitive data is protected as it cannot be accessed directly.

## **Abstraction**

Data Abstraction is the property by virtue of which only the essential details are displayed to the user. It is the process of showing only essential information and hiding the complex implementation details. In Java, abstraction is achieved using abstract classes and interfaces, allowing you to define a common interface without specifying the full implementation. Java provides two ways to implement abstraction: Abstract Classes (Partial Abstraction), Interface (100% Abstraction).

### __Abstract Classes and Abstract Methods__

- An abstract class is a class that is declared with an abstract keyword.
- An abstract method is a method that is declared without implementation.
- An abstract class may have both abstract methods (methods without implementation) and concrete methods (methods with implementation).
- Any class that contains one or more abstract methods must also be declared with an abstract keyword.
- We can have an abstract class without any abstract methods. This allows us to create classes that cannot be instantiated but can only be inherited. 
- There can be no object of an abstract class. That is, an abstract class can not be directly instantiated with the new operator.
- An abstract class can contain constructors, which are called when an instance of an inherited class is created.
- Concrete classes are those that extend the abstract class or implement the interface and should contain the program logic.
- Abstract classes can also have final methods (methods that cannot be overridden).
- An abstract method in an abstract class can not be declared as final, as it will yield an error: "Illegal combination of modifiers: abstract and final".
- If the Child class is unable to provide implementation to all abstract methods of the Parent class then we should declare that Child class as abstract so that the next level Child class should provide implementation to the remaining abstract methods.
- Similar to the interface we can define static methods in an abstract class that can be called independently without an object.
- So, an abstract class can have a main method, as the main method in Java is a static method.

### **Interface**

An Interface is defined as an abstract type used to specify the behaviour of a class. An interface in Java is a blueprint of a behaviour. A Java interface contains static constants and abstract methods. Apart from abstraction, interfaces can also be used to implement multiple inheritance in Java. Its more like a contract between the class and client code which the compiler enforces.

- By default, variables in an interface are public, static, and final.
- It supports loose coupling (classes depend on behavior, not implementation).
- In other words, interfaces primarily define methods that other classes must implement.
- An interface in Java defines a set of behaviours that a class can implement, usually representing an IS-A relationship, but not always in every scenario.
- All interface declarations should have the public or default access modifier; the abstract modifier will be added automatically by the compiler.
- Default methods in interfaces introduced in JDK8 where we can provide a method implementation within the interface itself.
- Static methods were also introduced in JDK8, that can be called independently without an object. These methods are not inherited. 
- We use interfaces to add certain behavioral functionality that can be used by unrelated classes. For instance, Comparable, Comparator, and Cloneable are Java interfaces that can be implemented by unrelated classes, e.g. - Comparator interface is used to compare two instances of a class.
- One interface can inherit another by the use of keyword `extends`. When a class implements an interface that inherits another interface, it must provide an implementation for all methods required by the interface inheritance chain.
- Inside the Interface, constructors are not allowed.
- Java classes support singular inheritance. However, by using interfaces, we’re also able to implement multiple inheritances.

__All methods on an interface are implicitly public:__ If we omit an access modifier on a class member, its implicitly package-private.  If we omit an access modifier on an interface member, its implicitly public. Changing the access modifier of a method to protected on an interface is a compiler error, whether the method is concrete or abstract. Only a concrete method can have private access.

__Private Methods in Interfaces (Java 9):__ Interface can now include private methods.

- Private methods are defined within the interface but it cannot be accessed by the implementing classes.
- Private methods cannot be overridden by implementing classes as they are not inherited.
- Unlike abstract methods, private methods in interfaces must have a method body (implementation).
- Private methods are primarily used to share common code between multiple default or static methods within the interface, preventing code duplication.
- Interfaces can also have private static methods, which can be called from other static methods or default methods within the interface.

__Why default methods added in interfaces:__ Default methods were introduced in Java 8 to address the challenge of evolving interfaces without breaking existing code that implements those interfaces. Backward Compatibility and Interface Evolution: Prior to Java 8, if a new abstract method was added to an interface, all classes that implemented that interface were required to provide an implementation for the new method. This could lead to significant refactoring, especially in large codebases with many implementing classes. Default methods allow new methods to be added to an interface with a default implementation, meaning that existing implementing classes do not need to be modified unless they specifically want to override the default behavior.

## **Inheritance**

Inheritance is an important pillar of OOP. It is the mechanism in Java by which one class is allowed to inherit the features (fields and methods) of another class. We are achieving inheritance by using extends keyword. Inheritance is also known as __is-a__ relationship. It supports the concept of _reusability_.

- Method Overriding is achievable only through Inheritance. It is one of the ways by which Java achieves Run Time Polymorphism.
- The concept of abstraction where we do not have to provide all details, is achieved through inheritance. Abstraction only shows the functionality to the user.


### **Types of Inheritance**


## **Polymorphism**

Polymorphism allows objects to behave differently based on their specific class type. This means one entity can take many forms. In Java, polymorphism allows the same method or object to behave differently based on the context, specially on the object's actual runtime class. 

- __Multiple Behaviors:__ The same method can behave differently depending on the object that calls this method.
- __Method Overriding:__ A child class can redefine a method of its parent class.
- __Method Overloading:__ We can define multiple methods with the same name but different parameters.
- __Runtime Decision:__ At runtime, Java determines which method to call depending on the object's actual class.

In Java Polymorphism is mainly divided into two types: 

- __Compile-Time Polymorphism (Static):__ is also known as static polymorphism or early binding. It is a type of polymorphism that is resolved during the compilation process. Overloading of methods is called through the reference variable of a class. Compile-time polymorphism is achieved by method overloading and operator overloading (not supported by Java).
- __Runtime Polymorphism (Dynamic):__ known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at runtime, rather than compile time. This type of polymorphism is achieved by Method Overriding.

### **Method Overloading and Method Overriding**

__Method Overloading:__ where more than one method share the same name with different signature(Parameters) in a class. 

- Difference in parameters may include number of parameters, datatype of parameters and their order.
- The return type of these methods may or may not be same. So, having 2 methods with same name and parameters list but different return type will be illegal with compilation error.
- It reduces duplicate code.
- We can overload static or instance methods. But, we cannot have an instance and a static method with same name with different parameters.
- Methods can be overloaded by subclasses. Its because a subclass inherits one version of the method from the parent class, and then the subclass can have another overloaded version of that method.
- Overloaded methods with same name but different parameter list can use different visibility settings (e.g. one can be public another private).

__Method Overriding:__ where method in the child class has the same name, return-type and parameters as in parent class. 

- The child class provides the implementation for the method already written.
- We cant override static methods.
- Overriden methods must have the same return type or covariant return type in the child class.
- The overriden method cant have a lower access modifier, i.e. it cant have more restrictive access.
- Final methods cannot be overridden.
- When an overridden method is called through a superclass reference, Java determines which version(superclass/subclasses) of that method is to be executed and it depends on the type of the object being referred to and not the type of the reference variable.
- A crucial aspect of dynamic method dispatch is upcasting. A superclass reference variable can refer to a subclass object. This is also known as upcasting. Java uses this fact to resolve calls to overridden methods at run time.

### **Class Type Casting in Java**

__`instanceof` keyword:__ used for check if a reference variable contains a given type of object reference or not. It determines whether an object is an instance of a specified type (class, subclass, or interface) at runtime. It returns true if the object is an instance of the Type or a subclass/implementation of Type. Returns false otherwise, including when the object is null. 

__Pattern Matching for instanceof (Java 14+):__ Java 14 introduced pattern matching for instanceof, which simplifies conditional type checking and casting. It allows you to declare a pattern variable directly within the instanceof check, eliminating the need for an explicit cast.

```java
Movie advMovie = Movie.getMovie("Adventure", "Shawshank Redemption");
advMovie.watchMovie();  // parent class method
if (advMovie instanceof Adventure adv) {
	adv.watchAdventure();  // child class method
}
```

We have seen here that a parent class data member is accessed when a reference of parent type refers to a child object. We can access child data members using typecasting. 


__Covariant Return Type:__ 

Covariant return types in Java refer to the ability of an overriding method in a subclass to return a more specific type than the return type of the method it overrides in the superclass. This feature was introduced in Java 5.0. 
Key principles of covariant return types:
Subtype Relationship:
The return type of the overriding method must be a subtype (or the same type) of the return type of the overridden method in the superclass.
Method Signature:
The method name and parameter types of the overriding method must be identical to the overridden method. Only the return type can differ, provided it adheres to the subtype rule.
Non-Primitive Types:
Covariant return types are applicable only to non-primitive return types (classes, interfaces, arrays, etc.), not to primitive types like int, boolean, char, etc. 

https://www.geeksforgeeks.org/java/serialization-and-deserialization-in-java/
https://www.geeksforgeeks.org/java/clone-method-in-java-2/
https://www.geeksforgeeks.org/java/reflection-in-java/

### **Java Records vs POJOs**

Records are immutable by default. This means that once a record object is created, its values cannot be changed. This can be useful for representing data that should not change once it is created. POJOs, on the other hand, are mutable by default and require additional effort to make them immutable.

https://www.geeksforgeeks.org/java/what-are-java-records-and-how-to-use-them-alongside-constructors-and-methods/


## **Java Development Environment** 

Java Development Environment is required to compile and run Java programs on a system. It involves installing the JDK and configuring environment variables like PATH and JAVA_HOME so the system can access Java tools properly.

### **Java Virtual Machine (JVM)**

JVM is an implementation of a virtual machine which executes a Java program. JVM first interprets the bytecode. It then stores the class information in the memory area. Finally, it executes the bytecode generated by the java compiler. Components of the JVM are: Class Loaders, Run-Time Data Areas
and Execution Engine.

#### **JVM Run-Time Data Areas:**

JVM defines various memory areas to execute a Java program. These are used during runtime and are known as run-time data areas. Some of these areas are created on the JVM start-up and destroyed when the JVM exits while some are created when a thread is created and destroyed when a thread exits. So, JVM is responsible for allocating and deallocating memory for Java programs.

__Heap Area:__ Area of memory where objects are allocated. Each object is allocated on the heap and its memory is reclaimed by GC when it is no longer being used. JVM creates heap area as soon as it starts up. All JVM threads share this area. Memory for heap area does not need to be contiguous.

__Stack Area:__ Area of memory where local variables and method calls are stored. When a method is called, a new stack frame is created on the stack, which contains the method's local variables and parameters. When the method returns, the stack frame is removed from the stack. JVM creates the stack area whenever it creates a new thread, so this area is private for each thread. Memory for JVM stack does not need to be contiguous.

__Method Area:__ Basically, method area is analogous to the storage area for compiled code. It stores structures such as run-time constant pool, field and method data, the code for methods and constructors as well as class definitions. JVM stores these structure for each and every class. This area is also known as permanent generation space (PermGen), is created when the JVM starts up. The memory for this area does not need to be contiguous. All the JVM threads share this memory area.

__PC Registers:__ Each JVM thread has a separate PC Register which stores the address of the currently executing instruction. If the currently executing instruction is a part of the native method then this value is undefined.

__Native method stacks:__ Native methods are those which are written in languages other than Java. Native method stacks are also known as "C stacks". They store the native method information. Whenever the native methods are compiled into machine codes, they usually use a native method stack to keep track of their state. JVM creates these stacks whenever it creates a new thread. And thus JVM threads don’t share this area.


### Stack Memory and Heap Space in Java

**Java method call stack:**

Java is an object-oriented and stack-based programming language where methods play a key role in controlling the program's execution flow. When a method is called, Java uses an internal structure known as the call stack to manage execution, variables, and return addresses. _Call stack_ is a data structure used during runtime to manage method calls and local variables. It operates in a _Last-In-First-Out(LIFO)_ manner, meaning the last method called is the first one to complete and exit. Java automatically manages the call stack using the JVM. When a method is called:

- A new stack frame is added to the call stack to store method details.
- The method runs its code.
- After execution, the stack frame is removed, and control goes back to the calling method.

