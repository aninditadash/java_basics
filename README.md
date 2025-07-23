# Introduction to Java

Java is a high-level, object-oriented programming language used to build web apps, mobile applications, and enterprise software systems. It is known for its **Write Once, Run Anywhere** capability, which means code written in Java can run on any device that supports the Java Virtual Machine (JVM). It is one of the most popular and widely used programming language and platform. A platform is an environment that helps to develop and run programs written in any programming language. 

## **Table of contents**


## **Java Environment** 

The programming environment of Java consists of three components mainly: __JDK__, __JRE__, __JVM__.

### **Java Development Kit (JDK)**

JDK enables the development and execution of Java programs. It is a set of development tools and libraries used to create Java programs. It works together with the JVM and JRE to run and build Java applications.

- Platform-dependent (OS specific - different version for windows, Linux, macOS).
- JDK is only for development (it is not needed for running Java programs).
- Includes JRE (to execute the java program) + Development tools (javac/compilers, debugger, etc.).
- Used for writing and compiling Java code.

#### **Working of JDK**

- __Java Source File (e.g., Example.java):__ You write the Java program in a source file.
- __Compilation:__ The source file is compiled by the Java Compiler (part of JDK) into bytecode, which is stored in a `.class` file (e.g., Example.class).
- __Execution:__ The bytecode is executed by the JVM, which interprets the bytecode and runs the Java program.

### **Java Runtime Environment (JRE)**

JRE provides an environment to run Java programs on the system. The environment includes Standard Libraries and JVM.

- Used to run Java applications.
- Platform-dependent (OS specific).
- Includes JVM + Libraries (e.g., rt.jar) and other components.
- Used for running a Java application on a system.

#### **Working of JRE**

When you run a Java program, the following steps occur:

- __Class Loader:__ The JRE’s class loader loads the `.class` file containing the bytecode into memory.
- __Bytecode Verifier:__ JRE includes a bytecode verifier to ensure security before execution.
- __Interpreter:__ JVM uses an interpreter + JIT compiler to execute bytecode for optimal performance.
- __Execution:__ The program executes, making calls to the underlying hardware and system resources as needed.

The following actions occur at runtime as listed below: Class Loader -> Byte Code Verifier -> Interpreter -> Executes the Byte Code, Make appropriate calls to the underlying hardware.

### **Java Virtual Machine (JVM)** 

JVM is responsible for executing the Java program. The Java program run using JRE or JDK goes into JVM and JVM is responsible for executing the java program line by line, hence it is also known as an interpreter, but it also utilizes a Just-In-Time (JIT) compiler for performance optimization.

- Executes Java bytecode, and converts bytecode into native machine code.
- JVM is OS-specific/platform-dependent, but bytecode (`.class` files) is platform-independent (same `.class` file runs in any JVM).
- Includes ClassLoader, JIT Compiler, Garbage Collector, etc.
- While JVM interprets bytecode instructions one by one when running in interpreter-only mode, the JIT compiler translates frequently executed bytecode into native machine code during runtime.

JVM is platform-independent in the sense that the bytecode can run on any machine with a JVM, but the actual JVM implementation is platform-dependent. Different operating systems (e.g., Windows, Linux, macOS) require different JVM implementations that interact with the specific OS and hardware.

### **Run the Compiled Java Program**

```java
javac HelloWorld.java
java HelloWorld
```

__Why `.class` is not included in the java command:__ When running a Java program, the java command expects a class name with the `main()` method specified. `javac` command compiles the `HelloWorld.java` file and generates `HelloWorld.class` file. After compilation, the command `java HelloWorld.class` is an incorrect command, this will cause an error because the JVM will look for a class named _HelloWorld.class, not HelloWorld_. Starting with Java SE 11/JDK 11, Java introduced the ability to launch a single-file source-code program with the java launcher, without first needing to explicitly compile the source code. This works by the java launcher automatically invoking the compiler and storing the compiled code in-memory.

```java
java HelloWorld.java
```

Notes:
- [Setting up Environment Variables For Java](https://www.geeksforgeeks.org/java/setting-environment-java/).
- [Setting up a Java Development Kit (JDK)](https://dev.java/learn/getting-started/#setting-up-jdk)

