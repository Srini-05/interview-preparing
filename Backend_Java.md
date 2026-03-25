# ☕ Java Backend Interview Questions

> **70+ Questions** | Organized by topic | Open/Close Accordions | Comparison Tables | Clear Explanations

---

## 📋 Table of Contents

- [Java Basics](#-java-basics)
- [OOP Concepts](#-oop-concepts)
- [Java Keywords](#-java-keywords)
- [Strings in Java](#-strings-in-java)
- [Java Collections](#-java-collections)
- [Java Advanced Concepts](#-java-advanced-concepts)
- [Exception Handling](#-exception-handling)
- [Multi-threading & Concurrency](#-multi-threading--concurrency)
- [Bonus Questions](#-bonus-questions)
- [Java Internals & Deep Concepts](#-java-internals--deep-concepts)
- [Advanced Multi-threading](#-advanced-multi-threading)
- [Java Data Structures & Algorithms](#-java-data-structures--algorithms)
- [Java 8+ Modern Features](#-java-8-modern-features)
- [Java Design & Patterns](#-java-design--patterns)
- [Java Memory & Performance](#-java-memory--performance)
- [Java Best Practices & Miscellaneous](#-java-best-practices--miscellaneous)

---

## ☕ Java Basics

<details>
<summary><b>Q1. What is Java?</b></summary>

> **One-Line Answer:** Java is a high-level, platform-independent, object-oriented programming language that runs on the JVM — famous for "Write Once, Run Anywhere."

### What Makes Java Special?

Java was created by James Gosling at Sun Microsystems in 1995. The big idea: write your code once, and it runs on any device with a JVM. This is called **platform independence**.

When you write Java code, the compiler converts it into **bytecode** — not machine code. That bytecode runs on any JVM on any platform (Windows, Linux, Mac, Android).

### Key Features

| Feature | Description |
|---------|-------------|
| **Platform Independent** | Write Once, Run Anywhere (WORA) |
| **Object-Oriented** | Everything organized around objects and classes |
| **Auto Memory Management** | Garbage Collector handles memory for you |
| **Strongly Typed** | Type errors caught at compile time |
| **Multithreaded** | Built-in Thread, Runnable, ExecutorService APIs |
| **Rich Ecosystem** | Spring, Hibernate, Maven, millions of libraries |

### Where Is Java Used?

- 🏦 Enterprise Banking Applications
- 📱 Android App Development
- 🌐 Web Backends (Spring Boot REST APIs)
- 📊 Big Data (Apache Hadoop, Spark)
- ☁️ Cloud & Microservices

> 💡 **Interview Tip:** Always mention WORA, garbage collection, and a real-world use case like banking or Android.

</details>

---

<details>
<summary><b>Q2. What are the main features of Java?</b></summary>

> **One-Line Answer:** Java is platform-independent, object-oriented, secure, robust, multithreaded, and architecturally neutral — designed for reliability and portability.

### The 10 Core Features

| Feature | What It Means |
|---------|--------------|
| **Platform Independent** | Bytecode runs on any JVM — WORA principle |
| **Object-Oriented** | Code organized around objects |
| **Secure** | No explicit pointers, bytecode verifier, Security Manager |
| **Robust** | Strong type checking, exception handling, garbage collection |
| **Simple** | No complex C++ features like pointers, operator overloading |
| **Multithreaded** | Built-in concurrency support |
| **High Performance** | JIT compiler optimizes frequently used code |
| **Distributed** | RMI, Sockets, networking APIs built in |
| **Portable** | No implementation-specific sizes for primitives |
| **Dynamic** | Classes loaded at runtime via ClassLoader |

> 💡 **Interview Tip:** Explain WHY a feature matters — e.g., "No pointers means fewer memory corruption bugs."

</details>

---

<details>
<summary><b>Q3. What is the difference between JVM, JRE, and JDK?</b></summary>

> **One-Line Answer:** JVM executes bytecode, JRE = JVM + libraries to run apps, JDK = JRE + compiler + tools to build apps. They are nested: JDK ⊃ JRE ⊃ JVM.

### Simple Analogy: The Kitchen

- **JVM** = The stove — it actually cooks (executes code)
- **JRE** = The kitchen — stove + utensils to run a recipe (run apps)
- **JDK** = Kitchen + recipe book + chef's tools — to create and run recipes (develop apps)

### Comparison Table

| Component | Full Form | Contains | Used For |
|-----------|-----------|----------|----------|
| **JVM** | Java Virtual Machine | Interpreter, JIT, GC, Runtime | Executing bytecode |
| **JRE** | Java Runtime Environment | JVM + Core Libraries | Running Java applications |
| **JDK** | Java Development Kit | JRE + javac + javadoc + tools | Developing Java applications |

### Key Tools Inside JDK

- `javac` — Java compiler (.java → .class bytecode)
- `java` — Launcher that starts JVM
- `javadoc` — Generates HTML documentation
- `jar` — Packages .class files into a JAR
- `jdb` — Java debugger

> 💡 **Interview Tip:** You need JDK to write code, JRE to run code, and JVM is always running under the hood.

</details>

---

<details>
<summary><b>Q4. What are the data types in Java?</b></summary>

> **One-Line Answer:** Java has 8 primitive types (byte, short, int, long, float, double, char, boolean) and reference types (objects, arrays, strings, interfaces).

### Primitive Data Types — The 8 Fundamentals

| Type | Size | Range | Default | Example |
|------|------|-------|---------|---------|
| **byte** | 8-bit | -128 to 127 | 0 | `byte b = 100;` |
| **short** | 16-bit | -32,768 to 32,767 | 0 | `short s = 5000;` |
| **int** | 32-bit | -2^31 to 2^31-1 | 0 | `int age = 25;` |
| **long** | 64-bit | -2^63 to 2^63-1 | 0L | `long id = 123456789L;` |
| **float** | 32-bit | ±3.4e38 | 0.0f | `float pi = 3.14f;` |
| **double** | 64-bit | ±1.8e308 | 0.0d | `double salary = 50000.0;` |
| **char** | 16-bit | 0 to 65,535 (Unicode) | '\u0000' | `char grade = 'A';` |
| **boolean** | 1-bit | true / false | false | `boolean active = true;` |

### Primitives vs Reference Types

| Aspect | Primitive | Reference |
|--------|-----------|-----------|
| Storage | Stack memory | Heap memory |
| Default value | 0 / false / '\u0000' | null |
| Performance | Faster | Slightly slower |
| Used in Collections | ❌ No (use wrappers) | ✅ Yes |
| Null allowed | ❌ No | ✅ Yes |

> 💡 **Interview Tip:** For financial calculations, always use `BigDecimal` instead of float/double to avoid floating-point precision issues!

</details>

---

<details>
<summary><b>Q5. What are access modifiers in Java?</b></summary>

> **One-Line Answer:** Access modifiers control visibility: public (everywhere), protected (package + subclasses), default (same package), private (same class only).

### The 4 Access Levels

| Modifier | Same Class | Same Package | Subclass | Anywhere |
|----------|-----------|--------------|----------|----------|
| **public** | ✅ | ✅ | ✅ | ✅ |
| **protected** | ✅ | ✅ | ✅ | ❌ |
| **default** (no keyword) | ✅ | ✅ | ❌ | ❌ |
| **private** | ✅ | ❌ | ❌ | ❌ |

### Code Example

```java
public class Person {
    public    String name;     // accessible from anywhere
    protected int    age;      // package + subclasses
              String address;  // default: same package only
    private   String ssn;      // this class ONLY
}
```

### When To Use Each?

- **private** — Always for fields (encapsulation principle)
- **public** — For API methods the outside world needs to call
- **protected** — For methods meant to be extended by subclasses
- **default** — For package-level internal helper classes

> 💡 **Interview Tip:** Always start with the most restrictive access (private) and open up only when needed — Principle of Least Privilege.

</details>

---

<details>
<summary><b>Q6. What is the difference between == and equals()?</b></summary>

> **One-Line Answer:** == checks if two references point to the same memory location. equals() checks if two objects have the same logical value/content.

### Comparison Table

| Aspect | == | equals() |
|--------|-----|---------|
| What it compares | Memory address / reference | Logical content / value |
| For primitives | Compares values directly | N/A |
| For objects | Checks if same instance | Checks if logically equal |
| Can be overridden | ❌ No | ✅ Yes |

### Code Example

```java
String s1 = new String("hello");
String s2 = new String("hello");
String s3 = s1;

System.out.println(s1 == s2);       // false — different objects
System.out.println(s1.equals(s2));  // true  — same content
System.out.println(s1 == s3);       // true  — same reference

// String pool behavior
String a = "hello";  // from pool
String b = "hello";  // same pool object
System.out.println(a == b);  // true!
```

> 💡 **Interview Tip:** Always use `equals()` for String comparison! When you override `equals()`, you MUST also override `hashCode()` — otherwise HashMaps and HashSets will break.

</details>

---

## 🧱 OOP Concepts

<details>
<summary><b>Q7. What is Inheritance?</b></summary>

> **One-Line Answer:** Inheritance lets a child class acquire the properties and behaviours of a parent class using the `extends` keyword, promoting code reuse and IS-A relationships.

### Real-World Analogy

A **Dog** IS-A **Animal**. A Dog inherits the ability to breathe and eat from Animal, and adds its own behaviour like barking. You don't rewrite those common behaviours for every animal.

### Code Example

```java
class Animal {
    String name;
    void eat()    { System.out.println("Animal eats"); }
    void breathe(){ System.out.println("Animal breathes"); }
}

class Dog extends Animal {     // Dog IS-A Animal
    void bark() { System.out.println("Woof!"); }
}

Dog dog = new Dog();
dog.eat();    // inherited from Animal
dog.bark();   // Dog's own method
```

### Types of Inheritance in Java

| Type | Supported? | Notes |
|------|-----------|-------|
| Single | ✅ Yes | A extends B |
| Multilevel | ✅ Yes | A → B → C chain |
| Hierarchical | ✅ Yes | Many classes extend one parent |
| Multiple | ❌ No (classes) | Achieved through interfaces |
| Hybrid | ❌ No (classes) | Achieved through interfaces |

> 💡 **Interview Tip:** Java doesn't allow multiple class inheritance to avoid the "Diamond Problem." Use interfaces to achieve it safely.

</details>

---

<details>
<summary><b>Q8. What is Polymorphism?</b></summary>

> **One-Line Answer:** Polymorphism means "many forms" — the same method name behaves differently based on context. Achieved via overloading (compile-time) and overriding (runtime).

### Two Types of Polymorphism

```java
// 1. COMPILE-TIME (Method Overloading) — resolved at compile time
class Calculator {
    int    add(int a, int b)       { return a + b; }
    double add(double a, double b) { return a + b; }
    int    add(int a, int b, int c){ return a + b + c; }
}

// 2. RUNTIME (Method Overriding) — resolved at runtime
class Animal {
    void sound() { System.out.println("Generic sound"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Woof!"); }
}

Animal a = new Dog();  // reference = Animal, actual = Dog
a.sound();             // prints "Woof!" — runtime polymorphism
```

### Compile-time vs Runtime Polymorphism

| Aspect | Compile-time (Overloading) | Runtime (Overriding) |
|--------|--------------------------|---------------------|
| Also called | Static polymorphism | Dynamic polymorphism |
| Resolved when? | At compile time | At runtime |
| Requires | Same class, different params | Inheritance / @Override |
| Performance | Faster | Slight overhead (vtable lookup) |

> 💡 **Interview Tip:** Polymorphism is the key to writing flexible, extensible code. A classic example: a method that accepts `Animal` type but works for Dog, Cat, Bird, etc.

</details>

---

<details>
<summary><b>Q9. What is Abstraction?</b></summary>

> **One-Line Answer:** Abstraction hides complex internal details and exposes only the essential features. Achieved through abstract classes and interfaces.

### Real-World Analogy

When you drive a car, you use the steering wheel and pedals. You don't need to know how the engine, fuel injection, or transmission work internally. That internal complexity is **abstracted away**.

### Code Example

```java
// Abstract class: partial abstraction
abstract class Shape {
    abstract double area();    // subclass MUST implement
    void display() { System.out.println("Area: " + area()); }
}

class Circle extends Shape {
    double radius;
    Circle(double r) { this.radius = r; }
    @Override
    double area() { return Math.PI * radius * radius; }
}

// Interface: full abstraction (contract)
interface Printable {
    void print();  // all implementing classes must define this
}
```

### Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|--------------|-----------|
| Methods | Abstract + concrete | Abstract + default + static (Java 8+) |
| Variables | Any type | public static final only |
| Constructor | ✅ Yes | ❌ No |
| Multiple inheritance | ❌ One only | ✅ A class can implement many |
| Access modifiers | Any | All members public by default |
| Use when | Shared base behaviour + state | Define a capability contract |

> 💡 **Interview Tip:** Use abstract class for "is-a" (Dog is an Animal). Use interface for "can-do" (Dog can Swim, can Fetch).

</details>

---

<details>
<summary><b>Q10. What is Encapsulation?</b></summary>

> **One-Line Answer:** Encapsulation wraps data (fields) and behavior (methods) together in a class, and hides internal state using private access + public getters/setters.

### Why Encapsulate?

- **Data Protection** — External code can't accidentally corrupt your object's state
- **Validation** — You can validate data inside setters before accepting it
- **Flexibility** — Change internal implementation without breaking external code
- **Maintainability** — Bugs are easier to find when data changes happen in one place

### Code Example

```java
public class BankAccount {
    private double balance;   // hidden from outside

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount > 0) {          // validation
            balance += amount;
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
        } else {
            throw new IllegalArgumentException("Invalid amount");
        }
    }
}
```

> 💡 **Interview Tip:** A well-encapsulated class is like a vending machine — you put in a request, get the result, but have no access to the internal mechanism.

</details>

---

<details>
<summary><b>Q11. What is the difference between Method Overloading and Method Overriding?</b></summary>

> **One-Line Answer:** Overloading = same method name, different parameters, in same class (compile-time). Overriding = same method signature, in child class (runtime).

### Comparison Table

| Feature | Overloading | Overriding |
|---------|------------|------------|
| Class | Same class | Parent & child class |
| Method signature | Same name, different params | Exactly the same |
| Return type | Can be different | Same or covariant |
| Access modifier | Any | Cannot reduce visibility |
| Polymorphism type | Compile-time (static) | Runtime (dynamic) |
| Annotation | None needed | @Override recommended |
| static methods | Can be overloaded | Cannot be overridden |

> 💡 **Interview Tip:** Always use `@Override` annotation when overriding. It lets the compiler catch mistakes if the signature doesn't match the parent method.

</details>

---

<details>
<summary><b>Q12. What is a Constructor? What are its types?</b></summary>

> **One-Line Answer:** A constructor is a special method with the same name as the class and no return type, called automatically when an object is created to initialize its state.

### Three Types of Constructors

```java
class Person {
    String name;
    int age;

    // 1. Default Constructor (no parameters)
    Person() {
        name = "Unknown";
        age  = 0;
    }

    // 2. Parameterized Constructor
    Person(String name, int age) {
        this.name = name;
        this.age  = age;
    }

    // 3. Copy Constructor
    Person(Person other) {
        this.name = other.name;
        this.age  = other.age;
    }
}
```

### Important Rules

- Same name as the class, **no return type** (not even void)
- If you don't define one, Java provides a free **default constructor**
- If you define a parameterized constructor, Java no longer provides the default
- Constructors can be **overloaded** but **cannot be overridden**
- Use `this()` to call another constructor in the same class (constructor chaining)

> 💡 **Interview Tip:** Constructor chaining with `this()` must be the **FIRST** statement in the constructor body.

</details>

---

## 🔑 Java Keywords

<details>
<summary><b>Q13. What is the this keyword in Java?</b></summary>

> **One-Line Answer:** 'this' refers to the current object instance. Used to resolve name conflicts between instance variables and parameters, call other constructors, and pass the current object.

### 4 Uses of this

```java
class Person {
    private String name;
    private int age;

    // USE 1: Differentiate instance var from parameter
    Person(String name, int age) {
        this.name = name;  // this.name = instance variable
        this.age  = age;
    }

    // USE 2: Constructor chaining
    Person(String name) {
        this(name, 0);  // calls Person(String, int)
    }

    // USE 3: Pass current object to another method
    void register() {
        Registry.add(this);  // passes this Person object
    }

    // USE 4: Return current object (method chaining / Builder pattern)
    Person setName(String name) {
        this.name = name;
        return this;  // enables: person.setName("X").setAge(20)
    }
}
```

> 💡 **Interview Tip:** The 'return this' pattern is the foundation of the Builder Pattern and fluent APIs — very common in interview discussions!

</details>

---

<details>
<summary><b>Q14. What is the super keyword in Java?</b></summary>

> **One-Line Answer:** 'super' refers to the parent class. Used to call the parent constructor, access overridden parent methods, and access hidden parent fields.

### Code Example

```java
class Animal {
    String type = "Animal";
    void sound() { System.out.println("Generic sound"); }
}

class Dog extends Animal {
    String type = "Dog";  // hides parent field

    Dog() {
        super();  // MUST be first — calls Animal() constructor
    }

    @Override
    void sound() {
        super.sound();  // calls Animal's sound() first
        System.out.println("Woof!");
    }

    void printTypes() {
        System.out.println(super.type);  // "Animal"
        System.out.println(this.type);   // "Dog"
    }
}
```

> 💡 **Interview Tip:** `super()` must be the FIRST statement in a constructor. If you don't write it, Java inserts `super()` automatically (calling parent's no-arg constructor).

</details>

---

<details>
<summary><b>Q15. What is the static keyword in Java?</b></summary>

> **One-Line Answer:** static members belong to the class itself, not to any specific object. They are shared across all objects and can be accessed without creating an object.

### What Can Be Static?

| Static Thing | Description | Use Case |
|-------------|-------------|----------|
| **Static variable** | Shared across all instances | Counter of objects created |
| **Static method** | Called on class, not object | Math.max(), Collections.sort() |
| **Static block** | Runs once when class loads | Loading config, registering drivers |
| **Static nested class** | Nested class without outer reference | Builder pattern helper classes |

### Code Example

```java
class Counter {
    static int count = 0;    // shared across all Counter objects

    static {
        System.out.println("Class loaded!");  // static block — runs once
    }

    Counter() { count++; }  // increments on each new object

    static void showCount() {
        System.out.println("Total: " + count);
    }
}

// No object needed:
Counter.showCount();  // "Total: 0"
```

### Important Restrictions

- Static methods **cannot** access instance (non-static) variables or methods
- Static methods **cannot** use `this` or `super` keywords
- Static variables are stored in **Metaspace** (not heap)

> 💡 **Interview Tip:** Avoid overusing static — it makes testing harder and couples code. Use it for true utility methods (like Math class) or constants.

</details>

---

<details>
<summary><b>Q16. What is the final keyword in Java?</b></summary>

> **One-Line Answer:** final prevents modification — final variable = constant, final method = cannot be overridden, final class = cannot be subclassed.

### What final Does

| Applied To | Effect | Example |
|-----------|--------|---------|
| **Variable** | Value cannot change (constant) | `final int MAX = 100;` |
| **Method** | Cannot be overridden in subclass | `public final void lock()` |
| **Class** | Cannot be extended/subclassed | `public final class String` |

### Code Example

```java
// final variable: value locked after assignment
final int MAX_SIZE = 100;
// MAX_SIZE = 200; → Compile ERROR

// final reference: reference locked, but object content can change!
final List<String> list = new ArrayList<>();
list.add("Java");  // ✅ OK — modifying content
// list = new ArrayList<>(); → Compile ERROR — can't change reference
```

> 💡 **Interview Tip:** A common interview trap — a `final` reference variable can't be reassigned, but the object it points to can still be mutated. True immutability requires more than just `final`!

</details>

---

## 📝 Strings in Java

<details>
<summary><b>Q17. Why is String immutable in Java?</b></summary>

> **One-Line Answer:** String is immutable because once created, its value cannot be changed — any "modification" creates a new String object. This enables security, thread safety, and String pool optimization.

### Proof of Immutability

```java
String s1 = "Hello";
String s2 = s1;        // s2 points to same object
s1 = s1 + " World";   // creates NEW object "Hello World"

System.out.println(s1);  // "Hello World" (new object)
System.out.println(s2);  // "Hello"       (original unchanged!)
```

### 4 Reasons Java Made String Immutable

| Reason | Explanation |
|--------|-------------|
| **Security** | File paths, DB URLs, passwords are Strings. Immutability prevents malicious modification after validation. |
| **String Pool** | Multiple references can safely share the same String object in the pool, saving memory. |
| **Thread Safety** | Immutable objects can be shared between threads without synchronization. |
| **Hashcode Caching** | String's hashcode is cached after first computation. Since value can't change, cached hash is always valid (crucial for HashMap keys). |

### String Pool Behavior

```java
String a = "Java";  // stored in String pool
String b = "Java";  // reuses same pool object → a == b is true!

String c = new String("Java");  // always creates new heap object
String d = new String("Java");  // c == d is false!
```

> 💡 **Interview Tip:** String pool saves memory by sharing identical string literals. `new String("Java")` bypasses the pool.

</details>

---

<details>
<summary><b>Q18. What is the difference between String, StringBuffer, and StringBuilder?</b></summary>

> **One-Line Answer:** String is immutable. StringBuffer is mutable and thread-safe (synchronized). StringBuilder is mutable, not thread-safe, but fastest.

### Comparison Table

| Feature | String | StringBuffer | StringBuilder |
|---------|--------|-------------|--------------|
| Mutable? | ❌ Immutable | ✅ Mutable | ✅ Mutable |
| Thread-safe? | ✅ Yes | ✅ Yes (synchronized) | ❌ No |
| Performance | Slow for concat | Moderate | Fastest |
| When to use | Constants, short strings | Multi-threaded building | Single-threaded building |
| Memory | Creates new objects | Modifies existing buffer | Modifies existing buffer |

### Code Example

```java
// String — creates new object every time (slow in loops!)
String s = "";
for (int i = 0; i < 1000; i++) s += i;  // 1000 new String objects 🐢

// StringBuilder — best for single-threaded
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) sb.append(i);  // one object 🚀
String result = sb.toString();

// StringBuffer — use when multiple threads build a String
StringBuffer sbf = new StringBuffer();
sbf.append("Thread-safe ");
sbf.append("concatenation");
```

> 💡 **Interview Tip:** StringBuilder is 10-100x faster than String concatenation in loops. Always use StringBuilder in performance-critical code.

</details>

---

## 📦 Java Collections

<details>
<summary><b>Q19. What is the difference between List, Set, and Map?</b></summary>

> **One-Line Answer:** List = ordered + duplicates allowed. Set = unique elements only. Map = key-value pairs with unique keys.

### Comparison Table

| Feature | List | Set | Map |
|---------|------|-----|-----|
| Order | Insertion order maintained | Depends on impl | Depends on impl |
| Duplicates | ✅ Allowed | ❌ Not allowed | Keys unique, values can repeat |
| Access | By index: `get(0)` | No index access | By key: `get("key")` |
| Null | Multiple nulls OK | One null (HashSet) | One null key (HashMap) |
| Implementations | ArrayList, LinkedList | HashSet, TreeSet, LinkedHashSet | HashMap, TreeMap, LinkedHashMap |
| Use when | Ordered sequence | Unique values only | Key-based lookups |

### Code Example

```java
// List - allows duplicates, maintains order
List<String> list = new ArrayList<>();
list.add("A"); list.add("B"); list.add("A");  // duplicate allowed
System.out.println(list);  // [A, B, A]

// Set - no duplicates
Set<String> set = new HashSet<>();
set.add("A"); set.add("B"); set.add("A");  // duplicate ignored
System.out.println(set);  // [A, B]

// Map - key-value pairs, unique keys
Map<Integer, String> map = new HashMap<>();
map.put(1, "A"); map.put(2, "B"); map.put(1, "C");  // replaces "A"
System.out.println(map);  // {1=C, 2=B}
```

> 💡 **Interview Tip:** Pick List when order matters. Pick Set when uniqueness matters. Pick Map when you need fast key-based lookup (like a dictionary or cache).

</details>

---

<details>
<summary><b>Q20. What is the difference between ArrayList and LinkedList?</b></summary>

> **One-Line Answer:** ArrayList uses a dynamic array — fast random access O(1). LinkedList uses doubly linked nodes — fast insertions/deletions O(1) at ends.

### Comparison Table

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| Internal structure | Dynamic array | Doubly linked list |
| Random access | O(1) — very fast | O(n) — slow |
| Insert/Delete (middle) | O(n) — shifts elements | O(n) to find, O(1) to remove |
| Insert/Delete (ends) | O(1) amortized | O(1) — very fast |
| Memory | Less — stores only data | More — prev/next pointers |
| Cache performance | Better (contiguous memory) | Poorer (scattered nodes) |
| Best for | Read-heavy, get by index | Frequent add/remove at ends |

### Code Example

```java
// ArrayList - fast random access
List<Integer> arrayList = new ArrayList<>();
arrayList.add(10);
arrayList.add(20);
int value = arrayList.get(0);  // O(1) - very fast

// LinkedList - fast modifications at ends
LinkedList<Integer> linkedList = new LinkedList<>();
linkedList.addFirst(5);    // O(1) - fast
linkedList.addLast(10);    // O(1) - fast
linkedList.removeLast();   // O(1) - fast
```

> 💡 **Interview Tip:** In practice, ArrayList is preferred 90% of the time. Use LinkedList as a Queue/Deque — but ArrayDeque is even better for that use case.

</details>

---

<details>
<summary><b>Q21. What is the difference between HashMap and Hashtable?</b></summary>

> **One-Line Answer:** HashMap is not synchronized, allows null, and is faster. Hashtable is synchronized (thread-safe), doesn't allow null, and is a legacy class.

### Comparison Table

| Feature | HashMap | Hashtable |
|---------|---------|-----------|
| Thread-safe? | ❌ No | ✅ Yes (synchronized) |
| Null keys | ✅ One null key allowed | ❌ NullPointerException |
| Null values | ✅ Multiple null values | ❌ Not allowed |
| Performance | Faster | Slower (synchronization overhead) |
| Introduced in | Java 1.2 (Collections) | Java 1.0 (legacy) |
| Iterator | Fail-fast iterator | Enumerator (not fail-fast) |

> 💡 **Interview Tip:** Never use Hashtable in new code. Use HashMap for single-threaded scenarios and `ConcurrentHashMap` for multi-threaded environments.

</details>

---

<details>
<summary><b>Q22. What is the difference between HashMap and HashSet?</b></summary>

> **One-Line Answer:** HashMap stores key-value pairs. HashSet stores only unique values — and internally it IS a HashMap where your element is the key and a dummy object is the value.

### Comparison Table

| Feature | HashMap | HashSet |
|---------|---------|---------|
| Stores | Key-value pairs | Unique elements only |
| Duplicates | Duplicate keys replace old value | Duplicates ignored |
| Access | `map.get(key)` | `set.contains(element)` |
| Null | 1 null key, many null values | 1 null element |
| Internally uses | Hash table | HashMap (element = key, dummy = value) |

> 💡 **Interview Tip:** HashSet wraps a HashMap internally — when you add "Hello" to a HashSet, it calls `map.put("Hello", DUMMY_OBJECT)` internally. This is a great answer to impress interviewers!

</details>

---

<details>
<summary><b>Q23. What is the difference between HashSet and TreeSet?</b></summary>

> **One-Line Answer:** HashSet is unordered with O(1) operations using hashing. TreeSet is always sorted with O(log n) operations using a Red-Black Tree.

### Comparison Table

| Feature | HashSet | TreeSet |
|---------|---------|---------|
| Order | No guaranteed order | Sorted (natural or custom) |
| Data structure | Hash table | Red-Black Tree |
| Performance | O(1) add/remove/contains | O(log n) all operations |
| Null element | ✅ One allowed | ❌ Not allowed |
| Use when | Fast lookup, order unimportant | Sorted unique data needed |

</details>

---

<details>
<summary><b>Q24. What is the difference between Comparable and Comparator?</b></summary>

> **One-Line Answer:** Comparable defines natural/default sort order inside the class (compareTo). Comparator defines custom sort logic outside the class (compare) — allowing multiple sort strategies.

### Comparison Table

| Feature | Comparable | Comparator |
|---------|-----------|------------|
| Package | java.lang | java.util |
| Method | `compareTo(T obj)` | `compare(T o1, T o2)` |
| Location | Inside the class | Separate class or lambda |
| Sort types | One (natural order) | Multiple custom orders |
| Modifies class? | Yes | No (external) |

### Code Example

```java
// Comparable — sort by age (natural order inside class)
class Student implements Comparable<Student> {
    int age; String name;

    @Override
    public int compareTo(Student other) {
        return this.age - other.age;  // natural order by age
    }
}

// Usage
Collections.sort(students);  // uses compareTo()

// Comparator — custom sort (external, multiple options)
Collections.sort(students, Comparator.comparing(Student::getName));
Collections.sort(students, (s1, s2) -> s1.age - s2.age);
```

> 💡 **Interview Tip:** Use Comparable for natural ordering. Use Comparator when you need multiple/custom sorting strategies or can't modify the class.

</details>

---

<details>
<summary><b>Q25. What is Optional in Java? Why use it?</b></summary>

> **One-Line Answer:** Optional is a container introduced in Java 8 that may or may not hold a value — a better way to handle null, preventing NullPointerExceptions by making null handling explicit.

### Code Example

```java
// Without Optional — NPE risk
String name = getUserName(id);  // might be null!
int len = name.length();        // BOOM — NullPointerException

// With Optional — safe and explicit
Optional<String> name = Optional.ofNullable(getUserName(id));

// orElse — return default if empty
String display = name.orElse("Anonymous");

// ifPresent — run only if value exists
name.ifPresent(n -> System.out.println(n.toUpperCase()));

// map — transform the value if present
Optional<String> upper = name.map(String::toUpperCase);

// orElseThrow — throw exception if empty
String required = name.orElseThrow(() -> new RuntimeException("Name required"));
```

### Creating Optional

| Method | When to Use |
|--------|-------------|
| `Optional.of(value)` | When value is guaranteed non-null (throws NPE if null) |
| `Optional.ofNullable(value)` | When value might be null (safe) |
| `Optional.empty()` | Explicitly empty container |

### When NOT to use Optional

- ❌ As method parameters
- ❌ In fields or constructors
- ❌ For collections or arrays (use empty collections instead)

> 💡 **Interview Tip:** Optional is designed for **return types only** — to signal "this method might not return a value."

</details>

---

## ⚙️ Java Advanced Concepts

<details>
<summary><b>Q26. How does Java work internally? (Compilation to Execution)</b></summary>

> **One-Line Answer:** Java source code (.java) is compiled to bytecode (.class) by javac, then the JVM loads, verifies, and executes it — using the JIT compiler to convert hot code to native machine code.

### Step-by-Step Execution Flow

| Step | Action | What Happens |
|------|--------|-------------|
| 1 | Write | Developer writes `Hello.java` |
| 2 | Compile | `javac Hello.java` → produces `Hello.class` (bytecode) |
| 3 | ClassLoader | JVM's ClassLoader loads the .class file into memory |
| 4 | Bytecode Verifier | Checks bytecode for security violations and type safety |
| 5 | Interpreter | JVM interprets bytecode line-by-line (slower start) |
| 6 | JIT Compiler | Hot (frequently called) methods compiled to native machine code |
| 7 | Execution | Program runs with GC managing memory automatically |

> 💡 **Interview Tip:** Bytecode is the secret to WORA. It's not machine code (CPU-specific), it's JVM code — any JVM on any OS can run it.

</details>

---

<details>
<summary><b>Q27. What are the memory areas in JVM?</b></summary>

> **One-Line Answer:** JVM has Heap (objects, GC-managed), Stack (method calls + local vars, per-thread), Metaspace (class metadata), PC Register, and Native Method Stack.

### JVM Memory Areas

| Memory Area | Stores | Managed By | Per Thread? |
|------------|--------|-----------|------------|
| **Heap** | Objects, instance variables | Garbage Collector | ❌ Shared |
| **Stack** | Method frames, local vars, references | Auto (LIFO) | ✅ Yes |
| **Metaspace** | Class metadata, static vars | GC (native memory) | ❌ Shared |
| **PC Register** | Address of current JVM instruction | Auto | ✅ Yes |
| **Native Method Stack** | Native (C/C++) method calls via JNI | OS | ✅ Yes |

### Common Memory Errors

| Error | Cause | Fix |
|-------|-------|-----|
| **OutOfMemoryError** | Heap is full — too many alive objects | Tune heap size, fix memory leaks |
| **StackOverflowError** | Stack is full — usually infinite recursion | Fix recursion logic |

> 💡 **Interview Tip:** Metaspace replaced PermGen in Java 8. PermGen had fixed size and caused OutOfMemoryError frequently. Metaspace uses native memory and grows dynamically.

</details>

---

<details>
<summary><b>Q28. What is Garbage Collection? How does it work?</b></summary>

> **One-Line Answer:** GC automatically reclaims heap memory from objects that are no longer reachable — freeing developers from manual memory management.

### How Objects Become Garbage

```java
void method() {
    String s = new String("Hello");  // object created on heap
    s = null;                        // no references → eligible for GC
}                                    // when method returns, s goes out of scope
```

### GC Types

| GC Type | What It Cleans | Speed |
|---------|---------------|-------|
| **Minor GC** | Young Generation (Eden + Survivor) | Fast, frequent |
| **Major GC** | Old Generation | Slower |
| **Full GC** | Entire heap | Most expensive — "stop-the-world" pause |

### GC Algorithms Comparison

| Algorithm | When to Use | Key Feature |
|-----------|-------------|-------------|
| Serial GC | Small apps, single CPU | Single thread |
| Parallel GC | Batch processing | Multiple threads, high throughput |
| G1 GC | Most apps (Java 9+ default) | Predictable pause times |
| ZGC | Ultra-low latency apps | <10ms pauses, multi-TB heaps |
| Shenandoah | Low-latency apps | Concurrent compaction |

> 💡 **Interview Tip:** Never call `System.gc()` manually — it's just a hint, not a guarantee. Trust the JVM to GC at the right time.

</details>

---

<details>
<summary><b>Q29. What are Java 8 features? (Must Know)</b></summary>

> **One-Line Answer:** Java 8 introduced Lambda Expressions, Stream API, Functional Interfaces, Optional, Default Methods in interfaces, Method References, and the new Date/Time API.

### 1. Lambda Expressions — Anonymous Functions

```java
// Old way
Runnable r = new Runnable() {
    public void run() { System.out.println("Running"); }
};

// Java 8 Lambda
Runnable r = () -> System.out.println("Running");
```

### 2. Stream API — Process Collections Functionally

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Anna");

List<String> result = names.stream()
    .filter(n -> n.startsWith("A"))      // Alice, Anna
    .map(String::toUpperCase)            // ALICE, ANNA
    .sorted()                            // alphabetical
    .collect(Collectors.toList());       // to List
```

### 3. Functional Interfaces

| Interface | Takes | Returns | Use For |
|-----------|-------|---------|---------|
| `Predicate<T>` | T | boolean | Filtering |
| `Function<T,R>` | T | R | Mapping/transforming |
| `Consumer<T>` | T | void | Side effects |
| `Supplier<T>` | nothing | T | Lazy creation |

### 4. Default Methods in Interfaces

```java
interface Vehicle {
    void start();
    default void honk() {   // default method — no need to implement
        System.out.println("Beep!");
    }
}
```

> 💡 **Interview Tip:** Java 8 is the most tested version in interviews. Know lambda, stream(), filter(), map(), collect(), Optional, and the 4 functional interfaces by heart.

</details>

---

<details>
<summary><b>Q30. What is try-with-resources?</b></summary>

> **One-Line Answer:** Try-with-resources (Java 7+) automatically closes resources when the try block finishes — even if an exception occurs — eliminating resource leaks.

### Code Example

```java
// OLD WAY — manual cleanup, error-prone
FileReader fr = null;
try {
    fr = new FileReader("file.txt");
    // use fr...
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (fr != null) fr.close();  // what if close() also throws?
}

// NEW WAY — automatic, safe, clean
try (FileReader fr = new FileReader("file.txt")) {
    // use fr...
}  // fr.close() called automatically!
```

Any class implementing `AutoCloseable` or `Closeable` works with try-with-resources.

> 💡 **Interview Tip:** Always use try-with-resources for files, database connections, sockets, and any I/O. It prevents resource leaks — a common source of production bugs.

</details>

---

## ⚠️ Exception Handling

<details>
<summary><b>Q31. What is Exception Handling in Java?</b></summary>

> **One-Line Answer:** Exception handling manages runtime errors gracefully using try-catch-finally. Checked exceptions must be handled at compile time; unchecked exceptions are optional.

### Exception Hierarchy

```
Throwable
├── Error (don't catch — JVM problems)
│   ├── OutOfMemoryError
│   └── StackOverflowError
└── Exception
    ├── Checked Exception (must handle)
    │   ├── IOException
    │   └── SQLException
    └── RuntimeException (unchecked — optional)
        ├── NullPointerException
        ├── ArrayIndexOutOfBoundsException
        └── ClassCastException
```

### Checked vs Unchecked Exceptions

| Feature | Checked Exception | Unchecked Exception |
|---------|-----------------|-------------------|
| Checked when? | At compile time | At runtime only |
| Must handle? | ✅ Yes — catch or throws | ❌ Optional |
| Parent class | Exception (not Runtime) | RuntimeException |
| Represents | External failures (file missing, DB down) | Programming errors |
| Examples | IOException, SQLException | NullPointerException, IndexOutOfBoundsException |

### Exception Handling Keywords

| Keyword | Purpose |
|---------|---------|
| **try** | Wraps code that might throw an exception |
| **catch** | Handles the exception |
| **finally** | Always executes — even if exception occurs or return is used |
| **throw** | Explicitly throw: `throw new IOException("error")` |
| **throws** | Declare: `void method() throws IOException` |

### Code Example

```java
public void readFile(String path) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(path))) {
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
    } catch (FileNotFoundException e) {
        // Specific exception first (more specific → less specific)
        System.err.println("File not found: " + e.getMessage());
    } catch (IOException e) {
        System.err.println("IO Error: " + e.getMessage());
    } finally {
        System.out.println("This ALWAYS runs");
    }
}

// Custom exception
class InsufficientFundsException extends RuntimeException {
    InsufficientFundsException(String message) { super(message); }
}
```

> 💡 **Interview Tip:** Catch specific exceptions before general ones. `finally` always runs. Create custom exceptions for domain-specific errors.

</details>

---

## 🔄 Multi-threading & Concurrency

<details>
<summary><b>Q32. What is Multi-threading in Java?</b></summary>

> **One-Line Answer:** Multi-threading allows a program to run multiple threads concurrently, sharing the same process memory — enabling parallelism, better CPU utilization, and responsive applications.

### Key Concepts

| Term | Definition |
|------|-----------|
| **Process** | A running program with its own memory space |
| **Thread** | Smallest execution unit within a process — shares process memory |
| **Concurrency** | Multiple tasks making progress (possibly on 1 CPU) |
| **Parallelism** | Multiple tasks running simultaneously on multiple CPU cores |

### Thread Lifecycle States

```
NEW → RUNNABLE → RUNNING → BLOCKED/WAITING → TERMINATED
```

| State | Meaning |
|-------|---------|
| **NEW** | Thread created, not started yet |
| **RUNNABLE** | Ready to run, waiting for CPU |
| **RUNNING** | Actively executing on CPU |
| **BLOCKED/WAITING** | Waiting for lock or event |
| **TERMINATED** | Execution completed |

> 💡 **Interview Tip:** Real-world analogy — a restaurant kitchen is one process. Multiple chefs (threads) work concurrently sharing the same kitchen resources.

</details>

---

<details>
<summary><b>Q33. How to create threads in Java? What are the ways?</b></summary>

> **One-Line Answer:** Three ways: extend Thread class, implement Runnable interface, or use Lambda (Java 8+). For production, always use ExecutorService/thread pools.

### All 4 Ways

```java
// WAY 1: Extend Thread class
class MyThread extends Thread {
    public void run() { System.out.println("Thread 1 running"); }
}
new MyThread().start();  // NEVER call run() directly!

// WAY 2: Implement Runnable (RECOMMENDED — composition over inheritance)
class MyTask implements Runnable {
    public void run() { System.out.println("Runnable running"); }
}
new Thread(new MyTask()).start();

// WAY 3: Lambda (Java 8+)
new Thread(() -> System.out.println("Lambda thread")).start();

// WAY 4: ExecutorService (PRODUCTION BEST PRACTICE)
ExecutorService pool = Executors.newFixedThreadPool(4);
pool.submit(() -> System.out.println("Pool thread"));
pool.shutdown();
```

> 💡 **Interview Tip:** Prefer Runnable over extending Thread (you can still extend another class). Use ExecutorService in production — raw threads are unmanaged and wasteful.

</details>

---

<details>
<summary><b>Q34. What is the difference between Thread and Process?</b></summary>

> **One-Line Answer:** Process = heavyweight, isolated memory space (like separate apps). Thread = lightweight, shares process memory — faster to create and communicate between.

### Comparison Table

| Aspect | Thread | Process |
|--------|--------|---------|
| Memory | Shared with other threads | Own separate memory space |
| Creation cost | Lightweight, fast | Heavyweight, slow |
| Communication | Easy (shared memory) | IPC needed (pipes, sockets) |
| Crash impact | Can crash other threads | Isolated — won't affect others |
| Context switch | Fast | Slow |
| Real example | HTTP request handlers | Chrome browser tabs |

</details>

---

<details>
<summary><b>Q35. What is Synchronization? What are thread safety issues?</b></summary>

> **One-Line Answer:** Synchronization ensures only one thread accesses a critical section at a time, preventing race conditions on shared mutable state.

### The Problem — Race Condition

```java
// PROBLEM: count++ is NOT atomic!
// It's actually: (1) read count, (2) add 1, (3) write back
class Counter {
    private int count = 0;
    public void increment() { count++; }  // BUG!
}

// SOLUTION 1: synchronized method
public synchronized void increment() { count++; }

// SOLUTION 2: synchronized block (more granular)
public void increment() {
    synchronized(this) { count++; }
}

// SOLUTION 3: AtomicInteger (best for simple counters)
private AtomicInteger count = new AtomicInteger(0);
public void increment() { count.incrementAndGet(); }
```

### Thread Safety Issues

| Problem | Description | Solution |
|---------|------------|---------|
| **Race Condition** | Multiple threads modify shared data — final value unpredictable | synchronized, AtomicInteger |
| **Deadlock** | Two threads wait for each other's lock — both frozen forever | Lock ordering, tryLock with timeout |
| **Starvation** | Thread never gets CPU/lock time | Fair locks, thread priority tuning |
| **Livelock** | Threads active but constantly reacting to each other, no progress | Introduce randomness in retry |

> 💡 **Interview Tip:** Use `AtomicInteger`/`AtomicLong` for simple counters. For complex scenarios, prefer `java.util.concurrent` (ReentrantLock, CopyOnWriteArrayList, ConcurrentHashMap) over raw synchronized.

</details>

---

## 🎯 Bonus Questions

<details>
<summary><b>Q36. What is the difference between interface and abstract class?</b></summary>

> **One-Line Answer:** Abstract class can have method implementations + state + constructor. Interface defines a pure contract — only abstract methods (+ default/static since Java 8), no constructor.

### Comparison Table

| Feature | Abstract Class | Interface |
|---------|--------------|-----------|
| Methods | Abstract + concrete methods | Abstract + default + static (Java 8+) |
| Variables | Any — instance variables allowed | Only public static final constants |
| Constructor | ✅ Yes | ❌ No |
| Multiple inheritance | ❌ One only (extends one) | ✅ A class can implement many |
| Access modifiers | Any | All members public by default |
| Use when | Shared base behaviour + state | Define a capability contract |

> 💡 **Interview Tip:** Use abstract class for "is-a" (Dog is an Animal). Use interface for "can-do" (Dog can Swim, can Fetch). Interfaces are preferred for API design.

</details>

---

<details>
<summary><b>Q37. What is a Functional Interface in Java?</b></summary>

> **One-Line Answer:** A functional interface has exactly ONE abstract method. It can be used with lambda expressions. Common examples: Runnable, Comparator, Predicate, Function, Consumer, Supplier.

### Code Example

```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);  // exactly ONE abstract method
}

// Use with lambda
MathOperation add      = (a, b) -> a + b;
MathOperation multiply = (a, b) -> a * b;

System.out.println(add.operate(5, 3));       // 8
System.out.println(multiply.operate(5, 3));  // 15
```

### Built-in Functional Interfaces (java.util.function)

| Interface | Signature | Use |
|-----------|-----------|-----|
| `Predicate<T>` | `boolean test(T t)` | Filtering |
| `Function<T,R>` | `R apply(T t)` | Mapping |
| `Consumer<T>` | `void accept(T t)` | Side effects |
| `Supplier<T>` | `T get()` | Lazy creation |
| `BiFunction<T,U,R>` | `R apply(T t, U u)` | Two-arg mapping |

> 💡 **Interview Tip:** `@FunctionalInterface` annotation is optional but recommended — it makes the compiler enforce the single-abstract-method rule.

</details>

---

<details>
<summary><b>Q38. What is the Stream API in Java?</b></summary>

> **One-Line Answer:** The Stream API (Java 8) provides a functional way to process collections using a pipeline of filter/map/reduce operations — without modifying the original data.

### Stream Operations

| Operation Type | Methods | Description |
|---------------|---------|-------------|
| **Intermediate** (lazy) | filter(), map(), flatMap(), sorted(), distinct(), limit(), skip() | Transforms stream, returns stream |
| **Terminal** (eager) | collect(), forEach(), count(), reduce(), findFirst(), anyMatch() | Triggers processing, returns result |

### Code Examples

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5, 6);

// Sum of squares of even numbers
int result = nums.stream()
    .filter(n -> n % 2 == 0)   // 2, 4, 6
    .mapToInt(n -> n * n)       // 4, 16, 36
    .sum();                     // 56

// Group by city
Map<String, List<Person>> byCity = people.stream()
    .collect(Collectors.groupingBy(Person::getCity));

// Find first adult
Optional<Person> adult = people.stream()
    .filter(p -> p.getAge() >= 18)
    .findFirst();
```

> 💡 **Interview Tip:** Streams are **lazy** — intermediate operations don't execute until a terminal operation is called. This makes pipelines efficient.

</details>

---

<details>
<summary><b>Q39. What are all 4 OOP pillars? (Quick Reference)</b></summary>

> **One-Line Answer:** OOP organizes code around objects. The 4 pillars are: Encapsulation (data hiding), Inheritance (code reuse), Polymorphism (many forms), Abstraction (hiding complexity).

### Quick Summary Table

| Pillar | What It Does | How to Achieve | Keyword |
|--------|-------------|---------------|---------|
| **Encapsulation** | Bundles data + methods, hides internals | private fields + getters/setters | `private` |
| **Inheritance** | Child class reuses parent's code | extends keyword | `extends` |
| **Polymorphism** | Same method, different behaviour | Overloading / Overriding | `@Override` |
| **Abstraction** | Hides complexity, shows essential features | Abstract class / Interface | `abstract` / `interface` |

> 💡 **Interview Tip:** Use real-world analogies — ATM = encapsulation, Vehicle hierarchy = inheritance, pay() method = polymorphism, TV remote = abstraction.

</details>

---

<details>
<summary><b>Q40. What is a deadlock? How do you prevent it?</b></summary>

> **One-Line Answer:** Deadlock is when two or more threads are waiting for each other to release a lock — permanently blocked, neither can proceed.

### Classic Deadlock

```java
// Thread 1: holds Lock A, waits for Lock B
// Thread 2: holds Lock B, waits for Lock A
// → Both frozen forever!

synchronized(lockA) {
    synchronized(lockB) {  // Thread 1 order: A → B
        // work
    }
}

synchronized(lockB) {
    synchronized(lockA) {  // Thread 2 order: B → A  ← DEADLOCK!
        // work
    }
}
```

### Deadlock Prevention Strategies

| Strategy | How |
|---------|-----|
| **Lock ordering** | Always acquire locks in same order across all threads |
| **tryLock with timeout** | Use `ReentrantLock.tryLock(timeout)` instead of blocking indefinitely |
| **Avoid nested locks** | Minimize scenarios where one lock is held while acquiring another |
| **Higher-level concurrency** | java.util.concurrent classes are designed to avoid deadlocks |

> 💡 **Interview Tip:** Deadlock has 4 necessary conditions (Coffman's conditions): Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait. Removing any one condition prevents deadlock.

</details>

---

<details>
<summary><b>Q41. What are wrapper classes in Java?</b></summary>

> **One-Line Answer:** Wrapper classes wrap primitive types into objects — Integer wraps int, Double wraps double, etc. — allowing primitives to be used in collections and APIs that require objects.

### Primitive to Wrapper Mapping

| Primitive | Wrapper Class |
|-----------|--------------|
| int | Integer |
| double | Double |
| char | Character |
| boolean | Boolean |
| long | Long |
| float | Float |
| byte | Byte |
| short | Short |

### Autoboxing & Unboxing

```java
// Autoboxing: primitive → wrapper (automatic)
Integer i = 42;  // Java auto-converts int to Integer

// Unboxing: wrapper → primitive (automatic)
int n = i;       // Java auto-converts Integer to int

// Used in collections
List<Integer> list = new ArrayList<>();
list.add(5);  // autoboxed to Integer.valueOf(5)
```

> 💡 **Interview Tip:** Java caches Integer values from **-128 to 127** in a pool. So `Integer a = 100; Integer b = 100; a == b` is `true`! But `a = 200; b = 200; a == b` is `false`. Always use `.equals()` for Integer comparison!

</details>

---

<details>
<summary><b>Q42. What is the volatile keyword in Java?</b></summary>

> **One-Line Answer:** volatile ensures that a variable's value is always read from and written to main memory — not a thread's local cache — making changes visible across all threads.

### Code Example

```java
// WITHOUT volatile: thread 2 may never see thread 1's update!
class Worker {
    private boolean running = true;  // cached by threads
    void stop() { running = false; } // may not be visible to loop thread!
    void work() { while (running) { /* may loop forever */ } }
}

// WITH volatile: guaranteed visibility
private volatile boolean running = true;  // always in main memory
```

### volatile vs synchronized

| Feature | volatile | synchronized |
|---------|---------|-------------|
| Visibility guarantee | ✅ Yes | ✅ Yes |
| Atomicity | ❌ No (`count++` is not safe) | ✅ Yes |
| Performance | Faster (no lock) | Slower (lock overhead) |
| Use for | Simple flags/state | Complex operations |

> 💡 **Interview Tip:** volatile is ideal for stop-flag variables. Use AtomicInteger for counters, synchronized/locks for critical sections with multiple operations.

</details>

---

<details>
<summary><b>Q43. What is the difference between HashMap, LinkedHashMap, and TreeMap?</b></summary>

> **One-Line Answer:** HashMap is unordered. LinkedHashMap maintains insertion order. TreeMap maintains sorted order by keys.

### Comparison Table

| Feature | HashMap | LinkedHashMap | TreeMap |
|---------|---------|--------------|---------|
| Order | No order | Insertion order | Sorted (natural/custom) |
| Performance | O(1) avg | O(1) avg (slightly slower) | O(log n) |
| Null keys | ✅ One | ✅ One | ❌ No |
| Data structure | Hash table | Hash table + linked list | Red-Black Tree |
| Use when | Fast unordered lookup | Preserve insertion order | Sorted data needed |

</details>

---

<details>
<summary><b>Q44. What are design patterns? Name the most common ones.</b></summary>

> **One-Line Answer:** Design patterns are reusable solutions to commonly occurring software design problems. The 23 GoF patterns are grouped into Creational, Structural, and Behavioral categories.

### Most Common Design Patterns

| Category | Pattern | Simple Description |
|----------|---------|------------------|
| **Creational** | Singleton | Only one instance allowed (DB connection pool) |
| **Creational** | Factory Method | Delegate object creation to subclasses |
| **Creational** | Builder | Construct complex objects step by step |
| **Creational** | Prototype | Clone existing objects |
| **Structural** | Adapter | Convert one interface to another (power adapter analogy) |
| **Structural** | Decorator | Add functionality without changing original |
| **Structural** | Proxy | Wrapper that controls access to another object |
| **Behavioral** | Observer | Notify dependents when state changes (event listener) |
| **Behavioral** | Strategy | Swap algorithms at runtime |
| **Behavioral** | Template Method | Define skeleton of algorithm; subclass fills in steps |

### Singleton Example (Thread-safe)

```java
public class DatabaseConnection {
    private static volatile DatabaseConnection instance;

    private DatabaseConnection() {}  // private constructor

    public static DatabaseConnection getInstance() {
        if (instance == null) {
            synchronized (DatabaseConnection.class) {
                if (instance == null) {  // double-checked locking
                    instance = new DatabaseConnection();
                }
            }
        }
        return instance;
    }
}
```

> 💡 **Interview Tip:** Most commonly asked: Singleton, Factory, Builder, Observer, and Strategy. Know Singleton's double-checked locking for thread safety!

</details>

---

<details>
<summary><b>Q45. What is the difference between fail-fast and fail-safe iterators?</b></summary>

> **One-Line Answer:** Fail-fast iterators throw ConcurrentModificationException if the collection is modified during iteration. Fail-safe iterators work on a copy so they never throw.

### Comparison Table

| Feature | Fail-Fast | Fail-Safe |
|---------|----------|----------|
| Behavior on modification | Throws `ConcurrentModificationException` | No exception — uses a copy |
| Memory | No extra memory | Uses extra memory (copy) |
| Examples | ArrayList, HashMap iterators | CopyOnWriteArrayList, ConcurrentHashMap |
| Thread safety | ❌ Not thread-safe | ✅ Thread-safe |
| Returns latest data | ✅ Yes | ❌ May return stale data |

### Code Example

```java
// Fail-fast — will throw ConcurrentModificationException
List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));
for (String s : list) {
    list.remove(s);  // BOOM — ConcurrentModificationException!
}

// Fail-safe — safe to modify
List<String> list = new CopyOnWriteArrayList<>(Arrays.asList("A", "B", "C"));
for (String s : list) {
    list.remove(s);  // OK — iterating over a copy
}
```

> 💡 **Interview Tip:** To safely remove during iteration, use `Iterator.remove()` or iterate over a copy.

</details>

---

<details>
<summary><b>Q46. What is the difference between Stack and Heap memory?</b></summary>

> **One-Line Answer:** Stack stores method calls and primitive local variables (per-thread, auto-managed). Heap stores all objects (shared, managed by GC).

### Comparison Table

| Feature | Stack | Heap |
|---------|-------|------|
| Stores | Method frames, local vars, references | Objects, instance variables |
| Access | LIFO (Last In, First Out) | Random access |
| Managed by | Automatically (by JVM) | Garbage Collector |
| Per thread? | ✅ Yes — each thread has own stack | ❌ Shared among all threads |
| Size | Fixed (small) — configurable with -Xss | Large — configurable with -Xmx |
| Error if full | `StackOverflowError` | `OutOfMemoryError` |
| Speed | Faster | Slower |

### Code Example

```java
public void createPerson() {
    int age = 25;           // stored on STACK (primitive local variable)
    String name = "Alice";  // reference on STACK, String object on HEAP
    Person p = new Person(); // reference on STACK, Person object on HEAP
}
// When method returns, stack frame is cleared automatically
// Person object on heap lives until GC collects it
```

> 💡 **Interview Tip:** When a method returns, its stack frame is automatically cleared. Objects on the heap live as long as someone holds a reference to them — then GC reclaims them.

</details>

---

## 🔬 Java Internals & Deep Concepts

<details>
<summary><b>Q47. What is the difference between shallow copy and deep copy?</b></summary>

> **One-Line Answer:** Shallow copy copies the object reference — both copies point to the same nested objects. Deep copy creates a fully independent clone — changes in one do NOT affect the other.

### Visual Explanation

```
Shallow Copy:
original ──► [name="Alice", address ──► AddressObj]
copy     ──► [name="Alice", address ──► AddressObj]  ← SAME object!

Deep Copy:
original ──► [name="Alice", address ──► AddressObj1]
copy     ──► [name="Alice", address ──► AddressObj2]  ← NEW object!
```

### Code Example

```java
class Address {
    String city;
    Address(String city) { this.city = city; }
}

class Person implements Cloneable {
    String name;
    Address address;

    Person(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    // SHALLOW COPY — clone() default behavior
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();  // copies reference to address, not the object
    }

    // DEEP COPY — manually clone nested objects
    protected Person deepCopy() {
        return new Person(this.name, new Address(this.address.city));
    }
}

// Usage
Person original = new Person("Alice", new Address("Mumbai"));
Person shallow  = (Person) original.clone();
Person deep     = original.deepCopy();

original.address.city = "Delhi";
System.out.println(shallow.address.city);  // "Delhi" ← affected!
System.out.println(deep.address.city);     // "Mumbai" ← NOT affected
```

### Ways to Achieve Deep Copy

| Method | Notes |
|--------|-------|
| Manual copy constructor | Most explicit and safe |
| Override `clone()` recursively | Verbose, error-prone |
| Serialization/Deserialization | Easy but slow |
| Libraries (ModelMapper, MapStruct) | Best for production |

> 💡 **Interview Tip:** Java's default `clone()` is a shallow copy. Always use deep copy when your object has mutable nested objects (like lists, other objects).

</details>

---

<details>
<summary><b>Q48. What is the difference between instance initializer block, static initializer block, and constructor?</b></summary>

> **One-Line Answer:** Static block runs once when class loads. Instance block runs every time an object is created (before constructor). Constructor initializes the specific object.

### Execution Order

```java
class Demo {
    // 1. Static block — runs ONCE when class is first loaded
    static {
        System.out.println("1. Static block");
    }

    // 2. Instance block — runs EVERY time before constructor
    {
        System.out.println("2. Instance initializer block");
    }

    // 3. Constructor — runs EVERY time an object is created
    Demo() {
        System.out.println("3. Constructor");
    }
}

new Demo();
new Demo();

// Output:
// 1. Static block           ← only once!
// 2. Instance initializer block
// 3. Constructor
// 2. Instance initializer block
// 3. Constructor
```

### Comparison Table

| Feature | Static Block | Instance Block | Constructor |
|---------|-------------|---------------|-------------|
| Runs when | Class is first loaded | Every object creation | Every object creation |
| Runs how many times | Once | Once per object | Once per object |
| Has access to | Static members only | All members | All members |
| Can be overloaded | ❌ No | ❌ No | ✅ Yes |
| Use case | Load config, register drivers | Common init across constructors | Object-specific initialization |

> 💡 **Interview Tip:** Instance blocks are rarely used in practice, but great for interview discussions. They help share common initialization code across multiple constructors.

</details>

---

<details>
<summary><b>Q49. What is covariant return type in Java?</b></summary>

> **One-Line Answer:** Covariant return type allows an overriding method to return a more specific (subclass) type than the return type declared in the parent method.

### Code Example

```java
class Animal {
    Animal create() {
        return new Animal();
    }
}

class Dog extends Animal {
    @Override
    Dog create() {          // returns Dog (subtype of Animal) — VALID!
        return new Dog();
    }
}

// Without covariant return type (old Java), you'd need:
Animal a = new Dog().create();
Dog d = (Dog) a;  // explicit cast needed

// With covariant return type:
Dog d = new Dog().create();  // no cast needed!
```

> 💡 **Interview Tip:** Covariant return types make APIs cleaner by avoiding unnecessary casting. Widely used in Builder patterns and factory methods.

</details>

---

<details>
<summary><b>Q50. What is the difference between abstract class and interface with default methods (Java 8+)?</b></summary>

> **One-Line Answer:** After Java 8, interfaces can have default and static methods — making the line thinner. But abstract classes still support state (instance fields), constructors, and non-public methods.

### Remaining Differences After Java 8

| Feature | Abstract Class | Interface (Java 8+) |
|---------|--------------|---------------------|
| Instance fields/state | ✅ Yes | ❌ No (only constants) |
| Constructor | ✅ Yes | ❌ No |
| Default methods | ✅ Yes | ✅ Yes (since Java 8) |
| Static methods | ✅ Yes | ✅ Yes (since Java 8) |
| Private methods | ✅ Yes | ✅ Yes (since Java 9) |
| Access modifiers on methods | Any | public only |
| Multiple inheritance | ❌ No (extend one only) | ✅ Yes (implement many) |

### When to Choose Which?

```java
// Use ABSTRACT CLASS when:
// — you have shared state (fields) and common behavior
abstract class Template {
    private int retryCount = 3;  // state — interface can't do this
    abstract void process();
    void retry() { /* uses retryCount */ }
}

// Use INTERFACE when:
// — you want to define a contract that many unrelated classes follow
interface Auditable {
    default void log(String action) {
        System.out.println("Action: " + action);
    }
}
```

> 💡 **Interview Tip:** The golden rule — prefer interfaces for API design (multiple inheritance, no state). Use abstract classes when you need shared state or constructors.

</details>

---

<details>
<summary><b>Q51. What is method hiding in Java?</b></summary>

> **One-Line Answer:** Method hiding happens when a subclass defines a static method with the same name as a static method in the parent class. Unlike overriding, the method called depends on the reference type, not the actual object.

### Code Example

```java
class Parent {
    static void greet() { System.out.println("Parent greet"); }
    void hello()        { System.out.println("Parent hello"); }
}

class Child extends Parent {
    static void greet() { System.out.println("Child greet"); }  // HIDING
    @Override
    void hello()        { System.out.println("Child hello"); }  // OVERRIDING
}

Parent obj = new Child();

obj.greet();   // "Parent greet"  ← reference type decides (hiding)
obj.hello();   // "Child hello"   ← actual object decides (overriding)
```

### Hiding vs Overriding

| Feature | Method Hiding (static) | Method Overriding (instance) |
|---------|----------------------|------------------------------|
| Applies to | static methods | instance methods |
| Resolved at | Compile time (reference type) | Runtime (actual object type) |
| Polymorphism | ❌ No | ✅ Yes |
| @Override | Not applicable | Recommended |

> 💡 **Interview Tip:** Static methods cannot be overridden — they can only be hidden. This is a common interview trick question!

</details>

---

<details>
<summary><b>Q52. What is the instanceof operator?</b></summary>

> **One-Line Answer:** instanceof checks if an object is an instance of a specific class or implements a specific interface — returns true or false. Java 16+ introduced pattern matching with instanceof.

### Code Example

```java
Object obj = "Hello";

// Traditional instanceof
if (obj instanceof String) {
    String s = (String) obj;   // explicit cast still needed
    System.out.println(s.length());
}

// Java 16+ Pattern Matching instanceof (no cast needed!)
if (obj instanceof String s) {
    System.out.println(s.length());  // s is already a String here
}

// Works with inheritance
class Animal {}
class Dog extends Animal {}

Dog d = new Dog();
System.out.println(d instanceof Dog);    // true
System.out.println(d instanceof Animal); // true (Dog IS-A Animal)
System.out.println(d instanceof Object); // true (everything is Object)
```

> 💡 **Interview Tip:** Pattern matching instanceof (Java 16+) reduces boilerplate — no more cast after the check. Mention this to show you're up to date!

</details>

---

<details>
<summary><b>Q53. What is var (local variable type inference) in Java 10+?</b></summary>

> **One-Line Answer:** var lets the compiler infer the type of a local variable automatically — reducing boilerplate while keeping Java statically typed. It only works for local variables, not fields or method parameters.

### Code Example

```java
// Before Java 10 — verbose
ArrayList<Map<String, List<Integer>>> data = new ArrayList<Map<String, List<Integer>>>();
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));

// Java 10+ with var — cleaner!
var data   = new ArrayList<Map<String, List<Integer>>>();
var reader = new BufferedReader(new FileReader("file.txt"));

// Works in for loops
var list = List.of("Alice", "Bob", "Charlie");
for (var name : list) {
    System.out.println(name.toUpperCase());  // name is inferred as String
}
```

### Rules for var

| Allowed ✅ | Not Allowed ❌ |
|-----------|--------------|
| Local variables | Class fields |
| For loop variables | Method parameters |
| Try-with-resources | Return types |
| Lambda parameters (Java 11) | Array initializer shortcut |

> 💡 **Interview Tip:** var is still statically typed — the type is fixed at compile time, not runtime. It's syntax sugar only, not like JavaScript's dynamic typing.

</details>

---

## 🧵 Advanced Multi-threading

<details>
<summary><b>Q54. What is the difference between synchronized and ReentrantLock?</b></summary>

> **One-Line Answer:** synchronized is simple and automatic. ReentrantLock is more flexible — supports tryLock, fairness policy, multiple conditions, and interruptible locking.

### Comparison Table

| Feature | synchronized | ReentrantLock |
|---------|-------------|--------------|
| Lock type | Implicit (JVM managed) | Explicit (manual lock/unlock) |
| Fairness | ❌ Not guaranteed | ✅ Optional fair mode |
| tryLock | ❌ No | ✅ Yes — non-blocking attempt |
| Interruptible | ❌ No | ✅ Yes — lockInterruptibly() |
| Multiple conditions | ❌ No | ✅ Yes — newCondition() |
| Ease of use | Simple | More complex |
| Performance | Good | Slightly better under contention |

### Code Example

```java
import java.util.concurrent.locks.ReentrantLock;

class SafeCounter {
    private int count = 0;
    private final ReentrantLock lock = new ReentrantLock();

    void increment() {
        lock.lock();           // acquire lock
        try {
            count++;
        } finally {
            lock.unlock();     // ALWAYS release in finally!
        }
    }

    void tryIncrement() {
        if (lock.tryLock()) {  // non-blocking — returns false if locked
            try {
                count++;
            } finally {
                lock.unlock();
            }
        } else {
            System.out.println("Could not acquire lock, skipping");
        }
    }
}
```

> 💡 **Interview Tip:** Always call `unlock()` inside a `finally` block with ReentrantLock — otherwise a thrown exception will leave the lock permanently acquired (deadlock!).

</details>

---

<details>
<summary><b>Q55. What is ExecutorService and thread pool?</b></summary>

> **One-Line Answer:** ExecutorService manages a pool of threads — reusing them for tasks instead of creating/destroying threads for each task, which is expensive.

### Why Use Thread Pools?

- Creating a thread costs ~1MB of memory and ~100ms startup time
- Thread pools reuse threads — submit tasks, threads pick them up
- Prevents system overload from unlimited thread creation

### Types of Thread Pools

| Pool Type | Method | Best For |
|-----------|--------|----------|
| Fixed Thread Pool | `newFixedThreadPool(n)` | CPU-bound tasks with known concurrency |
| Cached Thread Pool | `newCachedThreadPool()` | Many short-lived tasks |
| Single Thread Executor | `newSingleThreadExecutor()` | Sequential task execution |
| Scheduled Thread Pool | `newScheduledThreadPool(n)` | Recurring/delayed tasks |
| ForkJoinPool | `ForkJoinPool.commonPool()` | Parallel recursive tasks |

### Code Example

```java
ExecutorService pool = Executors.newFixedThreadPool(4);

// Submit Runnable (no return value)
pool.submit(() -> System.out.println("Task 1"));

// Submit Callable (returns a value via Future)
Future<Integer> future = pool.submit(() -> {
    Thread.sleep(1000);
    return 42;
});

System.out.println("Result: " + future.get());  // blocks until done

// Always shutdown!
pool.shutdown();             // waits for running tasks to finish
pool.awaitTermination(10, TimeUnit.SECONDS);
```

> 💡 **Interview Tip:** Always call `shutdown()` on ExecutorService — otherwise threads stay alive and the JVM won't exit. Use `shutdownNow()` to cancel pending tasks immediately.

</details>

---

<details>
<summary><b>Q56. What is the difference between Callable and Runnable?</b></summary>

> **One-Line Answer:** Runnable represents a task with no return value and cannot throw checked exceptions. Callable can return a result (via Future) and can throw checked exceptions.

### Comparison Table

| Feature | Runnable | Callable<V> |
|---------|---------|------------|
| Method | `void run()` | `V call() throws Exception` |
| Return value | ❌ None | ✅ Returns V |
| Throws checked exception | ❌ No | ✅ Yes |
| Used with | Thread, ExecutorService | ExecutorService only |
| Result access | N/A | Via `Future<V>.get()` |
| Introduced | Java 1.0 | Java 5 |

### Code Example

```java
// Runnable — fire and forget
Runnable task = () -> System.out.println("Running!");
new Thread(task).start();

// Callable — get a result back
Callable<String> callable = () -> {
    Thread.sleep(500);
    return "Done!";
};

ExecutorService pool = Executors.newSingleThreadExecutor();
Future<String> future = pool.submit(callable);

// future.get() blocks until Callable finishes
String result = future.get();
System.out.println(result);  // "Done!"
pool.shutdown();
```

> 💡 **Interview Tip:** `Future.get()` blocks the calling thread. Use `future.isDone()` to check without blocking, or `CompletableFuture` for fully async chaining.

</details>

---

<details>
<summary><b>Q57. What is CompletableFuture in Java?</b></summary>

> **One-Line Answer:** CompletableFuture (Java 8) provides a fully non-blocking, chainable way to write async code — like a Promise in JavaScript. It eliminates callback hell and blocking Future.get() calls.

### Code Example

```java
// Basic async task
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    // runs in a separate thread (ForkJoinPool by default)
    return "Hello";
});

// Chain transformations
CompletableFuture<String> result = CompletableFuture
    .supplyAsync(() -> "Hello")
    .thenApply(s -> s + " World")       // transform result
    .thenApply(String::toUpperCase);    // transform again

System.out.println(result.get());  // "HELLO WORLD"

// Combine two futures
CompletableFuture<String> userFuture = CompletableFuture.supplyAsync(() -> "Alice");
CompletableFuture<Integer> ageFuture = CompletableFuture.supplyAsync(() -> 25);

CompletableFuture<String> combined = userFuture.thenCombine(ageFuture,
    (name, age) -> name + " is " + age);

System.out.println(combined.get());  // "Alice is 25"

// Error handling
CompletableFuture<String> safe = CompletableFuture
    .supplyAsync(() -> { throw new RuntimeException("Oops!"); })
    .exceptionally(ex -> "Default value");

System.out.println(safe.get());  // "Default value"
```

### Key Methods

| Method | Purpose |
|--------|---------|
| `supplyAsync()` | Run async task that returns value |
| `runAsync()` | Run async task with no return value |
| `thenApply()` | Transform result (like map) |
| `thenAccept()` | Consume result (like forEach) |
| `thenCombine()` | Combine two futures |
| `exceptionally()` | Handle errors, provide default |
| `allOf()` | Wait for all futures to complete |
| `anyOf()` | Continue when ANY future completes |

> 💡 **Interview Tip:** CompletableFuture is the modern replacement for Future. It's central to reactive and async programming in Java — a must-know for senior roles.

</details>

---

## 🗂️ Java Data Structures & Algorithms

<details>
<summary><b>Q58. What is a Stack in Java? How to implement it?</b></summary>

> **One-Line Answer:** Stack is a LIFO (Last In, First Out) data structure. Java provides the Stack class (legacy) and ArrayDeque (recommended modern alternative).

### Code Example

```java
// Legacy Stack class (extends Vector — avoid in new code)
Stack<Integer> stack = new Stack<>();
stack.push(10);
stack.push(20);
stack.push(30);
System.out.println(stack.peek());  // 30 — view top without removing
System.out.println(stack.pop());   // 30 — remove top
System.out.println(stack.isEmpty()); // false

// Modern Approach — ArrayDeque as Stack (RECOMMENDED)
Deque<Integer> deque = new ArrayDeque<>();
deque.push(10);  // addFirst
deque.push(20);
deque.peek();    // peekFirst
deque.pop();     // removeFirst
```

### Real-World Uses of Stack

| Use Case | How Stack Helps |
|----------|----------------|
| Undo/Redo operations | Push actions, pop to undo |
| Browser back button | Push visited pages |
| Expression evaluation | Parse and evaluate math expressions |
| Method call tracking | JVM call stack |
| Balanced parentheses check | Push open, pop on close |

> 💡 **Interview Tip:** Always use `ArrayDeque` instead of `Stack` class. `Stack` extends `Vector` (synchronized), which adds unnecessary overhead. `ArrayDeque` is faster and not thread-safe (which is fine for most use cases).

</details>

---

<details>
<summary><b>Q59. What is a Queue in Java? What are its implementations?</b></summary>

> **One-Line Answer:** Queue is a FIFO (First In, First Out) data structure. Java offers LinkedList, ArrayDeque, PriorityQueue as implementations, and BlockingQueue variants for thread-safe operations.

### Queue Implementations

| Class | Type | Use Case |
|-------|------|----------|
| `ArrayDeque` | Regular Queue/Deque | General purpose (fast, non-thread-safe) |
| `LinkedList` | Queue/Deque | Also a List — flexible but more memory |
| `PriorityQueue` | Priority Queue | Elements dequeued by natural order or comparator |
| `ArrayBlockingQueue` | Blocking Queue | Thread-safe, bounded — producer/consumer |
| `LinkedBlockingQueue` | Blocking Queue | Thread-safe, optionally bounded |
| `ConcurrentLinkedQueue` | Lock-free Queue | High-concurrency scenarios |

### Code Example

```java
// Regular Queue
Queue<String> queue = new LinkedList<>();
queue.offer("Alice");   // add to tail (prefer offer over add)
queue.offer("Bob");
queue.offer("Charlie");

System.out.println(queue.peek());  // "Alice" — view head without removing
System.out.println(queue.poll());  // "Alice" — remove head (prefer poll over remove)
System.out.println(queue.size());  // 2

// PriorityQueue — dequeues smallest first
Queue<Integer> pq = new PriorityQueue<>();
pq.offer(30); pq.offer(10); pq.offer(20);
System.out.println(pq.poll());  // 10 (smallest first)
System.out.println(pq.poll());  // 20

// BlockingQueue — for producer-consumer pattern
BlockingQueue<String> bq = new ArrayBlockingQueue<>(10);
bq.put("task1");             // blocks if full
String task = bq.take();     // blocks if empty
```

> 💡 **Interview Tip:** Use `offer()`/`poll()` instead of `add()`/`remove()` — they return false/null instead of throwing exceptions when the queue is full/empty.

</details>

---

<details>
<summary><b>Q60. What is the difference between Iterator and ListIterator?</b></summary>

> **One-Line Answer:** Iterator can traverse any Collection in one direction (forward only). ListIterator is specific to List and supports bidirectional traversal, plus add/set operations during iteration.

### Comparison Table

| Feature | Iterator | ListIterator |
|---------|---------|-------------|
| Works with | Any Collection | List only |
| Direction | Forward only | Forward AND backward |
| Add elements | ❌ No | ✅ Yes |
| Replace elements | ❌ No | ✅ Yes (set()) |
| Get index | ❌ No | ✅ nextIndex() / previousIndex() |

### Code Example

```java
List<String> names = new ArrayList<>(Arrays.asList("Alice", "Bob", "Charlie"));

// Iterator — forward only
Iterator<String> it = names.iterator();
while (it.hasNext()) {
    String name = it.next();
    if (name.equals("Bob")) {
        it.remove();  // safe removal during iteration
    }
}

// ListIterator — bidirectional
ListIterator<String> lit = names.listIterator();
while (lit.hasNext()) {
    String name = lit.next();
    lit.set(name.toUpperCase());  // replace element
}
// traverse backwards
while (lit.hasPrevious()) {
    System.out.println(lit.previous());
}
```

> 💡 **Interview Tip:** Never modify a collection directly during iteration — always use `iterator.remove()` to avoid `ConcurrentModificationException`.

</details>

---

## 🌐 Java 8+ Modern Features

<details>
<summary><b>Q61. What are Method References in Java 8?</b></summary>

> **One-Line Answer:** Method references are a shorthand for lambdas that call an existing method — cleaner and more readable. Syntax: `ClassName::methodName`.

### 4 Types of Method References

| Type | Syntax | Equivalent Lambda |
|------|--------|-----------------|
| Static method | `Class::staticMethod` | `x -> Class.staticMethod(x)` |
| Instance method (specific object) | `obj::instanceMethod` | `x -> obj.instanceMethod(x)` |
| Instance method (arbitrary object) | `Class::instanceMethod` | `x -> x.instanceMethod()` |
| Constructor | `Class::new` | `x -> new Class(x)` |

### Code Example

```java
List<String> names = Arrays.asList("Charlie", "Alice", "Bob");

// Lambda way
names.forEach(name -> System.out.println(name));
names.sort((a, b) -> a.compareTo(b));

// Method reference way (cleaner!)
names.forEach(System.out::println);          // instance on specific object
names.sort(String::compareTo);               // instance on arbitrary object
names.replaceAll(String::toUpperCase);       // instance on arbitrary object

// Static method reference
List<String> filtered = names.stream()
    .filter(Objects::nonNull)                 // static method
    .collect(Collectors.toList());

// Constructor reference
List<Integer> nums = Arrays.asList(1, 2, 3);
List<String> strings = nums.stream()
    .map(String::valueOf)                     // static method ref
    .collect(Collectors.toList());
```

> 💡 **Interview Tip:** Method references are just syntactic sugar for lambdas — the compiler converts them. Use them to improve readability when the lambda just calls an existing method.

</details>

---

<details>
<summary><b>Q62. What are default and static methods in Java 8 interfaces?</b></summary>

> **One-Line Answer:** Default methods allow interfaces to have method implementations without breaking existing implementing classes. Static methods in interfaces are utility methods called on the interface itself.

### Why Were They Introduced?

Before Java 8, adding a new method to an interface would break ALL implementing classes. Default methods solve this — existing classes inherit the default implementation automatically.

### Code Example

```java
interface Greeting {
    // Abstract method — must be implemented
    String greet(String name);

    // Default method — optional to override
    default String greetLoudly(String name) {
        return greet(name).toUpperCase();  // reuses abstract method
    }

    // Static method — called on the interface itself
    static String defaultGreet() {
        return "Hello, stranger!";
    }
}

class FriendlyGreeting implements Greeting {
    @Override
    public String greet(String name) { return "Hi, " + name + "!"; }
    // greetLoudly() inherited for free!
}

// Usage
FriendlyGreeting fg = new FriendlyGreeting();
System.out.println(fg.greet("Alice"));       // "Hi, Alice!"
System.out.println(fg.greetLoudly("Alice")); // "HI, ALICE!"
System.out.println(Greeting.defaultGreet()); // "Hello, stranger!"
```

### Default Method Diamond Problem

```java
interface A { default void hello() { System.out.println("A"); } }
interface B { default void hello() { System.out.println("B"); } }

class C implements A, B {
    @Override
    public void hello() {
        A.super.hello();  // must explicitly resolve the conflict
    }
}
```

> 💡 **Interview Tip:** If a class implements two interfaces with the same default method, it MUST override that method to resolve the ambiguity — or the compiler will give an error.

</details>

---

<details>
<summary><b>Q63. What is the new Date and Time API in Java 8?</b></summary>

> **One-Line Answer:** Java 8 introduced java.time package — immutable, thread-safe date/time classes (LocalDate, LocalTime, LocalDateTime, ZonedDateTime) that replace the buggy, mutable Calendar and Date classes.

### Old (Broken) vs New (Java 8)

| Old Class | Problem | Java 8 Replacement |
|-----------|---------|-------------------|
| `java.util.Date` | Mutable, confusing API | `LocalDate`, `LocalDateTime` |
| `java.util.Calendar` | Verbose, buggy (months are 0-indexed!) | `LocalDate`, `ZonedDateTime` |
| `SimpleDateFormat` | Not thread-safe | `DateTimeFormatter` |

### Code Example

```java
// LocalDate — date only (no time, no timezone)
LocalDate today = LocalDate.now();
LocalDate birthday = LocalDate.of(1995, Month.JUNE, 15);
LocalDate nextWeek = today.plusDays(7);
long daysBetween = ChronoUnit.DAYS.between(birthday, today);

// LocalTime — time only
LocalTime now = LocalTime.now();
LocalTime meeting = LocalTime.of(14, 30, 0);

// LocalDateTime — date + time (no timezone)
LocalDateTime event = LocalDateTime.of(2025, 12, 31, 23, 59);

// ZonedDateTime — with timezone
ZonedDateTime mumbaiTime = ZonedDateTime.now(ZoneId.of("Asia/Kolkata"));

// Formatting
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
String formatted = today.format(formatter);  // "19/03/2026"
LocalDate parsed = LocalDate.parse("25/12/2025", formatter);
```

> 💡 **Interview Tip:** The Java 8 Date/Time API is immutable — methods like `plusDays()` return a NEW object, they don't modify the original. This makes it thread-safe!

</details>

---

<details>
<summary><b>Q64. What are Streams — parallel streams vs sequential streams?</b></summary>

> **One-Line Answer:** Sequential streams process elements one at a time in order. Parallel streams split the work across multiple CPU cores using the ForkJoinPool — faster for large datasets, but has ordering and thread-safety caveats.

### Code Example

```java
List<Integer> numbers = IntStream.rangeClosed(1, 1_000_000)
                                 .boxed()
                                 .collect(Collectors.toList());

// Sequential stream — single thread, ordered
long sumSeq = numbers.stream()
                     .mapToLong(Integer::longValue)
                     .sum();

// Parallel stream — multiple threads, unordered
long sumPar = numbers.parallelStream()
                     .mapToLong(Integer::longValue)
                     .sum();
// (both give same result for sum, but parallel is faster on large data)
```

### Sequential vs Parallel

| Feature | Sequential | Parallel |
|---------|-----------|---------|
| Threads | Single | Multiple (ForkJoinPool) |
| Order | Guaranteed | Not guaranteed |
| Overhead | Low | Higher (thread coordination) |
| Good for | Small data, ordered ops | Large data, independent ops |
| Thread-safety required | ❌ No | ✅ Yes (shared state) |

### When NOT to Use Parallel Streams

```java
// BAD — shared mutable state in parallel stream (race condition!)
List<Integer> result = new ArrayList<>();  // not thread-safe!
numbers.parallelStream().forEach(result::add);  // data corruption!

// GOOD — use thread-safe collectors instead
List<Integer> result = numbers.parallelStream()
                              .filter(n -> n % 2 == 0)
                              .collect(Collectors.toList());  // safe!
```

> 💡 **Interview Tip:** Parallel streams are NOT always faster! For small lists, thread creation overhead outweighs benefits. Benchmark before using parallelStream() in production.

</details>

---

## 🏗️ Java Design & Patterns

<details>
<summary><b>Q65. What is the Builder Pattern? When to use it?</b></summary>

> **One-Line Answer:** Builder Pattern constructs complex objects step-by-step with a fluent API — avoiding telescoping constructors and making object creation readable and flexible.

### The Problem It Solves

```java
// PROBLEM: Telescoping constructor anti-pattern
new Person("Alice", 25, "Mumbai", "alice@email.com", "9876543210", true, false);
// What does 'true, false' mean? Impossible to tell!

// SOLUTION: Builder Pattern
Person alice = new Person.Builder("Alice", 25)
    .city("Mumbai")
    .email("alice@email.com")
    .phone("9876543210")
    .premiumMember(true)
    .build();
```

### Full Builder Pattern Example

```java
public class Person {
    // All fields final — truly immutable!
    private final String name;
    private final int age;
    private final String city;
    private final String email;

    // Private constructor — only Builder can call this
    private Person(Builder builder) {
        this.name  = builder.name;
        this.age   = builder.age;
        this.city  = builder.city;
        this.email = builder.email;
    }

    // Static nested Builder class
    public static class Builder {
        private final String name;  // required
        private final int age;      // required
        private String city;        // optional
        private String email;       // optional

        public Builder(String name, int age) {
            this.name = name;
            this.age  = age;
        }
        public Builder city(String city)   { this.city = city;   return this; }
        public Builder email(String email) { this.email = email; return this; }
        public Person build()              { return new Person(this); }
    }
}
```

> 💡 **Interview Tip:** Lombok's `@Builder` annotation generates all this boilerplate automatically. But understanding the manual implementation shows you know what's happening under the hood.

</details>

---

<details>
<summary><b>Q66. What is the Singleton Pattern? How to make it thread-safe?</b></summary>

> **One-Line Answer:** Singleton ensures only ONE instance of a class exists in the JVM. Thread-safe implementation requires double-checked locking with volatile, or the enum-based approach.

### 4 Ways to Implement Singleton

```java
// 1. EAGER INITIALIZATION — simple, but creates instance even if never used
public class Singleton {
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() {}
    public static Singleton getInstance() { return INSTANCE; }
}

// 2. LAZY INITIALIZATION — not thread-safe!
public class Singleton {
    private static Singleton instance;
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {           // race condition here!
            instance = new Singleton();
        }
        return instance;
    }
}

// 3. DOUBLE-CHECKED LOCKING — thread-safe and lazy
public class Singleton {
    private static volatile Singleton instance;  // volatile is crucial!
    private Singleton() {}
    public static Singleton getInstance() {
        if (instance == null) {
            synchronized (Singleton.class) {
                if (instance == null) {   // second check inside sync block
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}

// 4. ENUM — best approach! Thread-safe, serialization-safe, reflection-safe
public enum Singleton {
    INSTANCE;
    public void doSomething() { /* ... */ }
}
// Usage: Singleton.INSTANCE.doSomething();
```

### Why volatile in Double-Checked Locking?

Without `volatile`, the JVM can reorder instructions — another thread might see a partially constructed object. `volatile` prevents instruction reordering.

> 💡 **Interview Tip:** The **enum** singleton is the recommended approach by Joshua Bloch (Effective Java). It's immune to reflection attacks, serialization issues, and is automatically thread-safe.

</details>

---

<details>
<summary><b>Q67. What is the Observer Pattern in Java?</b></summary>

> **One-Line Answer:** Observer Pattern defines a one-to-many dependency — when the subject (publisher) changes state, all registered observers (subscribers) are automatically notified.

### Code Example

```java
import java.util.ArrayList;
import java.util.List;

// Subject (Publisher)
interface Subject {
    void subscribe(Observer o);
    void unsubscribe(Observer o);
    void notifyObservers(String event);
}

// Observer (Subscriber)
interface Observer {
    void update(String event);
}

// Concrete Subject
class EventSystem implements Subject {
    private List<Observer> observers = new ArrayList<>();

    @Override public void subscribe(Observer o)   { observers.add(o); }
    @Override public void unsubscribe(Observer o) { observers.remove(o); }
    @Override public void notifyObservers(String event) {
        observers.forEach(o -> o.update(event));
    }

    public void triggerEvent(String event) {
        System.out.println("Event: " + event);
        notifyObservers(event);
    }
}

// Concrete Observer
class EmailNotifier implements Observer {
    @Override
    public void update(String event) {
        System.out.println("Email sent for: " + event);
    }
}

// Usage
EventSystem es = new EventSystem();
es.subscribe(new EmailNotifier());
es.subscribe(event -> System.out.println("SMS sent for: " + event));  // lambda!
es.triggerEvent("New Order");
// Output:
// Event: New Order
// Email sent for: New Order
// SMS sent for: New Order
```

> 💡 **Interview Tip:** Java's `java.util.Observable` class and `Observer` interface are deprecated (Java 9+). In modern Java, use reactive streams (RxJava, Reactor) for event-driven programming.

</details>

---

## 🔐 Java Memory & Performance

<details>
<summary><b>Q68. What is memory leak in Java? How to prevent it?</b></summary>

> **One-Line Answer:** A memory leak in Java happens when objects are no longer needed but still referenced — preventing GC from reclaiming that memory. Java's GC doesn't prevent memory leaks, it only collects unreachable objects.

### Common Causes of Memory Leaks

```java
// 1. STATIC COLLECTIONS growing forever
class Cache {
    static Map<String, Object> cache = new HashMap<>();
    void store(String key, Object val) {
        cache.put(key, val);  // never cleaned — grows forever!
    }
}

// 2. Unregistered Listeners / Observers
button.addActionListener(myListener);
// If you never remove myListener, it holds a reference forever

// 3. Unclosed Resources
Connection conn = getConnection();
// If exception before conn.close() — leak! Use try-with-resources instead

// 4. ThreadLocal variables not removed
ThreadLocal<Object> tl = new ThreadLocal<>();
tl.set(bigObject);
// When thread is pooled (ExecutorService), the ThreadLocal persists!
// FIX:
try {
    tl.set(bigObject);
    // use it...
} finally {
    tl.remove();  // always clean up!
}
```

### Prevention Strategies

| Strategy | How It Helps |
|----------|-------------|
| Use `WeakReference` for caches | GC can collect even if reference exists |
| Always close resources (try-with-resources) | Prevents unclosed I/O leaks |
| Unregister listeners | Prevents listener accumulation |
| Clear ThreadLocal in finally | Prevents thread pool leaks |
| Use `WeakHashMap` for caches | Keys collected by GC when no strong ref |

### Detection Tools

- **VisualVM** — Heap dump analysis, memory profiling
- **JProfiler** — Professional profiler
- **Eclipse MAT (Memory Analyzer Tool)** — Heap dump analysis
- **JVM flags** — `-Xmx`, `-verbose:gc`, `-XX:+HeapDumpOnOutOfMemoryError`

> 💡 **Interview Tip:** Java prevents dangling pointers but NOT memory leaks. Leaks happen when you hold references you no longer need. The most common real-world leak: static collections and unclosed database connections.

</details>

---

<details>
<summary><b>Q69. What is String interning in Java?</b></summary>

> **One-Line Answer:** String interning places a String into the String Pool — so that identical strings share the same memory. Calling `intern()` on a String returns the pooled version.

### How It Works

```java
String s1 = new String("Java");  // creates new object in heap (NOT pool)
String s2 = new String("Java");  // another new object
String s3 = "Java";              // from pool
String s4 = "Java";              // same pool object

System.out.println(s1 == s2);     // false — different heap objects
System.out.println(s3 == s4);     // true  — same pool object
System.out.println(s1 == s3);     // false — s1 not in pool

// intern() — move to pool
String s5 = s1.intern();          // returns pool version
System.out.println(s5 == s3);     // true!
System.out.println(s5 == s1);     // false! (s1 still points to heap object)
```

### When to Use intern()

```java
// Good use: store many duplicate strings (e.g., country codes from DB)
// Without interning: 1 million rows × "INDIA" = 1 million String objects
// With interning: 1 million rows × "INDIA" = 1 String object in pool
```

> 💡 **Interview Tip:** The String Pool is stored in Metaspace (since Java 8). Don't overuse intern() — the pool has a fixed size and can cause performance issues if overloaded.

</details>

---

## 📝 Java Best Practices & Miscellaneous

<details>
<summary><b>Q70. What is the difference between checked and runtime exceptions? When to use which?</b></summary>

> **One-Line Answer:** Use checked exceptions for recoverable external failures (file not found, network timeout). Use unchecked (runtime) exceptions for programming errors and unrecoverable conditions.

### Decision Guide

```
Is the caller ABLE to recover from this error?
├── YES → Checked Exception (caller must handle it)
│         e.g., FileNotFoundException — caller can ask user for another file
└── NO  → Runtime Exception (don't force caller to handle)
          e.g., NullPointerException — indicates a bug, not a scenario
```

### Common Exception Hierarchy

| Exception | Type | When Thrown |
|-----------|------|-------------|
| `IOException` | Checked | File/network I/O issues |
| `SQLException` | Checked | Database errors |
| `ClassNotFoundException` | Checked | Class not found at runtime |
| `NullPointerException` | Unchecked | Accessing null reference |
| `IllegalArgumentException` | Unchecked | Invalid method argument |
| `IllegalStateException` | Unchecked | Wrong state to call this method |
| `UnsupportedOperationException` | Unchecked | Operation not supported |
| `IndexOutOfBoundsException` | Unchecked | Invalid array/list index |

### Best Practice: Custom Exception

```java
// Good custom exception design
public class OrderNotFoundException extends RuntimeException {
    private final Long orderId;

    public OrderNotFoundException(Long orderId) {
        super("Order not found with ID: " + orderId);
        this.orderId = orderId;
    }

    public Long getOrderId() { return orderId; }
}
```

> 💡 **Interview Tip:** Modern Java convention (and Spring's approach): prefer **unchecked** exceptions. Checked exceptions leak implementation details and make APIs harder to use. Always include meaningful messages.

</details>

---

<details>
<summary><b>Q71. What is the difference between mutable and immutable objects? How to create an immutable class?</b></summary>

> **One-Line Answer:** Mutable objects can be changed after creation. Immutable objects cannot — every "modification" returns a new object. Immutable objects are thread-safe by nature.

### Rules to Create an Immutable Class

1. Declare the class `final` (prevent subclassing)
2. Make all fields `private` and `final`
3. No setter methods
4. Initialize all fields via constructor
5. Return deep copies of mutable fields (like lists)

### Code Example

```java
public final class ImmutablePerson {
    private final String name;
    private final int age;
    private final List<String> hobbies;  // mutable field — needs deep copy!

    public ImmutablePerson(String name, int age, List<String> hobbies) {
        this.name    = name;
        this.age     = age;
        this.hobbies = new ArrayList<>(hobbies);  // defensive copy on creation
    }

    public String getName()         { return name; }
    public int getAge()             { return age; }
    public List<String> getHobbies() {
        return Collections.unmodifiableList(hobbies);  // return unmodifiable view
    }
    // NO setters!
}
```

### Benefits of Immutability

| Benefit | Explanation |
|---------|-------------|
| Thread-safe | Can be shared across threads without synchronization |
| Cacheable | Safe to cache (String pool, Integer cache) |
| Reliable | State never changes unexpectedly |
| Good Map keys | Hashcode is stable (prerequisite for HashMap keys) |

> 💡 **Interview Tip:** Java's built-in immutable classes: `String`, `Integer`, `BigDecimal`, `LocalDate`. Java 16+ records (`record Person(String name, int age) {}`) create immutable classes automatically!

</details>

---

<details>
<summary><b>Q72. What is the difference between transient, volatile, and synchronized?</b></summary>

> **One-Line Answer:** transient = skip this field during serialization. volatile = ensure field is read/written to main memory (visibility). synchronized = ensure only one thread enters a block at a time (atomicity + visibility).

### Comparison Table

| Keyword | Applied To | Purpose | Thread-Related? |
|---------|-----------|---------|----------------|
| `transient` | Fields | Skip during Java serialization | ❌ No |
| `volatile` | Fields | Guarantee main memory visibility | ✅ Yes |
| `synchronized` | Methods/Blocks | Mutual exclusion + visibility | ✅ Yes |

### Code Example

```java
class UserSession implements Serializable {
    String username;          // will be serialized
    transient String password; // NOT serialized (sensitive data!)
    transient Connection conn; // NOT serialized (can't serialize a connection!)

    volatile boolean isLoggedIn;  // visible to all threads immediately

    synchronized void logout() {  // only one thread at a time
        isLoggedIn = false;
        // cleanup...
    }
}
```

> 💡 **Interview Tip:** `transient` and `volatile` are frequently confused. Remember: `transient` = "skip in file/network", `volatile` = "always use RAM, not CPU cache". They solve completely different problems.

</details>

---

## 📊 Quick Comparison Tables Reference

### Collections at a Glance

| Collection | Ordered? | Duplicates? | Null? | Thread-safe? | Performance |
|-----------|---------|------------|-------|-------------|-------------|
| ArrayList | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No | O(1) access |
| LinkedList | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No | O(1) insert/delete at ends |
| HashSet | ❌ No | ❌ No | ✅ One | ❌ No | O(1) avg |
| LinkedHashSet | ✅ Insertion | ❌ No | ✅ One | ❌ No | O(1) avg |
| TreeSet | ✅ Sorted | ❌ No | ❌ No | ❌ No | O(log n) |
| HashMap | ❌ No | Keys: No | ✅ One key | ❌ No | O(1) avg |
| LinkedHashMap | ✅ Insertion | Keys: No | ✅ One key | ❌ No | O(1) avg |
| TreeMap | ✅ Sorted | Keys: No | ❌ No | ❌ No | O(log n) |
| ConcurrentHashMap | ❌ No | Keys: No | ❌ No | ✅ Yes | O(1) avg |

---

### String Classes at a Glance

| Feature | String | StringBuffer | StringBuilder |
|---------|--------|-------------|--------------|
| Mutable | ❌ No | ✅ Yes | ✅ Yes |
| Thread-safe | ✅ Yes | ✅ Yes (sync) | ❌ No |
| Speed | Slow (new objects) | Medium | Fast |
| Best for | Constants | Multi-threaded concat | Single-threaded concat |

---

### OOP Pillars Summary

| Pillar | Keyword | Purpose | Violation Example |
|--------|---------|---------|------------------|
| Encapsulation | `private` + getters | Hide internal state | Public fields |
| Inheritance | `extends` | Code reuse | Copy-pasting code |
| Polymorphism | `@Override` | Flexibility | Hard-coded type checks |
| Abstraction | `abstract`/`interface` | Hide complexity | Exposing implementation |

---

### Exception Types at a Glance

| Category | Examples | Must Handle? | Represents |
|----------|---------|-------------|-----------|
| **Checked** | IOException, SQLException | ✅ Yes | External failures |
| **Unchecked** | NullPointerException, IllegalArgumentException | ❌ No | Programming bugs |
| **Error** | OutOfMemoryError, StackOverflowError | ❌ No (don't catch) | JVM-level problems |

---

### Thread Creation Methods Comparison

| Method | Returns Result? | Throws Exception? | Thread Management |
|--------|---------------|-----------------|-----------------|
| `Thread + Runnable` | ❌ No | ❌ No | Manual |
| `Callable + Future` | ✅ Yes | ✅ Yes | Via ExecutorService |
| `CompletableFuture` | ✅ Yes | ✅ Yes | Auto (ForkJoinPool) |

---

### Java Version Feature Summary

| Java Version | Key Features |
|-------------|-------------|
| **Java 8** | Lambdas, Streams, Optional, Default methods, New Date/Time API |
| **Java 9** | Module system, JShell, Private interface methods |
| **Java 10** | `var` (local variable type inference) |
| **Java 11** | `String` methods (isBlank, strip), `Files` methods, HTTP Client |
| **Java 14** | Switch expressions (standard), Records (preview) |
| **Java 16** | Records (standard), `instanceof` pattern matching |
| **Java 17** | Sealed classes, Pattern matching for switch (preview) |
| **Java 21** | Virtual threads (Project Loom), Pattern matching finalized |

---

*Happy Interview Preparation! ☕ — Remember: Understand the concept, then explain it simply with a real-world example.*
