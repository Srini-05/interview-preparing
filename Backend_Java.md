# Backend Java Interview Questions

## Basic Java Concepts

### 1. What is Java?

> **Interview Answer:** Java is a high-level, object-oriented programming language developed by Sun Microsystems (now Oracle) that is platform-independent, secure, and widely used for enterprise applications.

Java is a versatile, object-oriented programming language known for its "write once, run anywhere" philosophy. It compiles to bytecode that runs on the Java Virtual Machine (JVM), making it platform-independent. Key features include automatic memory management through garbage collection, strong type checking, and extensive standard libraries. Java is widely used in enterprise applications, Android development, web servers, and big data processing.

**Key Points:**
- Platform-independent (WORA - Write Once, Run Anywhere)
- Object-oriented with strong encapsulation
- Automatic memory management via Garbage Collection
- Rich ecosystem with millions of libraries and frameworks
- Used in web development, mobile apps, enterprise software, and more

**Interview Tip:** Emphasize platform independence and object-oriented nature. Mention real-world applications like banking systems, Android apps, and enterprise software.

---

### 2. What are the features of Java?

> **Interview Answer:** Java features include platform independence, object-oriented programming, security, robustness, simplicity, and automatic memory management.

Java's key features that make it popular for enterprise development:

1. **Platform Independent:** Compile once, run anywhere using JVM
2. **Object-Oriented:** Everything is an object with encapsulation, inheritance, polymorphism
3. **Secure:** Built-in security features, no pointers, bytecode verification
4. **Robust:** Strong memory management, exception handling, type checking
5. **Simple:** Removed complex features like pointers, operator overloading
6. **Multithreaded:** Built-in support for concurrent programming
7. **Architectural Neutral:** Bytecode works on any system with JVM
8. **Portable:** No implementation-dependent aspects
9. **High Performance:** JIT compiler optimizes performance
10. **Distributed:** Built-in support for networking and distributed computing

**Interview Tip:** Focus on WORA (Write Once Run Anywhere), security, and garbage collection as key differentiators from languages like C++.

---

### 3. What is JVM, JRE, JDK?

> **Interview Answer:** JVM (Java Virtual Machine) executes Java bytecode, JRE (Java Runtime Environment) provides runtime environment including JVM and libraries, JDK (Java Development Kit) includes JRE plus development tools.

- **JVM (Java Virtual Machine):** Runtime engine that executes Java bytecode. Provides platform independence by acting as an abstraction layer between compiled Java programs and the underlying hardware/OS.

- **JRE (Java Runtime Environment):** Contains JVM, core libraries, and supporting files needed to run Java applications. Required to run Java programs but not develop them.

- **JDK (Java Development Kit):** Includes JRE plus development tools like compiler (javac), debugger, documentation generator (javadoc), and other utilities. Required for developing Java applications.

**Real-Life Analogy:**
- JVM → Gas stove (actually executes/cooks)
- JRE → Kitchen (stove + utensils for cooking)
- JDK → Kitchen + recipe book + cooking tools (for developing recipes)

**Interview Tip:** JDK for development, JRE for running apps, JVM for bytecode execution. JDK includes JRE which includes JVM.

---

### 4. What are the data types in Java?

> **Interview Answer:** Java has primitive data types (byte, short, int, long, float, double, char, boolean) and reference data types (objects, arrays, strings).

Java data types are divided into two categories:

**Primitive Data Types (8 types):**
- **byte:** 8-bit signed integer (-128 to 127)
- **short:** 16-bit signed integer (-32,768 to 32,767)
- **int:** 32-bit signed integer (-2^31 to 2^31-1)
- **long:** 64-bit signed integer (-2^63 to 2^63-1)
- **float:** 32-bit floating point (IEEE 754)
- **double:** 64-bit floating point (IEEE 754)
- **char:** 16-bit Unicode character
- **boolean:** true/false

**Reference Data Types:**
- Objects, Arrays, Strings, Interfaces, etc.

**Example:**
```java
// Primitive types
int age = 25;
double salary = 50000.50;
boolean isActive = true;
char grade = 'A';

// Reference types
String name = "John Doe";
int[] numbers = {1, 2, 3};
```

**Interview Tip:** Primitives are stored in stack memory, references in heap. Primitives have default values (0, false, etc.), references are null by default.

---

### 5. What are access modifiers?

> **Interview Answer:** Access modifiers control visibility of classes, methods, and variables: public (anywhere), protected (same package + subclasses), default/package-private (same package), private (same class).

Access modifiers determine the accessibility of classes, methods, and variables:

- **public:** Accessible from anywhere
- **protected:** Accessible within same package and subclasses
- **default (no modifier):** Accessible within same package only
- **private:** Accessible within same class only

**Example:**
```java
public class Person {
    public String name;        // accessible everywhere
    protected int age;         // same package + subclasses
    String address;            // same package only (default)
    private String ssn;        // same class only
}
```

**Interview Tip:** Use private for encapsulation, public for APIs, protected for inheritance, default for package-level utilities.

---

### 6. What is the difference between == and equals()?

> **Interview Answer:** == compares reference equality (memory addresses), equals() compares content/value equality. For objects, == checks if they are the same instance, equals() checks if they represent the same value.

**Key Differences:**

| == | equals() |
|----|----------|
| Compares references/memory addresses | Compares content/values |
| Works with primitives and objects | Only works with objects |
| For primitives: compares values | N/A |
| For objects: checks if same instance | Checks if logically equal |

**Example:**
```java
String s1 = new String("hello");
String s2 = new String("hello");
String s3 = s1;

System.out.println(s1 == s2);     // false (different objects)
System.out.println(s1.equals(s2)); // true (same content)
System.out.println(s1 == s3);     // true (same reference)
```

**Interview Tip:** Always use equals() for string comparison, not ==. Override equals() and hashCode() together in custom classes.

---

### 7. What is the difference between String, StringBuffer, StringBuilder?

> **Interview Answer:** String is immutable (unchangeable), StringBuffer is mutable and thread-safe, StringBuilder is mutable and not thread-safe (faster).

**Key Differences:**

| Feature | String | StringBuffer | StringBuilder |
|---------|--------|--------------|---------------|
| Mutability | Immutable | Mutable | Mutable |
| Thread Safety | Yes | Yes | No |
| Performance | Slow for concatenation | Slower than StringBuilder | Fastest |
| Memory Usage | Creates new objects | Modifies existing object | Modifies existing object |

**Example:**
```java
// String - creates new objects
String s = "Hello";
s = s + " World"; // Creates new String object

// StringBuilder - modifies existing object
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies same object

// StringBuffer - thread-safe version of StringBuilder
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World");
```

**Interview Tip:** Use String for constants, StringBuilder for single-threaded concatenation, StringBuffer for multi-threaded scenarios.

---

### 8. What is inheritance?

> **Interview Answer:** Inheritance allows a class to inherit properties and methods from another class using the 'extends' keyword, promoting code reuse and establishing IS-A relationships.

Inheritance is an OOP concept where a child class (subclass) inherits properties and behaviors from a parent class (superclass). It establishes an IS-A relationship and promotes code reuse.

**Key Points:**
- Use `extends` keyword
- Child class inherits all non-private members
- Child can override inherited methods
- Child can add new methods/properties
- Supports single inheritance (one parent) but multiple inheritance through interfaces

**Example:**
```java
class Animal {
    void eat() {
        System.out.println("Animal eats");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

// Usage
Dog dog = new Dog();
dog.eat();  // Inherited from Animal
dog.bark(); // Own method
```

**Interview Tip:** Inheritance promotes code reuse but can lead to tight coupling. Favor composition over inheritance when possible.

---

### 9. What is polymorphism?

> **Interview Answer:** Polymorphism allows objects to take multiple forms. Achieved through method overloading (compile-time) and method overriding (runtime).

Polymorphism means "many forms" - the ability of an object to take different forms. In Java, it's achieved through:

**Compile-time Polymorphism (Method Overloading):**
- Multiple methods with same name but different parameters
- Resolved at compile time

**Runtime Polymorphism (Method Overriding):**
- Subclass provides specific implementation of inherited method
- Resolved at runtime based on actual object type

**Example:**
```java
// Overloading (compile-time)
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

// Overriding (runtime)
class Animal {
    void sound() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    @Override
    void sound() { System.out.println("Woof"); }
}
```

**Interview Tip:** Polymorphism enables flexibility and extensibility. Method overriding is key to runtime polymorphism.

---

### 10. What is abstraction?

> **Interview Answer:** Abstraction hides implementation details and shows only essential features. Achieved through abstract classes and interfaces.

Abstraction is the concept of hiding complex implementation details and showing only the necessary features of an object. It focuses on "what" an object does rather than "how" it does it.

**Ways to achieve abstraction:**
1. **Abstract Classes:** Cannot be instantiated, can have abstract methods
2. **Interfaces:** Pure abstraction, all methods are abstract (until Java 8)

**Example:**
```java
// Abstract class
abstract class Vehicle {
    abstract void start();
    void stop() { System.out.println("Vehicle stopped"); }
}

// Interface
interface Drivable {
    void drive();
}

class Car extends Vehicle implements Drivable {
    void start() { System.out.println("Car started"); }
    public void drive() { System.out.println("Car driving"); }
}
```

**Interview Tip:** Abstraction reduces complexity and allows focusing on high-level design. Interfaces support multiple inheritance.

---

### 11. What is encapsulation?

> **Interview Answer:** Encapsulation wraps data and methods into a single unit (class) and hides internal details using access modifiers.

Encapsulation is the bundling of data and methods that operate on that data within a single unit (class), and restricting access to some of the object's components.

**Key Principles:**
- Data hiding using private access modifiers
- Controlled access through public getter/setter methods
- Protects object integrity
- Allows validation in setters

**Example:**
```java
class Person {
    private String name;
    private int age;

    // Getter
    public String getName() {
        return name;
    }

    // Setter with validation
    public void setAge(int age) {
        if (age > 0) {
            this.age = age;
        }
    }
}
```

**Interview Tip:** Encapsulation protects data integrity and allows changing implementation without affecting users.

---

### 12. What is the difference between overloading and overriding?

> **Interview Answer:** Overloading provides compile-time polymorphism with multiple methods of same name but different signatures. Overriding provides runtime polymorphism where subclasses change parent behavior.

**Key Differences:**

| Overloading | Overriding |
|-------------|------------|
| Same method name, different parameters | Same method signature |
| Compile-time polymorphism | Runtime polymorphism |
| Can change return type | Must have same return type (or covariant) |
| Can change access modifiers | Cannot reduce visibility |
| Happens in same class | Happens in different classes (inheritance) |

**Example Overloading:**
```java
class Calculator {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
```

**Example Overriding:**
```java
class Parent {
    void show() { System.out.println("Parent"); }
}

class Child extends Parent {
    @Override
    void show() { System.out.println("Child"); }
}
```

**Interview Tip:** Overloading changes behavior, overriding replaces behavior. The @Override annotation helps catch errors.

---

### 13. What is a constructor?

> **Interview Answer:** Constructors initialize objects when created. Same name as class, no return type. Types: default, parameterized, copy.

Constructors are special methods that initialize objects when they are created. They have the same name as the class and no return type.

**Types of Constructors:**
1. **Default Constructor:** No parameters, provided by Java if none defined
2. **Parameterized Constructor:** Takes parameters to initialize fields
3. **Copy Constructor:** Creates object from another object

**Example:**
```java
class Person {
    String name;
    int age;

    // Default constructor
    Person() {}

    // Parameterized constructor
    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy constructor
    Person(Person other) {
        this.name = other.name;
        this.age = other.age;
    }
}
```

**Interview Tip:** If no constructor defined, Java provides default. Cannot be inherited but can be overloaded.

---

### 14. What is the this keyword?

> **Interview Answer:** 'this' refers to the current object instance. Used to differentiate instance variables from parameters, call other constructors, and pass current object.

The `this` keyword refers to the current instance of the class. It's used to:

1. **Differentiate variables:** Between instance variables and parameters
2. **Call constructors:** `this()` calls other constructors in same class
3. **Pass current object:** To methods or constructors
4. **Access members:** Explicitly access instance members

**Example:**
```java
class Person {
    private String name;
    private int age;

    Person(String name, int age) {
        this.name = name;  // instance var = parameter
        this.age = age;
    }

    void display() {
        System.out.println(this.name); // explicit access
    }

    Person(String name) {
        this(name, 0); // calls parameterized constructor
    }
}
```

**Interview Tip:** Used to avoid name conflicts and enable constructor chaining. In inner classes, `this` refers to inner class instance.

---

### 15. What is the super keyword?

> **Interview Answer:** 'super' refers to the parent class. Used to call parent constructor, access parent methods/variables.

The `super` keyword refers to the immediate parent class. It's used to:

1. **Call parent constructor:** `super()` must be first statement
2. **Access parent members:** `super.method()`, `super.field`
3. **Access overridden methods:** Call parent's version

**Example:**
```java
class Animal {
    String type = "Animal";

    Animal() {
        System.out.println("Animal created");
    }

    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    String type = "Dog";

    Dog() {
        super(); // calls parent constructor
        System.out.println("Dog created");
    }

    void sound() {
        super.sound(); // calls parent method
        System.out.println("Woof");
    }

    void printType() {
        System.out.println(super.type); // "Animal"
        System.out.println(this.type);  // "Dog"
    }
}
```

**Interview Tip:** `super()` must be first in constructor. Enables calling parent implementations in overridden methods.

---

### 16. What are packages in Java?

> **Interview Answer:** Packages organize classes and avoid name conflicts. Follow reverse domain naming convention (com.company.project).

Packages are namespaces that organize classes and interfaces, preventing naming conflicts and providing access control.

**Key Points:**
- Group related classes together
- Use reverse domain naming (com.example.project)
- Classes in same package have package-private access
- Import statement brings classes into scope
- Access modifiers work at package level

**Example:**
```java
// File: com/example/model/Person.java
package com.example.model;

public class Person {
    String name; // package-private
}

// File: com/example/Main.java
package com.example;

import com.example.model.Person;

public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        // Can access name because same package
    }
}
```

**Interview Tip:** Use packages for organization and encapsulation. The classpath tells JVM where to find packages.

---

### 17. What is the difference between ArrayList and LinkedList?

> **Interview Answer:** ArrayList uses dynamic array (fast random access, slow insertions), LinkedList uses doubly linked list (fast insertions/deletions, slow random access).

**ArrayList:**
- **Uses a dynamic array internally** - resizes automatically when capacity increases
- **Fast random access** - O(1) time complexity for get(index)
- **Slower insert/delete in middle** - O(n) due to shifting elements
- **Less memory overhead** - only stores the elements
- **Better for read-heavy operations** - frequent get() operations

**LinkedList:**
- **Uses a doubly linked list** - each node has references to previous and next
- **Slow random access** - O(n) time complexity for get(index)
- **Faster insert/delete** - O(1) if node reference is known, O(n) otherwise
- **More memory usage** - extra space for node pointers
- **Better for frequent modifications** - especially at ends (add/remove)

**Key Differences:**

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| **Data Structure** | Dynamic Array | Doubly Linked List |
| **Access Time** | O(1) | O(n) |
| **Insert/Delete** | O(n) | O(1)* |
| **Memory Usage** | Less | More (extra pointers) |
| **Performance Best** | Read operations | Insert/Delete operations |

*O(1) only when position/node is already known (like add/remove at ends)

**Code Examples:**
```java
// ArrayList - fast random access
List<Integer> arrayList = new ArrayList<>();
arrayList.add(10);
arrayList.add(20);
int value = arrayList.get(0);  // O(1) - very fast

// LinkedList - fast modifications
List<Integer> linkedList = new LinkedList<>();
linkedList.add(10);
linkedList.add(20);
linkedList.addFirst(5);        // O(1) - fast
linkedList.removeLast();       // O(1) - fast
```

**When to Use:**
- **ArrayList:** Frequent read/search operations, random access patterns
- **LinkedList:** Frequent add/remove operations, especially at ends

**Interview Tip:** ArrayList is better for fast access and reads, while LinkedList is better for frequent insertions and deletions. Choose based on your dominant operation pattern.

---

### 18. What is the difference between HashSet and TreeSet?

> **Interview Answer:** HashSet unordered, uses hash for fast lookup. TreeSet ordered, uses red-black tree, maintains sorted order.

**Key Differences:**

| HashSet | TreeSet |
|---------|---------|
| Unordered collection | Sorted collection |
| Uses hash table | Uses red-black tree |
| O(1) average operations | O(log n) operations |
| Allows null element | Allows null element |
| Faster | Slower due to sorting |

**Example:**
```java
Set<String> hashSet = new HashSet<>();
Set<String> treeSet = new TreeSet<>();

hashSet.add("banana");
hashSet.add("apple");
// Order not guaranteed

treeSet.add("banana");
treeSet.add("apple");
// Will be sorted: "apple", "banana"
```

**Interview Tip:** HashSet for fast lookups when order doesn't matter, TreeSet for sorted unique elements.

---

### 19. What is the difference between HashMap and HashTable?

> **Interview Answer:** HashMap not synchronized (faster, allows null), HashTable synchronized (thread-safe, doesn't allow null).

**Key Differences:**

| HashMap | HashTable |
|---------|-----------|
| Not synchronized | Synchronized |
| Allows null keys/values | Doesn't allow null keys/values |
| Faster | Slower (due to synchronization) |
| Iterator fails-fast | Enumerator doesn't fail-fast |
| Introduced in Java 1.2 | Legacy class from Java 1.0 |

**Example:**
```java
// HashMap - allows null
Map<String, String> hashMap = new HashMap<>();
hashMap.put(null, null); // OK

// HashTable - throws NullPointerException
Map<String, String> hashTable = new HashTable<>();
hashTable.put(null, null); // Error
```

**Interview Tip:** Use HashMap for single-threaded, ConcurrentHashMap for multi-threaded applications.

---

### 20. What is the try-with-resources statement?

> **Interview Answer:** Automatically closes resources that implement AutoCloseable. Prevents resource leaks and simplifies code.

Try-with-resources automatically closes resources at the end of the try block, eliminating the need for explicit finally blocks.

**Key Points:**
- Resources must implement AutoCloseable or Closeable
- Close() methods called in reverse order of declaration
- Exceptions from close() suppressed if try block throws
- Much safer than manual try-finally

**Example:**
```java
// Old way - error prone
FileReader fr = null;
try {
    fr = new FileReader("file.txt");
    // use fr
} finally {
    if (fr != null) fr.close();
}

// New way - automatic closing
try (FileReader fr = new FileReader("file.txt")) {
    // use fr
} // automatically closed
```

**Interview Tip:** Use for files, database connections, sockets. Prevents resource leaks in exception scenarios.

---
```

### Interview Explanation:
"Java has 8 primitive types for performance and memory efficiency, plus reference types for objects. Primitives are stored on the stack and have default values (0 for numeric, false for boolean, \u0000 for char), while references point to objects on the heap. I choose primitives for simple values to avoid object overhead, but use wrapper classes (Integer, Double) when I need null values or collections. For example, in a banking app, I'd use double for amounts but BigDecimal for precise financial calculations to avoid floating-point precision issues."

**Interview Tip:** Know the size and range of primitives. Strings are immutable objects.
</details>

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">3. What are the access modifiers in Java?</summary>

Access modifiers control the visibility of classes, methods, and variables.

- **public:** Accessible from anywhere.
- **protected:** Accessible within the same package and subclasses.
- **default (no modifier):** Accessible within the same package.
- **private:** Accessible only within the same class.

Example:
```java
public class Car {
    private String model;
    protected int year;
    public void drive() { }
}
```

### Interview Explanation:
"Access modifiers in Java control encapsulation and API design. I use private for implementation details that shouldn't be exposed, protected for inheritance hierarchies, default for package-private functionality, and public for the API. For example, in a service class, I'd make the constructor package-private (default) to allow testing within the package but prevent external instantiation, while keeping business methods public. This follows the principle of least privilege and makes refactoring safer."

**Interview Tip:** private for encapsulation, public for APIs.
</details>

</details>

<details>
<summary style="font-size: 1.3em; font-weight: bold;">4. What is the difference between == and equals()?</summary>

- **==** compares reference equality (memory addresses) for objects, value equality for primitives.
- **equals()** compares content/value equality for objects.

Example:
```java
String s1 = new String("Hello");
String s2 = new String("Hello");
System.out.println(s1 == s2); // false (different objects)
System.out.println(s1.equals(s2)); // true (same content)
```

### Interview Explanation:
"The == operator checks if two references point to the same object in memory, while equals() checks if two objects have the same logical value. For primitives, == compares values directly. For objects, == is rarely what you want - it would only return true for the same instance. I always override equals() and hashCode() together in my domain objects, following the contract that equal objects must have equal hash codes. In collections like HashSet or HashMap keys, this is crucial for correct behavior."

**Interview Tip:** Override equals() and hashCode() together in custom classes.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">5. What is the static keyword?</summary>

Static members belong to the class rather than instances.

- Static variables: Shared among all instances.
- Static methods: Can be called without creating an object.
- Static blocks: Executed when the class is loaded.

Example:
```java
class Counter {
    static int count = 0;
    Counter() { count++; }
    static void showCount() { System.out.println(count); }
}
```

### Interview Explanation:
"Static members belong to the class itself, not to instances. Static variables are shared across all instances and can be used for constants or global state. Static methods are useful for utility functions that don't need instance state, like Math.max(). I use static blocks for one-time initialization, such as loading configuration or registering drivers. However, I avoid static state for business logic as it makes testing harder and creates tight coupling. In Spring applications, I prefer dependency injection over static utility classes."

**Interview Tip:** Static methods cannot access instance variables. Used for utility methods.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">6. What is the final keyword?</summary>

Final makes variables, methods, or classes unchangeable.

- Final variable: Cannot be reassigned.
- Final method: Cannot be overridden.
- Final class: Cannot be subclassed.

Example:
```java
final int MAX = 100;
final class MathUtils { }
```

### Interview Explanation:
"Final provides immutability guarantees in Java. Final variables create constants (use UPPER_CASE naming), final methods prevent overriding in inheritance hierarchies, and final classes like String prevent extension. I use final extensively for thread safety - final fields can be safely accessed from multiple threads without synchronization. In method parameters, final prevents accidental reassignment. However, final doesn't make objects immutable if they have mutable state - for that I use immutable classes or libraries like Immutables."

**Interview Tip:** Final for constants, security, and performance.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">7. What is the difference between String, StringBuffer, and StringBuilder?</summary>

- **String:** Immutable, thread-safe, slow for modifications.
- **StringBuffer:** Mutable, thread-safe, synchronized.
- **StringBuilder:** Mutable, not thread-safe, faster.

Example:
```java
String s = "Hello";
s += " World"; // Creates new string

StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies same object
```

### Interview Explanation:
"String is immutable - every modification creates a new object, which is expensive for concatenation in loops. StringBuffer is thread-safe with synchronization, making it safe for multi-threaded environments but slower. StringBuilder is the fastest option for single-threaded string building, with the same API as StringBuffer but without synchronization overhead. In modern Java, the compiler optimizes string concatenation with +, but for loops I always use StringBuilder. For logging or single concatenations, String is fine, but for building complex strings, I choose based on thread safety requirements."

**Interview Tip:** Use StringBuilder for single-threaded string manipulations, StringBuffer for multi-threaded.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">7.5. Why is String Immutable in Java?</summary>

In Java, String is actually immutable, not mutable. This is a very common interview question, so it's important to understand clearly.

### What Does Immutable Mean?

Immutable means the value of the object cannot be changed after it is created.

For example:

```java
String str = "Hello";
str = str + " World";
```

Here it looks like the string changed, but actually:

- "Hello" object is created.
- "Hello World" is created as a new object.
- str now references the new object.
- The original "Hello" string still exists in memory.

### Example Showing Immutability

```java
String s1 = "Java";
String s2 = s1;

s1 = s1 + " Programming";

System.out.println(s1); // Java Programming
System.out.println(s2); // Java
```

s2 still points to "Java" because the original string was not modified.

### Why String Is Immutable in Java

1️⃣ **Security**

Strings are used in:
- file paths
- network connections
- database URLs

Immutability prevents malicious modification.

2️⃣ **String Pool Optimization**

Java uses a String Constant Pool to save memory.

Example:

```java
String a = "Java";
String b = "Java";
```

Both a and b reference the same object in the pool.

This works safely because strings cannot change.

3️⃣ **Thread Safety**

Since strings cannot change, they are automatically thread-safe in multi-threaded environments.

4️⃣ **Hashcode Caching**

Strings are used as keys in HashMap.

Example:

```java
Map<String, Integer> map = new HashMap<>();
```

If strings were mutable, the hashcode could change, breaking the map.

### Mutable Alternatives

If you need a modifiable string, Java provides:

- StringBuilder
- StringBuffer

Example:

```java
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");

System.out.println(sb); // Hello World
```

### Interview One-Line Answer

In Java, String is immutable, meaning its value cannot be changed after creation. This improves security, enables string pooling, ensures thread safety, and allows efficient hashing.

**Interview Tip:** String immutability is crucial for security, performance, and thread safety. Always mention the String pool and HashMap usage.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">8. What are arrays in Java?</summary>

Arrays are fixed-size, homogeneous data structures.

Declaration: `int[] arr = new int[5];`
Initialization: `int[] arr = {1, 2, 3, 4, 5};`

### Interview Explanation:
"Arrays in Java are fixed-size containers for elements of the same type, stored contiguously in memory for fast access. They have O(1) access time but fixed size makes them inflexible. I use arrays when I know the size in advance and need performance, but prefer ArrayList for dynamic collections. Multi-dimensional arrays are arrays of arrays, useful for matrices. The JVM performs bounds checking to prevent buffer overflows, though it costs a small performance penalty. For primitives, arrays store values directly; for objects, they store references."

**Interview Tip:** Arrays have fixed size; use ArrayList for dynamic size.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">9. What is inheritance in Java?</summary>

Inheritance allows a class to inherit properties and methods from another class using `extends`.

Example:
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
```

### Interview Explanation:
"Inheritance creates an 'is-a' relationship where subclasses inherit behavior from superclasses. It promotes code reuse but can create tight coupling. I use inheritance for specialization, like different types of vehicles inheriting from a base Vehicle class. However, I prefer composition over inheritance when possible, as it provides more flexibility. In Java, all classes implicitly extend Object, giving access to methods like toString(), equals(), and hashCode(). Multiple inheritance isn't allowed for classes to avoid the diamond problem, but interfaces provide a way to achieve similar behavior."

**Interview Tip:** Java supports single inheritance. Use interfaces for multiple inheritance.
</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">10. What are interfaces in Java?</summary>

Interfaces define a contract with abstract methods. Classes implement interfaces using `implements`.

Example:
```java
interface Animal {
    void sound();
}

class Dog implements Animal {
    public void sound() { System.out.println("Bark"); }
}
```

### Interview Explanation:
"Interfaces define contracts that implementing classes must fulfill, enabling polymorphism and loose coupling. Before Java 8, interfaces only had abstract methods, but now they can have default methods (providing implementation) and static methods. I use interfaces for dependency injection and testing - I can easily mock interface implementations. In Spring, interfaces like Repository, Service, and Controller are markers that enable framework features. Multiple interface implementation allows mixin-like behavior, and functional interfaces (single abstract method) work with lambdas for functional programming."

**Interview Tip:** All methods are public abstract by default. From Java 8, can have default and static methods.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">11. What are abstract classes?</summary>

Abstract classes cannot be instantiated and may contain abstract methods.

Example:
```java
abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() { System.out.println("Drawing circle"); }
}
```

### Interview Explanation:
"Abstract classes provide partial implementation and force subclasses to implement certain methods. I use them when I want to share common code among related classes but prevent direct instantiation. Unlike interfaces, abstract classes can have state and concrete methods. In frameworks, abstract classes often provide template methods that subclasses customize. For example, in Spring Data JPA, repository interfaces extend from interfaces but the framework provides abstract base classes for common functionality. I choose abstract classes over interfaces when I need to share implementation details among closely related classes."

**Interview Tip:** Use abstract classes when sharing code, interfaces when defining contracts.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">12. What is method overloading and overriding?</summary>

- **Overloading:** Same method name, different parameters in the same class (compile-time polymorphism).
- **Overriding:** Same method signature in subclass (runtime polymorphism).

Example Overloading:
```java
void print(int i) { }
void print(String s) { }
```

Example Overriding:
```java
class Parent {
    void show() { }
}

class Child extends Parent {
    @Override
    void show() { }
}
```

### Interview Explanation:
"Overloading provides compile-time polymorphism with multiple methods of the same name but different signatures, resolved by the compiler based on arguments. Overriding provides runtime polymorphism where subclasses can change parent behavior. I use overloading for convenience (like String.valueOf() with different types) and overriding for specialization. The @Override annotation helps catch errors and documents intent. In inheritance hierarchies, overriding allows the Liskov Substitution Principle - any subclass can be used where the parent is expected."

**Interview Tip:** Overloading changes behavior, overriding replaces behavior.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">13. What is a constructor?</summary>

Constructors initialize objects. Same name as class, no return type.

Types: Default, Parameterized, Copy.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

### Interview Explanation:
"Constructors initialize object state when created with new. Java provides a default no-arg constructor if none is defined, but I always define parameterized constructors for required fields. Constructor chaining with this() calls other constructors in the same class, while super() calls parent constructors. In immutable classes, all fields are final and set in the constructor. For complex initialization, I use builder patterns or factory methods. In Spring, the framework uses reflection to call constructors for dependency injection."

**Interview Tip:** If no constructor, Java provides default. Cannot be inherited.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">14. What is the this keyword?</summary>

`this` refers to the current object instance.

Uses: Differentiate instance variables, call other constructors, pass current object.

Example:
```java
class Person {
    String name;
    Person(String name) { this.name = name; }
}
```

### Interview Explanation:
"The this keyword refers to the current instance, helping distinguish between instance variables and parameters with the same name. I use this.field = parameter in constructors and setters. this() calls other constructors in the same class for constructor chaining. In method chaining (fluent interfaces), I return this to allow method calls like obj.method1().method2(). In inner classes, this refers to the inner class instance, and OuterClass.this refers to the outer class. It's essential for object-oriented programming and prevents shadowing issues."

**Interview Tip:** Used to avoid name conflicts.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">15. What is the super keyword?</summary>

`super` refers to the parent class.

Uses: Call parent constructor, access parent methods/variables.

Example:
```java
class Dog extends Animal {
    Dog() { super(); } // calls parent constructor
}
```

### Interview Explanation:
"Super accesses parent class members, essential for inheritance. super() must be the first statement in a constructor to call parent constructors. I use super.method() to call overridden parent methods, and super.field to access hidden parent fields. In method overriding, super allows calling the parent's version before or after adding subclass behavior. Without explicit super() calls, Java automatically calls the parent's no-arg constructor. Understanding super is crucial for proper inheritance hierarchies and avoiding initialization issues."

**Interview Tip:** Must be first statement in constructor.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">16. What are packages in Java?</summary>

Packages organize classes and avoid name conflicts.

Example: `import java.util.*;`

### Interview Explanation:
"Packages provide namespace management and access control in Java. They follow reverse domain naming (com.company.project) to ensure uniqueness. Classes in the same package have package-private access to each other, which I use for internal implementation classes. Import statements bring classes into scope, with * for all classes in a package. The classpath tells JVM where to find packages. In enterprise applications, packages organize code by functionality (controller, service, repository) and help with modular development and testing."

**Interview Tip:** Use reverse domain naming convention.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">17. What is the difference between ArrayList and LinkedList?</summary>

- **ArrayList:** Dynamic array, fast random access, slow insertions/deletions.
- **LinkedList:** Doubly linked list, fast insertions/deletions, slow random access.

### Interview Explanation:
"ArrayList is backed by a dynamic array, offering O(1) random access but O(n) insertions/deletions in the middle due to shifting. LinkedList uses nodes with pointers, providing O(1) insertions/deletions at ends but O(n) random access. I choose ArrayList for read-heavy operations like iterating or getting by index, and LinkedList for write-heavy scenarios like frequent additions/removals. Both implement List interface, so they're interchangeable in most code. For stacks/queues, I prefer ArrayDeque over LinkedList for better performance."

**Interview Tip:** Choose based on use case: ArrayList for reads, LinkedList for modifications.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">18. What is the difference between HashSet and TreeSet?</summary>

- **HashSet:** Unordered, uses hash, faster.
- **TreeSet:** Ordered, uses red-black tree, slower.

### Interview Explanation:
"HashSet provides O(1) average time complexity for add/remove/contains operations using hashing, but doesn't maintain order. TreeSet keeps elements sorted using a red-black tree, offering O(log n) operations but with ordering guarantees. I use HashSet for fast lookups when order doesn't matter, and TreeSet when I need sorted unique elements. Both implement Set interface and prevent duplicates. For concurrent access, I use ConcurrentSkipListSet (TreeSet equivalent) or ConcurrentHashMap-based sets."

**Interview Tip:** HashSet for uniqueness, TreeSet for sorted order.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">19. What is the difference between HashMap and HashTable?</summary>

- **HashMap:** Not synchronized, allows null keys/values, faster.
- **HashTable:** Synchronized, doesn't allow null, thread-safe but slower.

### Interview Explanation:
"HashTable is the legacy synchronized version from Java 1.0, while HashMap is the modern non-synchronized implementation. HashTable doesn't allow null keys or values (throws NullPointerException), while HashMap allows one null key and multiple null values. For thread safety, I use ConcurrentHashMap instead of HashTable, as it provides better concurrency with segment-level locking. HashMap is faster for single-threaded use, which is most common. In Spring applications, I use HashMap for configuration maps and ConcurrentHashMap for shared caches."

**Interview Tip:** Use HashMap for single-threaded, ConcurrentHashMap for multi-threaded.

</details>

<details><summary style="font-size: 1.3em; font-weight: bold;">20. What is the try-with-resources statement?</summary>

Automatically closes resources that implement AutoCloseable.

Example:
```java
try (FileReader fr = new FileReader("file.txt")) {
    // use fr
} // automatically closed
```

**Interview Tip:** Use for files, database connections, sockets. Prevents resource leaks in exception scenarios.

---

### 21. What is Optional in Java?

> **Interview Answer:** Optional is a container object introduced in Java 8 to handle null values safely and prevent NullPointerException.

Optional is a container object that may or may not contain a non-null value. It provides a better alternative to returning null from methods, helping to avoid the dreaded NullPointerException.

**Key Points:**
- Introduced in Java 8 to handle null values safely
- Container that may or may not contain a value
- Prevents NullPointerException by encouraging explicit null handling
- Functional programming style with methods like map(), filter()
- Not meant to be used as a replacement for all null checks

**Creating Optional Objects:**
```java
// Creating Optional with a value
Optional<String> opt1 = Optional.of("Hello");        // Throws NPE if null passed

// Creating Optional that may be null
Optional<String> opt2 = Optional.ofNullable(null);  // Safe with null

// Creating empty Optional
Optional<String> opt3 = Optional.empty();           // Empty container
```

**Common Methods:**
```java
Optional<String> name = Optional.ofNullable("John");

// 1. isPresent() - Check if value exists
if (name.isPresent()) {
    System.out.println(name.get());  // John
}

// 2. ifPresent() - Execute if value exists
name.ifPresent(val -> System.out.println(val.toUpperCase()));  // JOHN

// 3. orElse() - Return default if empty
String result = name.orElse("Default Name");  // John

// 4. orElseGet() - Lazy default value
String lazy = name.orElseGet(() -> "Generated: " + System.currentTimeMillis());

// 5. orElseThrow() - Throw exception if empty
String mustHave = name.orElseThrow(() -> new RuntimeException("Value required"));

// 6. map() - Transform value if present
Optional<String> upper = name.map(String::toUpperCase);  // Optional[JOHN]

// 7. filter() - Filter based on condition
Optional<String> longName = name.filter(n -> n.length() > 3);  // Optional[John]
```

**Real-World Example:**
```java
// Bad practice - returning null
public String findUserName(Long id) {
    User user = userRepository.findById(id);
    return user != null ? user.getName() : null;  // Can cause NPE
}

// Good practice - using Optional
public Optional<String> findUserName(Long id) {
    return userRepository.findById(id)
            .map(User::getName);  // Returns Optional.empty() if user not found
}

// Usage
Optional<String> userName = findUserName(123L);
String displayName = userName.orElse("Unknown User");
```

**When NOT to use Optional:**
- As method parameters (confusing and not recommended)
- In fields or constructors (breaks serialization)
- For collections or arrays (use empty collections instead)
- Everywhere (only where null is a valid return value)

**Interview Tip:** Optional prevents NPE by making null handling explicit. Use ofNullable() for potentially null values, of() for guaranteed non-null. Prefer orElseGet() over orElse() for expensive defaults.

---

### 22. What is the difference between List, Set, and Map in Java?

> **Interview Answer:** List allows duplicates and maintains order, Set stores unique elements, and Map stores key-value pairs with unique keys.

Java Collections Framework provides three main interfaces: List, Set, and Map. Each serves different purposes and has distinct characteristics.

**List:**
- **Ordered collection** that allows duplicate elements
- **Maintains insertion order** - elements stay in the order they were added
- **Index-based access** - can access elements by position (0, 1, 2...)
- **Allows duplicates** - same element can appear multiple times
- **Common implementations:** ArrayList, LinkedList, Vector

**Set:**
- **Collection that does NOT allow duplicates**
- **Uniqueness guarantee** - each element appears only once
- **No index-based access** - cannot access by position
- **Order depends on implementation:**
  - HashSet: No guaranteed order
  - LinkedHashSet: Maintains insertion order
  - TreeSet: Sorted order (natural ordering or custom comparator)
- **Common implementations:** HashSet, LinkedHashSet, TreeSet

**Map:**
- **Stores data as key-value pairs**
- **Keys are unique** - each key maps to exactly one value
- **Values can be duplicates** - different keys can have same values
- **Not part of Collection interface** - separate interface in Collections Framework
- **Fast lookup using keys** - O(1) average time complexity for HashMap
- **Order depends on implementation:**
  - HashMap: No guaranteed order
  - LinkedHashMap: Maintains insertion order
  - TreeMap: Sorted by keys
- **Common implementations:** HashMap, LinkedHashMap, TreeMap

**Code Examples:**

```java
// List - allows duplicates, maintains order
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("A");  // duplicate allowed
System.out.println(list);  // [A, B, A]
System.out.println(list.get(1));  // B (index-based access)

// Set - no duplicates, order depends on implementation
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("A");  // duplicate ignored
System.out.println(set);  // [A, B] or [B, A] (no guaranteed order)

// Map - key-value pairs, unique keys
Map<Integer, String> map = new HashMap<>();
map.put(1, "A");
map.put(2, "B");
map.put(1, "C");  // replaces value for key 1
System.out.println(map);  // {1=C, 2=B}
System.out.println(map.get(1));  // C (key-based access)
```

**Quick Comparison:**

| Feature | List | Set | Map |
|---------|------|-----|-----|
| **Order** | Maintains insertion order | Depends on implementation | Depends on implementation |
| **Duplicates** | Allowed | Not allowed | Keys: No, Values: Yes |
| **Access** | Index-based (get(index)) | No index access | Key-based (get(key)) |
| **Structure** | Elements | Unique elements | Key → Value pairs |
| **Common Use** | Sequential data | Unique collections | Dictionaries, caches |

**When to Use:**
- **List:** When you need ordered data with possible duplicates (shopping cart items, task lists)
- **Set:** When you need unique elements only (unique IDs, distinct values)
- **Map:** When you need key-value associations (user profiles, configuration data, caches)

**Interview Tip:** List allows duplicates and maintains order, Set stores unique elements, and Map stores key-value pairs with unique keys. Choose based on your data access patterns and uniqueness requirements.

---

### 23. What is the difference between HashMap and HashSet in Java?

> **Interview Answer:** HashMap stores key-value pairs with unique keys, while HashSet stores only unique elements and internally uses a HashMap.

Both HashMap and HashSet are fundamental data structures in Java's Collections Framework, but they serve different purposes and have different internal implementations.

**HashMap:**
- **Stores data as key-value pairs** - each entry has a key and a corresponding value
- **Keys are unique** - duplicate keys are not allowed (values can be duplicate)
- **Allows one null key and multiple null values** - null keys are permitted
- **Fast operations** - O(1) average time complexity for put/get operations
- **Not synchronized** - not thread-safe by default
- **Common use cases:** Caches, configuration data, lookup tables

**HashSet:**
- **Stores only unique elements** - no duplicates allowed
- **Internally uses HashMap** - elements are stored as keys in a HashMap with dummy values
- **Allows one null value** - only a single null element is permitted
- **Fast operations** - O(1) average time complexity for add/contains operations
- **Not synchronized** - not thread-safe by default
- **Common use cases:** Unique collections, duplicate removal, membership testing

**Key Differences:**

| Feature | HashMap | HashSet |
|---------|---------|---------|
| **Structure** | Key → Value pairs | Only values (elements) |
| **Duplicates** | Keys: No, Values: Yes | No duplicates |
| **Null Handling** | 1 null key, many null values | Only 1 null allowed |
| **Internal Use** | Core data structure | Uses HashMap internally |
| **Access** | By key: `get(key)` | By value: `contains(value)` |

**Code Examples:**
```java
// HashMap - key-value pairs
Map<Integer, String> map = new HashMap<>();
map.put(1, "A");
map.put(2, "B");
map.put(1, "C");  // replaces value for key 1
map.put(null, "NullKey");  // allowed
map.put(3, null); // allowed
System.out.println(map.get(1));  // "C"

// HashSet - unique elements only
Set<String> set = new HashSet<>();
set.add("A");
set.add("B");
set.add("A");  // ignored (duplicate)
set.add(null); // allowed (only one)
System.out.println(set.contains("A"));  // true
```

**Internal Insight (Important for Interviews):**
HashSet uses a HashMap internally where:
- The element you add becomes the **key** in the HashMap
- A **dummy object** (constant) is used as the **value**
- This is why HashSet has the same performance characteristics as HashMap

**When to Use:**
- **HashMap:** When you need key-value associations, fast lookups by key, or when you need to store additional data with each element
- **HashSet:** When you only need unique elements, want to eliminate duplicates, or need fast membership testing

**Interview Tip:** HashMap stores key-value pairs with unique keys, while HashSet stores only unique elements and internally uses a HashMap. Remember that HashSet uses dummy values in its internal HashMap.

---

### 24. What is the difference between Comparable and Comparator in Java?

> **Interview Answer:** Comparable is used for default/natural sorting inside the class using compareTo(), while Comparator is used for custom sorting outside the class using compare().

Both Comparable and Comparator are interfaces used for sorting objects in Java, but they serve different purposes and are implemented differently.

**Comparable:**
- **Used to define natural/default sorting** - represents the "natural order" of objects
- **Present in java.lang package** - core Java interface
- **Class must implement Comparable** - the sorting logic is inside the class itself
- **Overrides compareTo() method** - single method that takes one parameter
- **Sorting logic is inside the class** - tightly coupled with the class
- **Less flexible** - only one way to sort (natural ordering)

**Comparator:**
- **Used to define custom sorting** - allows multiple sorting strategies
- **Present in java.util package** - part of Collections Framework
- **Implemented separately from class** - sorting logic is external to the class
- **Overrides compare() method** - single method that takes two parameters
- **Allows multiple sorting logics** - can have multiple comparators for different sorting needs
- **More flexible** - multiple ways to sort the same objects

**Key Differences:**

| Feature | Comparable | Comparator |
|---------|------------|------------|
| **Package** | java.lang | java.util |
| **Method** | compareTo(T obj) | compare(T obj1, T obj2) |
| **Sorting Type** | Default (natural) | Custom |
| **Logic Location** | Inside class | Separate class |
| **Flexibility** | Less (only one sorting) | More (multiple ways to sort) |

**Code Examples:**
```java
// Comparable - natural sorting inside the class
class Student implements Comparable<Student> {
    private int age;
    private String name;

    // Constructor and getters...

    @Override
    public int compareTo(Student other) {
        return this.age - other.age;  // Natural order by age
    }
}

// Usage with Comparable
List<Student> students = Arrays.asList(new Student(25, "John"), new Student(20, "Jane"));
Collections.sort(students);  // Uses natural ordering (by age)

// Comparator - custom sorting outside the class
class AgeComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getAge() - s2.getAge();  // Sort by age
    }
}

class NameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.getName().compareTo(s2.getName());  // Sort by name
    }
}

// Usage with Comparator
Collections.sort(students, new AgeComparator());   // Sort by age
Collections.sort(students, new NameComparator());  // Sort by name

// Modern Java 8+ way with lambda
Collections.sort(students, (s1, s2) -> s1.getAge() - s2.getAge());
Collections.sort(students, Comparator.comparing(Student::getName));
```

**When to Use:**
- **Comparable:** When you want default/natural sorting and the class has a clear natural order (like String, Integer, Date)
- **Comparator:** When you need multiple/custom sorting strategies or when you can't modify the class to implement Comparable

**Interview Tip:** Comparable provides natural ordering inside the class using compareTo(), while Comparator enables custom sorting outside the class using compare(). Use Comparable for default sorting, Comparator for flexibility.

---

## Spring Framework Concepts

### 25. What is the difference between RestTemplate and WebClient?

> **Interview Answer:** RestTemplate is synchronous and blocking, WebClient is asynchronous and non-blocking. RestTemplate is legacy, WebClient is recommended for new applications.

RestTemplate and WebClient are both used for making HTTP requests in Spring applications, but they differ significantly in their approach and performance characteristics.

**RestTemplate:**
- Synchronous and blocking
- Each request ties up a thread until response received
- Simple imperative programming model
- Part of Spring Web MVC
- Now in maintenance mode

**WebClient:**
- Asynchronous and non-blocking
- Uses reactive programming with Mono/Flux
- Better performance under high load
- Part of Spring WebFlux
- Recommended for new applications

**Key Differences:**

| Aspect | RestTemplate | WebClient |
|--------|-------------|-----------|
| Programming Model | Imperative | Reactive |
| Blocking | Yes | No |
| Performance | Lower under load | Higher scalability |
| Thread Usage | One per request | Non-blocking I/O |
| Status | Maintenance mode | Active development |

**Examples:**

RestTemplate:
```java
RestTemplate restTemplate = new RestTemplate();
String response = restTemplate.getForObject("https://api.example.com/users", String.class);
```

WebClient:
```java
WebClient client = WebClient.create();
Mono<String> response = client.get()
    .uri("https://api.example.com/users")
    .retrieve()
    .bodyToMono(String.class);
```

**Interview Tip:** RestTemplate blocks threads leading to scalability issues. WebClient uses non-blocking I/O, making it ideal for microservices and high-concurrency applications.

---

### 22. How do you handle microservice communication failures?

> **Interview Answer:** Use resilience patterns: circuit breakers, retries, timeouts, fallbacks. Implement with Resilience4j or Hystrix to prevent cascading failures.

Microservice communication failures are common due to network issues, service downtime, or high latency. Several patterns help build resilient systems:

**Key Resilience Patterns:**

1. **Circuit Breaker:** Stops calling failing services to prevent cascading failures
2. **Retry Mechanism:** Automatically retries failed requests with exponential backoff
3. **Timeout:** Prevents indefinite waiting for responses
4. **Fallback:** Returns default/cached data when service unavailable
5. **Bulkhead:** Isolates failures to prevent affecting other services

**Implementation with Resilience4j:**
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallbackGetUser")
@Retry(name = "userService")
public Mono<User> getUser(String id) {
    return webClient.get()
        .uri("/users/" + id)
        .retrieve()
        .bodyToMono(User.class);
}

public Mono<User> fallbackGetUser(String id, Throwable t) {
    return Mono.just(new User("default", "user"));
}
```

**Configuration:**
```yaml
resilience4j.circuitbreaker:
  instances:
    userService:
      failureRateThreshold: 50
      waitDurationInOpenState: 10000
```

**Interview Tip:** Circuit breakers prevent system-wide failures by failing fast. Always implement timeouts and retries. Use tools like Resilience4j for production-ready implementations.

---

### 23. What are the types of Garbage Collectors (GC) in Java?

> **Interview Answer:** Serial GC (single-threaded), Parallel GC (multi-threaded throughput), CMS (concurrent low-pause), G1 (region-based), ZGC/Shenandoah (ultra-low pause). G1 is default since Java 9.

Java's garbage collectors automatically manage heap memory by reclaiming unused objects. Different GC algorithms optimize for different performance characteristics.

**Major Garbage Collectors:**

1. **Serial GC (-XX:+UseSerialGC):**
   - Single thread for all GC work
   - Stop-the-world pauses
   - Suitable for small applications, single CPU

2. **Parallel GC (-XX:+UseParallelGC):**
   - Multiple threads for minor GC
   - Focuses on throughput over pause time
   - Good for batch processing, scientific computing

3. **CMS (Concurrent Mark Sweep) (-XX:+UseConcMarkSweepGC):**
   - Concurrent marking and sweeping
   - Low pause times
   - Deprecated in newer Java versions

4. **G1 GC (-XX:+UseG1GC):**
   - Divides heap into regions
   - Predictable pause times
   - Default GC since Java 9
   - Good for large heaps

5. **ZGC (-XX:+UseZGC):**
   - Ultra-low pause times (<10ms)
   - Handles multi-terabyte heaps
   - Available since Java 11

6. **Shenandoah (-XX:+UseShenandoahGC):**
   - Similar to ZGC with concurrent compaction
   - Low pause times
   - Available since Java 12

**Choosing a GC:**
- **Small apps:** Serial GC
- **Batch processing:** Parallel GC
- **Low latency:** ZGC or Shenandoah
- **Balanced:** G1 GC (default)

**Interview Tip:** G1 is the default and works well for most applications. For low-latency requirements, use ZGC. Monitor GC performance with tools like VisualVM or GC logs.

---

## Advanced Java Concepts

### 26. JDK vs JRE vs JVM

> **Interview Answer:** JDK includes JRE + development tools, JRE includes JVM + libraries for running Java apps, JVM executes bytecode. JDK for development, JRE for running applications.

**JDK (Java Development Kit):**
- Complete development environment
- Includes JRE + compilers, debuggers, documentation tools
- Required for developing Java applications
- Contains javac (compiler), java (launcher), javadoc, etc.

**JRE (Java Runtime Environment):**
- Runtime environment for executing Java applications
- Includes JVM + core libraries and supporting files
- Required to run Java programs but not develop them
- Contains JVM, class libraries, and other supporting files

**JVM (Java Virtual Machine):**
- Runtime engine that executes Java bytecode
- Platform-independent execution environment
- Converts bytecode to machine-specific instructions
- Provides memory management, garbage collection, security

**Real-Life Analogy:**
- JDK → Complete kitchen with appliances and tools
- JRE → Kitchen with appliances for cooking
- JVM → The stove that actually cooks the food

**Interview Tip:** JDK > JRE > JVM in terms of inclusion. You need JDK to develop, JRE to run, JVM to execute bytecode.

---

### 27. How Java works internally

> **Interview Answer:** Java source code (.java) is compiled to bytecode (.class) by javac, then executed by JVM which converts bytecode to machine code using JIT compiler.

**Java Execution Flow:**

1. **Source Code (.java)** → Developer writes Java code
2. **Compilation** → `javac` compiles to bytecode (.class files)
3. **Class Loading** → ClassLoader loads .class files into memory
4. **Bytecode Verification** → JVM verifies bytecode for security
5. **Execution** → JVM interprets or JIT-compiles bytecode to machine code
6. **Runtime** → Program executes with automatic memory management

**Key Components:**
- **ClassLoader:** Loads classes dynamically
- **Bytecode Verifier:** Ensures bytecode safety
- **JIT Compiler:** Compiles hot methods to native code for performance
- **Garbage Collector:** Automatic memory management
- **Runtime Environment:** Provides execution context

**Interview Tip:** Understand the compilation to bytecode enables WORA. JIT compilation optimizes performance by compiling frequently used code to native instructions.

---

### 28. Memory Areas in Java

> **Interview Answer:** Heap stores objects (GC managed), Stack stores method calls and primitives (auto-managed), Metaspace stores class metadata (Java 8+).

**Memory Areas in JVM:**

1. **Heap Memory:**
   - Stores objects and instance variables
   - Shared among all threads
   - Managed by Garbage Collector
   - Divided into Young Generation, Old Generation, Metaspace (Java 8+)

2. **Stack Memory:**
   - Stores method calls, local variables, references
   - Thread-specific (each thread has its own stack)
   - Automatically managed (LIFO - Last In, First Out)
   - Fixed size, can cause StackOverflowError

3. **Metaspace (Java 8+):**
   - Stores class metadata, method info, static variables
   - Replaced PermGen from Java 7
   - Uses native memory, grows dynamically
   - Configured with -XX:MaxMetaspaceSize

4. **Program Counter (PC) Register:**
   - Holds address of currently executing JVM instruction
   - Thread-specific

5. **Native Method Stack:**
   - For native method execution (JNI)

**Memory Issues:**
- **OutOfMemoryError:** Heap full, can't allocate objects
- **StackOverflowError:** Stack full, usually from infinite recursion

**Interview Tip:** Heap for objects (GC), Stack for execution (auto). Metaspace replaced PermGen to avoid memory issues.

---

### 29. Garbage Collection (basic types, when it runs)

> **Interview Answer:** GC automatically reclaims memory from unused objects. Runs when heap is full or JVM needs space. Types: Minor GC (Young gen), Major GC (Old gen), Full GC (entire heap).

**When Garbage Collection Runs:**
- When Young Generation is full (Minor GC)
- When Old Generation is full (Major GC)
- When Metaspace is full
- When System.gc() is called (not recommended)
- When JVM needs memory for new allocations

**GC Types:**
1. **Minor GC:** Cleans Young Generation (Eden + Survivor spaces)
2. **Major GC:** Cleans Old Generation
3. **Full GC:** Cleans entire heap (expensive, stop-the-world)

**GC Roots:**
- Local variables in stack frames
- Static variables
- Active threads
- JNI references

**Interview Tip:** GC is automatic but can be tuned. Use tools like VisualVM to monitor GC performance. Avoid calling System.gc() manually.

---

### 30. OOPS (Object-Oriented Programming System)

> **Interview Answer:** OOP is programming paradigm using objects containing data and behavior. Four pillars: Encapsulation, Inheritance, Polymorphism, Abstraction.

**OOP Principles:**

1. **Encapsulation:**
   - Bundling data and methods in a class
   - Hiding internal details using access modifiers
   - Controlled access through getters/setters

2. **Inheritance:**
   - Child classes inherit properties from parent classes
   - Promotes code reuse and IS-A relationships
   - Single inheritance in Java, multiple through interfaces

3. **Polymorphism:**
   - "Many forms" - same method behaves differently
   - Achieved through method overloading and overriding
   - Enables flexibility and extensibility

4. **Abstraction:**
   - Hiding complexity, showing only essential features
   - Achieved through abstract classes and interfaces
   - Focus on "what" not "how"

**Real-World Example:**
```java
// Encapsulation
class Car {
    private String model;
    public void drive() { /* implementation */ }
}

// Inheritance
class ElectricCar extends Car {
    public void charge() { /* implementation */ }
}

// Polymorphism
interface Vehicle {
    void move();
}
class Bike implements Vehicle {
    public void move() { System.out.println("Bike moves"); }
}
class Bus implements Vehicle {
    public void move() { System.out.println("Bus moves"); }
}
```

**Interview Tip:** OOP promotes modularity, reusability, and maintainability. Java supports all four pillars with classes, interfaces, and access modifiers.

---

### 31. Exception Handling

> **Interview Answer:** Exceptions are runtime errors handled with try-catch-finally. Checked exceptions must be caught or declared, unchecked are runtime exceptions.

**Exception Types:**

1. **Checked Exceptions:**
   - Checked at compile time
   - Must be handled or declared with `throws`
   - Examples: IOException, SQLException

2. **Unchecked Exceptions:**
   - Runtime exceptions, not checked at compile time
   - Subclasses of RuntimeException
   - Examples: NullPointerException, IllegalArgumentException

3. **Errors:**
   - Serious problems, usually not recoverable
   - Examples: OutOfMemoryError, StackOverflowError

**Exception Handling Keywords:**
- **try:** Code that might throw exception
- **catch:** Handle the exception
- **finally:** Always executes (cleanup code)
- **throw:** Explicitly throw exception
- **throws:** Declare exceptions method might throw

**Example:**
```java
public void readFile(String filename) throws IOException {
    try (FileReader fr = new FileReader(filename)) {
        // read file
    } catch (FileNotFoundException e) {
        System.out.println("File not found: " + e.getMessage());
    } catch (IOException e) {
        System.out.println("IO error: " + e.getMessage());
    } finally {
        System.out.println("Cleanup code always runs");
    }
}
```

**Interview Tip:** Use try-with-resources for automatic resource cleanup. Catch specific exceptions before general ones. finally always runs even if there's a return in try/catch.

---

## Multi-threading

### 32. Multi-threading Made Simple

> **Interview Answer:** Multi-threading allows concurrent execution of multiple threads within a process. Threads share memory but are lighter than processes. Use for responsive UIs and parallel processing.

**Key Concepts:**

- **Process:** Running program with separate memory space (heavyweight)
- **Thread:** Smallest unit of execution within a process (lightweight)
- **Concurrency:** Multiple tasks appear to run simultaneously
- **Parallelism:** Multiple tasks actually run simultaneously (multi-core)

**Real-World Analogy:**
- **Restaurant Kitchen (Process)**: Shared space and resources
- **Chefs (Threads)**: Work concurrently on different dishes
- **One chef grills, another chops, another plates**

**Thread States:**
1. NEW → Created but not started
2. RUNNABLE → Ready to run, waiting for CPU
3. RUNNING → Actively executing
4. WAITING/BLOCKED → Waiting for resource or I/O
5. TERMINATED → Completed execution

**Interview Tip:** Threads share memory making communication easy but requiring synchronization. Use Thread class or Runnable interface to create threads.

---

### 33. Creating Threads in Java

> **Interview Answer:** Three ways: extend Thread class, implement Runnable interface, use lambda expressions. Prefer Runnable for composition over inheritance.

**Way 1: Extend Thread Class**
```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + getName());
    }
}
// Usage
MyThread t1 = new MyThread();
t1.start(); // Don't call run() directly!
```

**Way 2: Implement Runnable Interface (Recommended)**
```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running!");
    }
}
// Usage
Thread t2 = new Thread(new MyRunnable());
t2.start();
```

**Way 3: Lambda Expression (Java 8+)**
```java
Thread t3 = new Thread(() -> {
    System.out.println("Lambda thread running! 🚀");
});
t3.start();
```

**Production-Ready: ExecutorService**
```java
ExecutorService pool = Executors.newFixedThreadPool(4);
pool.submit(() -> System.out.println("Pool thread running!"));
pool.shutdown();
```

**Interview Tip:** Prefer Runnable over extending Thread (composition over inheritance). Use ExecutorService for managing thread pools in production.

---

### 34. Thread vs Process

> **Interview Answer:** Process is heavyweight with separate memory, Thread is lightweight sharing process memory. Processes are isolated, threads are fast to create and communicate.

**Key Differences:**

| Aspect | Thread | Process |
|--------|--------|---------|
| Memory | Shares with other threads | Separate memory space |
| Creation | Lightweight, fast | Heavyweight, slow |
| Communication | Easy (shared memory) | Needs IPC (pipes, sockets) |
| Crash Impact | Affects other threads | Isolated |
| Examples | HTTP request handlers | Chrome browser tabs |
| Switching | Fast context switching | Slow context switching |

**When to Use:**
- **Threads:** For concurrent tasks within same application
- **Processes:** For running separate applications or services

**Interview Tip:** Threads are faster and share resources, processes provide isolation. Most Java applications use threads for concurrency.

---

### 35. Synchronization & Thread Safety

> **Interview Answer:** Synchronization prevents race conditions using synchronized blocks/methods. Ensures only one thread accesses critical section at a time.

**Race Condition Example:**
```java
class Counter {
    private int count = 0;

    public void increment() {
        count++; // Not thread-safe!
    }
}
```

**Synchronization Solution:**
```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++; // Now thread-safe
    }
}
```

**Synchronization Types:**
1. **Synchronized Methods:** Lock entire method
2. **Synchronized Blocks:** Lock specific code section
3. **Static Synchronization:** Lock class-level resources
4. **Lock Interface:** More flexible than synchronized

**Thread Safety Issues:**
- **Race Conditions:** Multiple threads modify shared data
- **Deadlocks:** Threads waiting for each other indefinitely
- **Starvation:** Thread never gets CPU time
- **Livelocks:** Threads active but not progressing

**Interview Tip:** Use synchronized for simple cases, Locks for complex scenarios. Always synchronize access to shared mutable state.

---
