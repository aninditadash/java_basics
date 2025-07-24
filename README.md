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

## **Variables in Java**



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



