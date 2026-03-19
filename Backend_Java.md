# ☕ Java Backend Interview Questions

> **50+ Questions** | Organized by topic | Open/Close Accordions | Comparison Tables | Clear Explanations

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
- [Spring Framework](#-spring-framework)
- [Bonus Questions](#-bonus-questions)

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

## 🌿 Spring Framework

<details>
<summary><b>Q36. What is the difference between RestTemplate and WebClient?</b></summary>

> **One-Line Answer:** RestTemplate is the classic blocking HTTP client (deprecated in Spring 6). WebClient is the modern non-blocking reactive HTTP client — supports both sync and async calls.

### Comparison Table

| Feature | RestTemplate | WebClient |
|---------|-------------|-----------|
| Introduced in | Spring 3 | Spring 5 (WebFlux) |
| Blocking? | ✅ Blocking (synchronous) | ❌ Non-blocking (reactive) |
| Async support | Limited | ✅ Full async/reactive |
| Status (Spring 6) | Deprecated | Recommended |
| Return type | Direct objects | `Mono<T>` / `Flux<T>` |
| Thread model | One thread per request | Event loop — fewer threads |

### Code Example

```java
// RestTemplate (old way)
RestTemplate rt = new RestTemplate();
User user = rt.getForObject("http://api/users/1", User.class);

// WebClient (new way)
WebClient client = WebClient.create("http://api");
Mono<User> user = client.get()
    .uri("/users/1")
    .retrieve()
    .bodyToMono(User.class);

// WebClient — blocking (use only when needed)
User userSync = client.get().uri("/users/1")
    .retrieve().bodyToMono(User.class).block();
```

> 💡 **Interview Tip:** Migrate to WebClient for all new projects. RestTemplate is deprecated but still widely found in existing codebases.

</details>

---

## 🎯 Bonus Questions

<details>
<summary><b>Q37. What is the difference between interface and abstract class?</b></summary>

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
<summary><b>Q38. What is a Functional Interface in Java?</b></summary>

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
<summary><b>Q39. What is the Stream API in Java?</b></summary>

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
<summary><b>Q40. What are all 4 OOP pillars? (Quick Reference)</b></summary>

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
<summary><b>Q41. What is a deadlock? How do you prevent it?</b></summary>

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
<summary><b>Q42. What are wrapper classes in Java?</b></summary>

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
<summary><b>Q43. What is the volatile keyword in Java?</b></summary>

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
<summary><b>Q44. What is Dependency Injection? How does Spring use it?</b></summary>

> **One-Line Answer:** Dependency Injection (DI) is a design pattern where an object receives its dependencies from outside (injected) rather than creating them itself — enabling loose coupling and testability.

### Without DI vs With DI

```java
// WITHOUT DI — tight coupling
class OrderService {
    private PaymentService payment = new PaymentService(); // hardcoded!
}

// WITH DI — loose coupling (Spring)
@Service
class OrderService {
    private final PaymentService payment;

    @Autowired  // Spring injects PaymentService
    OrderService(PaymentService payment) {
        this.payment = payment;
    }
}
```

### Three Types of Injection in Spring

| Type | Recommended? | Notes |
|------|-------------|-------|
| **Constructor Injection** | ✅ Yes — Best practice | Dependencies immutable, easier to test |
| **Setter Injection** | ✅ For optional dependencies | Allows re-injection |
| **Field Injection** (`@Autowired` on field) | ❌ Avoid | Hides dependencies, hard to test |

> 💡 **Interview Tip:** Always prefer constructor injection — it makes dependencies explicit, supports immutability (final fields), and enables unit testing without Spring container.

</details>

---

<details>
<summary><b>Q45. What is the difference between @Component, @Service, @Repository, @Controller?</b></summary>

> **One-Line Answer:** All four are Spring stereotypes that mark a class as a Spring-managed bean. They're functionally equivalent but carry semantic meaning and enable layer-specific behaviour.

### Comparison Table

| Annotation | Layer | Purpose | Extra Behaviour |
|-----------|-------|---------|----------------|
| **@Component** | Generic | Any Spring bean | None specific |
| **@Service** | Business | Business logic | Semantic clarity |
| **@Repository** | Data Access | DAO / database layer | Auto-translates DB exceptions to `DataAccessException` |
| **@Controller** | Web | Handles HTTP requests | Works with Spring MVC view resolution |
| **@RestController** | Web/REST | REST endpoints | = @Controller + @ResponseBody |

> 💡 **Interview Tip:** Always use the semantically correct annotation. `@Repository` especially matters because it enables automatic exception translation for the persistence layer.

</details>

---

<details>
<summary><b>Q46. What is the difference between @RequestParam and @PathVariable?</b></summary>

> **One-Line Answer:** @PathVariable extracts values from the URL path (`/users/{id}`). @RequestParam extracts values from query parameters (`/users?id=5`).

### Code Example

```java
// @PathVariable — part of the URL path
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
    return userService.findById(id);
}
// Call: GET /users/42

// @RequestParam — query parameter
@GetMapping("/users")
public List<User> getUsers(
    @RequestParam("city") String city,
    @RequestParam(value = "page", defaultValue = "0") int page) {
    return userService.findByCity(city, page);
}
// Call: GET /users?city=Mumbai&page=1
```

> 💡 **Interview Tip:** Use @PathVariable for identifying a resource (user ID, product ID). Use @RequestParam for filtering, sorting, or pagination parameters.

</details>

---

<details>
<summary><b>Q47. What is the difference between HashMap, LinkedHashMap, and TreeMap?</b></summary>

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
<summary><b>Q48. What are design patterns? Name the most common ones.</b></summary>

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
<summary><b>Q49. What is the difference between fail-fast and fail-safe iterators?</b></summary>

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
<summary><b>Q50. What is the difference between Stack and Heap memory?</b></summary>

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

*Happy Interview Preparation! ☕ — Remember: Understand the concept, then explain it simply with a real-world example.*
