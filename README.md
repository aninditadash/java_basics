# Introduction to Java

Java is a high-level, object-oriented programming language used to build web apps, mobile applications, and enterprise software systems. It is platform-independent, which means we can write code once and run it anywhere using the Java Virtual Machine (JVM) (**Write Once, Run Anywhere**). It is one of the most popular and widely used programming language and platform. A platform is an environment that helps to develop and run programs written in any programming language. 

Notes:
- [Setting up Environment Variables For Java](https://www.geeksforgeeks.org/java/setting-environment-java/).
- [Setting up a Java Development Kit (JDK)](https://dev.java/learn/getting-started/#setting-up-jdk)

### **Key Features of Java**



## **Table of contents**


## **Java Environment** 

The programming environment of Java consists of three components mainly: __JDK__, __JRE__, __JVM__.

### **Java Development Kit (JDK)**

JDK enables the development and execution of Java programs. It is a set of development tools and libraries used to create Java programs. It works together with the JVM and JRE to run and build Java applications.

- Platform-dependent (OS specific - different version for windows, Linux, macOS).
- JDK is only for development (it is not needed for running Java programs).
- Includes JRE (to execute the java program) + Development tools (javac/compilers, debugger, etc.).
- Used for writing and compiling Java code.

**Working of JDK:** The JDK enables the development and execution of Java programs:

- __Java Source File (e.g., Example.java):__ You write the Java program in a source file.
- __Compilation:__ The source file is compiled by the Java Compiler (part of JDK) into bytecode, which is stored in a `.class` file (e.g., Example.class).
- __Execution:__ The bytecode is executed by the JVM, which interprets the bytecode and runs the Java program.

### **Java Runtime Environment (JRE)**

JRE provides an environment to run Java programs on the system. The environment includes Standard Libraries and JVM.

- Used to run Java applications.
- Platform-dependent (OS specific).
- Includes JVM + Libraries (e.g., rt.jar) and other components.
- Used for running a Java application on a system.

**Working of JRE:** When you run a Java program, the following steps occur:

- __Class Loader:__ The JRE’s class loader loads the `.class` file containing the bytecode into memory.
- __Bytecode Verifier:__ JRE includes a bytecode verifier to ensure security before execution.
- __Interpreter:__ JVM uses an interpreter + JIT compiler to execute bytecode for optimal performance.
- __Execution:__ The program executes, making calls to the underlying hardware and system resources as needed.

The following actions occur at runtime as listed below: Class Loader -> Byte Code Verifier -> Interpreter -> Executes the Byte Code, Make appropriate calls to the underlying hardware.

### **Java Virtual Machine (JVM)** 

JVM is responsible for executing the Java program. The Java program run using JRE or JDK goes into JVM and JVM is responsible for executing the java program line by line, hence it is also known as an interpreter, but it also utilizes a Just-In-Time (JIT) compiler for performance optimization. JVM is a very important part of both JDK and JRE because it is contained or inbuilt in both.

- Executes Java bytecode, and converts bytecode into native machine code.
- JVM is OS-specific/platform-dependent, but bytecode (`.class` files) is platform-independent (same `.class` file runs in any JVM).
- Includes ClassLoader, JIT Compiler, Garbage Collector, etc.
- While JVM interprets bytecode instructions one by one when running in interpreter-only mode, the JIT compiler translates frequently executed bytecode into native machine code during runtime.

JVM is platform-independent in the sense that the bytecode can run on any machine with a JVM, but the actual JVM implementation is platform-dependent. Different operating systems (e.g., Windows, Linux, macOS) require different JVM implementations that interact with the specific OS and hardware.

<br/>
<img src="https://media.geeksforgeeks.org/wp-content/uploads/20250714182833376232/java_jit_compiler.jpg" width=600 />
<br/>

### **Run the Compiled Java Program**

```java
javac HelloWorld.java
java HelloWorld
```

__Why `.class` is not included in the java command:__ When running a Java program, the java command expects a class name with the `main()` method specified. `javac` command compiles the `HelloWorld.java` file and generates `HelloWorld.class` file. After compilation, the command `java HelloWorld.class` is an incorrect command, this will cause an error because the JVM will look for a class named _HelloWorld.class, not HelloWorld_. Starting with Java SE 11/JDK 11, Java introduced the ability to launch a single-file source-code program with the java launcher, without first needing to explicitly compile the source code. This works by the java launcher automatically invoking the compiler and storing the compiled code in-memory.

```java
java HelloWorld.java
```

## **How JVM Works - JVM Architecture**

<https://www.geeksforgeeks.org/java/how-jvm-works-jvm-architecture/>

## **Variables and Methods in Java**

### **Instance Variables**

- Also known as non-static variables and are declared in a class outside of any method, constructor, or block. 
- Created when an object of the class is created and destroyed when the object is destroyed.
- Unlike local variables, we may use access specifiers for instance variables. If we do not specify any access specifier, then the default access specifier will be used.
- Initialization of an instance variable is not mandatory. Its default value is dependent on the data type of variable.
- For String it is null, for float it is 0.0f, for int it is 0, for Wrapper classes like Integer it is null, etc.
- Scope of instance variables are throughout the class except the static contexts.
- Instance variables can be accessed only by creating objects.
- Instance variables can be initialized using constructors while creating an object.
- Instance blocks can be used to initialize instance variables.

### **Static Variables**

- Also known as class variables and are declared similarly to instance variables, but declared using static keyword.
- We can only have one copy of a static variable per class.
- Static variables are created at the start of program execution and destroyed automatically when execution ends.
- Initialization of a static variable is similar to instance variables.
- When accessing a static variable through an object, compiler will show a warning message, but will replace the object name with the class name automatically.
- Static variables cannot be declared locally inside an instance method.
- Static blocks can be used to initialize static variables.

### **Method Call Stack in Java**

Java is an object-oriented and stack-based programming language where methods play a key role in controlling the program's execution flow. When a method is called, Java uses an internal structure known as the call stack to manage execution, variables, and return addresses. _Call stack_ is a data structure used during runtime to manage method calls and local variables. It operates in a _Last-In-First-Out(LIFO)_ manner, meaning the last method called is the first one to complete and exit. Java automatically manages the call stack using the JVM. When a method is called:

- A new stack frame is added to the call stack to store method details.
- The method runs its code.
- After execution, the stack frame is removed, and control goes back to the calling method.

## **Datatypes in Java**

Java is statically typed programming language which means variable types are known at the compile time. In Java, compiler knows exactly what types each variable holds and enforces correct usage during compilation. Data types in Java are of different sizes and values that can be stored in a variable that is made as per convenience and circumstances to handle different scenarios or data requirements.

A language is __statically typed__ if the type of a variable is known at compile time. So, the variable's data type is checked at compile time (before the program runs) rather than at runtime (when the program is executing). This allows compilers to catch type-related errors early on, potentially preventing runtime crashes and improving code reliability.

Java data types are categorized into two main groups: Primitive Data Types and Non-Primitive (Reference) Data Types.

### **Primitive Data Types**

These are the basic building blocks that store simple values directly in memory. They store only single values and have no additional capabilities. They have a fixed size and are stored in the stack memory.

There are eight primitive data types:

- __Integer Types:__ byte: 1 byte (8 bits), short: 2 bytes (16 bits), int: 4 bytes (32 bits) - Default for integer values, long: 8 bytes (64 bits).
- __Floating-Point Types:__ float: 4 bytes (32 bits) - Single-precision, double: 8 bytes (64 bits) - Double-precision, default for decimal values. _Precision refers to the format and amount of space occupied by the relevant type._ Should not be used for precise and accurate calculations. (use BigDecimal)
- __Character Type:__ char - is a single 16-bit Unicode character with the size of 2 bytes (16 bits). Unicode range (0 to 65535).
- __Boolean Type:__ boolean: Typically 1 byte (actual size can vary depending on JVM). Stores true or false.

**Why Java has char size as 2 bytes:** Unlike languages such as C/C++ that use the _ASCII character set_ (7-bit code), Java uses the _Unicode character set to support internationalization_. Unicode requires more than 8 bits to represent a wide range of characters from different languages, including Latin, Greek, Cyrillic, Chinese, Arabic, etc. As a result, Java uses 2 bytes to store a char, ensuring it can represent any Unicode character.

**In Java, a `char` variable can be assigned a value in several ways:** 

- Using a character literal:
- Using an integer literal representing a Unicode value: char takes 2 bytes (16-bit UTF encoding ), while int takes 4 bytes (32-bit). Here, we need to typecast the int to get converted to a char. Every character has its own unique code called a Unicode value, which is represented by a numeric value. Here, we convert the numerical value to its equivalent ASCII representation.
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

**Overflow and Underflow in Java:** overflow and underflow (observed in Integer and Floating-point datatypes) refer to runtime conditions where the result of an arithmetic operation exceeds the maximum or falls below the minimum value that a data type can represent. 

- Overflow occurs when a calculation produces a value larger than the maximum value that can be stored in the assigned data type.
- Underflow occurs when a calculation produces a value smaller than the minimum value (closest to zero, or negative for signed types) that can be stored in the assigned data type.
- In case of overflow/underflow, the compiler doesnot throw any error during compilation process.
- Java handles integer overflow and underflow by "wrapping around" the values. e.g., adding 1 to Integer.MAX_VALUE results in Integer.MIN_VALUE. For floating-point numbers, underflow can result in 0.0, while overflow can result in Infinity or -Infinity.
- Java's default behavior for arithmetic overflow and underflow does not involve throwing exceptions, which can make it challenging to detect and debug these issues.
- However, when assigning a literal number value to a datatype that is outside of the range, the compiler will give an error.

```java
int maxInt = Integer.MAX_VALUE; // 2147483647
int overflowResult = maxInt + 1; // Result will be -2147483648 (Integer.MIN_VALUE)

int minInt = Integer.MIN_VALUE; // -2147483648
int underflowResult = minInt - 1; // Result will be 2147483647 (Integer.MAX_VALUE)

int num1 = Integer.MAX_VALUE + 1; // Code compiles
int num2 = 2147483648; // Error: The literal 2147483648 of type int is out of range

float largeFloat = Float.MAX_VALUE;
float overflowFloat = largeFloat * 2; // Result will be Infinity

float smallFloat = Float.MIN_VALUE; // Smallest positive non-zero value
float underflowFloat = smallFloat / 2; // Result will be 0.0f
```

__Memory Allocation/Efficiency for Primitives:__  Local primitive variables are typically stored on the stack memory. If a primitive variable is a field within an object, its value is stored directly within the object's memory on the heap. They are generally more memory-efficient and offer faster access because their values are stored directly.

### **Non-Primitive (Reference) Data Types**

These data types do not directly store values but instead store references (memory addresses) to objects. It represents the set of properties or methods that are common to all objects of one type. Examples include String, Arrays, and user-defined classes and interfaces.

- __Classes:__ User-defined blueprints or prototypes from which objects are created.
- __Object:__ An Object is a basic unit of Object-Oriented Programming and represents real-life entities. An object consists of :
  - _State:_ It is represented by the attributes of an object. It also reflects the properties of an object.
  - _Behavior:_ It is represented by the methods of an object. It also reflects the response of an object to other objects.
  - _Identity:_ It gives a unique name to an object and enables one object to interact with other objects.
- __Interfaces:__ Like a class, an interface can have methods and variables, but the methods declared in an interface are by default abstract (only method signature, no body).
- __Arrays:__ Collections of elements of the same data type.
- __String:__ A sequence of characters (a special class in Java). The difference between a character array and a string in Java is, that the string is designed to hold a sequence of characters in a single variable whereas, a character array is a collection of separate char-type entities.

__Memory Allocation for Non-Primitives:__ Objects (instances of non-primitive types) and their data are stored on the heap memory. Variables of non-primitive types store references (memory locations) to these objects. References to these objects (i.e. the local variables referencing these objects) are stored in the stack memory. 

## **Strings in Java**

In Java, a String is the type of object that can store a sequence of characters enclosed by double quotes, and every character is stored in 16 bits, i.e., using UTF 16-bit encoding. Java provides a robust and flexible API for handling strings, allowing for various operations such as concatenation, comparison, and manipulation. There are two ways to create a string in Java: using string literal, using new keyword.

- Strings are immutable means their values cannot be changed once they are created.
- If we try to change a string, Java does not modify the original one, it creates a new string object instead.
- __Security:__ Strings are frequently used to store sensitive data like passwords, usernames, and file paths. Immutability ensures that once these values are set, they cannot be accidentally or maliciously altered by other parts of the program, enhancing security.
- __Thread Safety:__ In a multi-threaded environment, mutable objects can lead to race conditions and data corruption if multiple threads try to modify them concurrently without proper synchronization. Since String objects are immutable, they are inherently thread-safe and can be shared across threads without requiring explicit synchronization mechanisms.

### **How Strings are Stored in Java Memory**

- __Using string literal:__ When a string literal is encountered, the JVM first checks if an identical string already exists in the string constant pool. If it does, a reference to that existing object is returned. If not, a new String object is created in the pool, and a reference to it is returned. This mechanism promotes memory efficiency by reusing identical string objects. This string constant pool is present in the heap.
- __Using the new keyword:__ This method explicitly creates a new String object in the heap memory, regardless of whether an identical string exists in the String Constant Pool.
- It is preferred to use String literals as it allows JVM to optimize memory allocation.

### **String Methods**

Three basic categories of String methods: 

- String inspection methods: length, charAt, indexOf, lastIndexOf, isEmpty, isBlank (JDK 11)
- Methods for comparing string values: contains, startsWith, endsWith, regionMatches
- string manipulation methods: 

__`isEmpty()` vs `isBlank():`__ `isEmpty()` checks if a string contains no characters at all. It returns true only if the string's length is zero. But if the string contains whitespace characters (spaces, tabs, newlines, etc.), it will return false. `isBlank()` method provides a more comprehensive check for "blankness." It returns true if the string is either empty (has a length of zero) or consists of only whitespace characters.

```java
String str = "\n \t";
		
System.out.println(str.isEmpty()); // false
System.out.println(str.isBlank()); // true
```

__Confusing == and .equals() for Strings:__ == is used to compare object references, while .equals() is used to compare the content of the strings.

## **StringBuilder and StringBuffer classes in Java**

### **Java StringBuilder Class**

The StringBuilder class is a part of the _java.lang_ package that provides a mutable sequence of characters. Unlike String (which is immutable), StringBuilder allows in-place modifications, making it memory-efficient and faster for frequent string operations.

- StringBuilder in Java represents a mutable sequence of characters.
- String Class in Java creates an immutable sequence of characters, whereas StringBuilder creates a mutable sequence of characters, offering an alternative.
- Functionality of StringBuilder is similar to the StringBuffer class, as both provide mutable sequences of characters.
- StringBuilder does not guarantee synchronization, while StringBuffer does. It is a high-performance, low-overhead and non-thread-safe alternative to StringBuffer, suitable for single-threaded applications, while StringBuffer is used for synchronization in multithreaded applications.
- StringBuilder is faster than StringBuffer in most implementations.

## **Flow Control and Loops in Java**

### **Enhancements for Switch Statement in Java 13**

Enhanced switch in Java, introduced as a preview feature in Java 12 and standardized in Java 14, offers a more concise and expressive way to handle conditional logic compared to the traditional switch statement.

- __Arrow Syntax (->):__ This new syntax replaces the traditional colon (:) and eliminates the need for explicit break statements, preventing fall-through behavior by default.
- __Switch Expressions:__ It can be used as an expression, meaning it can directly return a value, which can then be assigned to a variable.
- __yield Keyword:__ When a case block in a switch expression contains multiple statements, the yield keyword is used to explicitly return a value from that specific branch. This replaces the use of break for returning values in such scenarios.
- __Multiple Values per Case:__ Multiple case labels can be specified for a single branch by separating them with commas.

### **For-Each Loop in Java**

The for-each loop (also called the enhanced for loop) simplifies iteration over arrays and collections. It is cleaner and more readable than the traditional for loop and is commonly used when the exact index of an element is not required.

- _We cannot modify array elements directly:_ for-each loop gives copy of each element, not a reference. So modifying the loop variable  does not affect the actual array or collection. For objects, the loop variable is a reference, so modifying fields of the object will affect the original.
- No access to array/collection index
- Cannot perform reverse iteration directly.
- It has some performance overhead over the for a loop.

## **OOP(Object Oriented Programming) in Java**

Object-Oriented Programming (OOPs) is a programming approach that organizes code into classes and objects and makes it more structured and easy to manage. The core idea of OOPs is to bind data and the functions that operate on it, preventing unauthorized access from other parts of the code. A class is a blueprint that defines properties and behaviors, while an object is an instance of a class representing real-world entities.
In Java, the `Object` class, found within the `java.lang` package, is the root of the entire class hierarchy. 

### **Classes and Objects**

A __Class__ is a user-defined blueprint or prototype from which objects are created. It represents the set of properties or methods that are common to all objects of one type. Components of Java classes:

- __Access Modifiers:__ used to control the visibility of the variables, classes, and methods within a class or package.
- __Superclass (if any):__ name of the superclass, using keyword `extends`. _A class can only extend (subclass) one parent._
- __Interfaces(if any):__ A comma-separated list of interfaces implemented by the class, using keyword `implements`. A class can implement more than one interface.
- __Fields:__ Fields are variables defined within a class that hold the data or state of an object.
- __Constructors:__ It is a special method in a class that is automatically called when an object is created. And it's name is same as class name.

Objects are the instances of a class that are created to use the attributes and methods of a class. An object consists of:

- __State:__ It is represented by attributes of an object. It also reflects the properties of an object.
- __Behavior:__ It is represented by the methods of an object. It also reflects the response of an object with other objects.
- __Identity:__ It gives a unique name to an object and enables one object to interact with other objects.

When an object of a class is created, the class is said to be instantiated. In general, we can't create objects of an abstract class or an interface. The `new` operator instantiates a class by allocating memory for a new object and returning a reference to that memory. The new operator also invokes the class constructor.

__Anonymous Objects in Java:__ are objects that are instantiated without storing their reference in a variable. They are used for one-time operations (e.g., method calls) and are discarded immediately after use.

- No reference variable: Cannot reuse the object.
- Created & used instantly: Saves memory for short-lived tasks.
- Common in event handling (e.g., button clicks).

### **Constructors in Java**

Constructors play an important role in object creation. A constructor is a special block of code that is called when an object is created. Its main job is to initialize the object, to set up its internal state, or to assign default values to its attributes. This process happens automatically when we use the "new" keyword to create an object.

- A constructor has the same name as the class in which it is defined.
- Constructors do not have any return type, not even void.
- When an object of a class is created, the constructor is called automatically to initialize the object’s attributes.
- Not necessary to write a constructor for a class as the Java compiler creates a default constructor if not explicitly added.
- A constructor in Java can not be abstract, final, static, or Synchronized.
- Access modifiers can be used in constructor declaration to control its access i.e which other class can call the constructor.

There are three types of constructors in Java:

- __Default Constructor:__ A constructor with no parameters. If no constructor is defined in a class, the Java compiler automatically provides a default constructor. If we define a parameterised constructor, the compiler no longer provides the default constructor. Default constructor can be implicit or explicit.
- __Parameterized Constructor:__ A constructor that has parameters.
- __Copy Constructor:__ Unlike other constructors copy constructor is passed with another object which copies the data available from the passed object to the newly created object.

__Constructor Overloading:__ In Java, overloaded constructor is called based on the parameters specified when a "new" keyword is executed, as we can initialize an object in different ways. `this()` reference can be used during constructor overloading to call the different constructors implicitly from the parameterized constructor. Constructor calling must be the first statement of the constructor in Java.





__Access Modifiers:__ A class can be public or has default access (Refer this for more details).


### **Abstraction**

Data Abstraction is the property by virtue of which only the essential details are displayed to the user. It is the process of showing only essential information and hiding the complex implementation details. In Java, abstraction is achieved using abstract classes and interfaces, allowing you to define a common interface without specifying the full implementation.

### **Encapsulation**

It is defined as the wrapping up of data under a single unit. It is the mechanism of bundling data (variables) and the methods that operate on that data within a single unit (a class). It restricts direct access to an object's internal state, allowing interaction only through defined public methods (getters and setters). This promotes data hiding and security.


https://www.geeksforgeeks.org/java/serialization-and-deserialization-in-java/
https://www.geeksforgeeks.org/java/clone-method-in-java-2/
https://www.geeksforgeeks.org/java/reflection-in-java/
